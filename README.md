
# landing-page
Landing page of BISC

## Requirements
- [x] Pages: Welcome, contact, sponsors (thanks), link to recruitment page.
- [ ] Pages:  members, achievements
- [ ] Academic profile for teacher (embed google scholar profile https://scholar.google.com/citations?user=ha11OwIAAAAJ&hl=vi), link to BISC landing page
## Set up:
- Requirement: latest Hugo extended
- Modified variable in config.toml file to change the website content

### Change sponsor icon images
- Add images to static/images
- add link to modified images[] in [param.footer]

### All content of website is save in "content/" and can be write using Markdown languauge

#### About and Contact can be modified on content/ about.md and contact.md
#### Add a new posts
- cmd: hugo new posts/{name-of-post}.md will create a new post in content/posts

## Built-in shortcodes

Of course you are able to use all default shortcodes from hugo (https://gohugo.io/content-management/shortcodes/).

### image

Properties:

  - `src` (required)
  - `alt` (optional)
  - `position` (optional, default: `left`, options: [`left`, `center`, `right`])
  - `style`

Example:

``` golang
{{< image src="/img/hello.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}
```

### Code highlighting

By default the theme is using PrismJS to color your code syntax. All you need to do is to wrap you code like this:

<pre>
``` html
  // your code here
```
</pre>

### Favicon

Check the [docs](docs/favicons.md).

### Audio Support

You wrote an article and recorded it? Or do you have a special music that you would like to put on a certain article? Then you can do this now without further ado.

In your article add to your front matters part:

```yaml
audio: path/to/file.mp3
```

## Social Icons:

A large variety of social icons are available and can be configured like this:

```toml
[[params.social]]
  name = "<site>"
  url = "<profile_URL>"
```

Take a look into this [list](docs/svgs.md) of available icon options. 

If you need another one, just open an issue or create a pull request with your wished icon. :)


