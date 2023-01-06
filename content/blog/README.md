# Note For Blog Contributers
In /content/blog/web/sekai-ctf-2022-bottle-poem holds an example for a blog contribution. The only important things you need to take away is the front matter fields name.

## Blog create
From the `Workspace Directory`, type this command in terminal:

```
hugo new blog/<your category>/<file-name-with-hypens-only>.md
```
Currently there are 4 major categories: web, re (reverse engineering), crypto, pwn. Feel free to add another category if necessary just create new folder named `<category_name>` inside /content/blog. 

### Images
Since BKISC use roxo-theme, we recommend you specify 2 fields in the front matter: images and feature_image
- `images`  
    - Will be the image of the blog if the blog list page, the one user will see before clicking to access that blog. Recommend upload or (choose if existed) the Organization related image (for example an CTFs writeup for SekaiCTF 2022 challenge should pick the SekaiCTF logo).
    - Upload path: /static/images/blog/organiztion/`<ctf or wargame or>`/... (to help later refercences for others)
- `feature_image` 
    - The hero image place on that blog header
    - Upload path: /static/images/blog/`<your categories>`/`<the-blog-file-name-with-hypens>`/... (help seperate blog by blog)
- Others image use as {{figure}} shortcodes in blog's content also use /static/images/blog/`<your categories>`/`<the-blog-file-name-with-hypens>`/... path

## Blog Format
Below is an example of a blog
```
--- # 1. Front matter
title: "Sekai Ctf 2022 Bottle Poem"
date: 2023-01-06T10:27:19+07:00
image: images/blog/web/sekai-ctf-2022-bottle-poem/sekai-ctf-2022-logo.png
feature_image: images/blog/web/sekai-ctf-2022-bottle-poem/sekai-ctf-2022-logo.png
author: duti
tags: ["web", "ctf", "duti"]
draft: true
---

# 2. Cotent

### Problem statement

{{< figure src="/images/blog/web/sekai-ctf-2022-bottle-poem/problem-statement.png" title="" >}}
Author hints that flag is executable
...
```
Follow Hugo convention, content file contains 2 parts:
- Front Matters
- Content

### Front Matters
Contains these field:

1. title

    - Type: string
    - Example value: ` MyNSUCrypto 2022 Writeups`

2. date
    - Type: string
    - Is auto-generated if `hugo new blog` command is used

3. author
    - Type: string
    - Value: your nickname

4. images
    - Type: string
    - Pattern: /static/images/blog/organiztion/`<ctf or wargame or>`/...

5. features_images
    - Type: string
    - Pattern: /static/images/blog/`<your categories>`/`<the-blog-file-name-with-hypens>`/..

6. tags
    - Type: array of string
    - Note: recommend placing your name here, currently we are not having support for filter blogs by author
    - Example: `["duti", "web", "ctf"]`