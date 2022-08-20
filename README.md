
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
- cmd: hugo new posts/{name-of-post}.md


