
# BKISC Page
Landing page of BKISC

## Roadmap
### Current
- [x] Pages: Welcome, contact, sponsors (thanks), link to recruitment page, achievements.
- [x] Pages: Blog
- [ ] README update for Blog Contribution guide

### Next week
- [ ] Github Workflow + JS Script for validating commits content
- [ ] Figure out themes mix-match if possbile between [Roxo](https://github.com/StaticMania/roxo-hugo) and [Loveit](https://hugoloveit.com/)
- [ ] Latex shortcodes support for Cryptography bloggers
- [ ] Taxonomies: [ctf, web, re, crypto, pwn, root-me, wsa, nsucrypto, istdtu]
- [ ] Blog by Timeline (By Year-month)
- [ ] Blog by Author

### Future
- [ ] Pages:  members
- [ ] Academic profile for teacher advisor (embed google scholar profile https://scholar.google.com/citations?user=ha11OwIAAAAJ&hl=vi)

## Installation and Run:
- Installation Hugo Extended binart [guide](https://gohugo.io/installation/)

## Localhost development run and testing
- Run ````hugo server -D -w```` to start the Hugo server with draft content and hot reload features
- Run ````hugo -D```` to build static pages with draft

## Contribution Guide
1. Fork project repository
1. Checkout `contribute-blog` branch
1. Create your content file in `/content` folder and add images. Please follow [Note For Blog Contributers](./content/blog/README.md) for detail explanation.
1. Open your favorite editor and add content
```
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
...
```
5. Stage and commit new file, please just add 1 markdown content file only in each commit and each pull request just contains 1 commit.

`Note: Commit message must comply with below format for easy read`  
    - Adding a blog: `Add: <category>/file-name.md`  
    - Delete a blog: `Delete: <category>/file-name.md`  
    - Modify a blog: `Modified: <category>/file-name.md`  

6. Push the commit to your username remote codeql-cheatsheet repository, then create a pull request from \<your-username\>/bkisc.com's `contribute-blog` branch to BKISC/bkisc.com's `main` branch.

## Raising Issue
If you want to request a new feature, encounter a bugs or having questions, please [raise issues](https://github.com/clbattthcmut/bkisc.com/issues).

## Change sponsor icon images
- Add images to `static/images/clients`
- Add link to modified images[] in [param.footer]


# Reference
## Themes
Currently BKISC landing page are using only [roxo-hugo](https://github.com/StaticMania/roxo-hugo) theme. We will try adding more shortcodes support from [LoveIt](https://hugoloveit.com/) after figuring out how to mix-match 2 themes.