# Install mkdocs-material

```bash
# Install mkdocs before

mkdocs new <my-project>
cd <my-project>
pip install mkdocs-material
# add image zoom feature
pip install mkdocs-glightbox
```

> Add line to `mkdocs.yml` :

```yaml
theme:
  name: material
```

> Run or deploy on Github

```yml
site_name: <your_site_name>
site_url: https://<account>.github.io/<your_site_name>
site_author: your name
site_description: >-
  Efxdev docs, exercices, tips on web technologies and tools
# Repository
repo_name: <account>/<your_site_name>
repo_url: https://github.com/<account>/<your_site_name>
```

```bash
# Run in local
mkdocs serve
# deploy on github page :
# info with : mkdocs gh-deploy --help
mkdocs gh-deploy
```

> If you want custom material template add in `mkdocs.yml` :

```yml
theme:
  name: material
  custom_dir: overrides
```

The structure in the `overrides` directory must mirror the directory structure of the original theme, as any file in the `overrides` directory will replace the file with the same name which is part of the original theme. Besides, further assets may also be put in the `overrides` directory:

```textile
.
├─ .icons/                             # Bundled icon sets
├─ assets/
│  ├─ images/                          # Images and icons
│  ├─ javascripts/                     # JavaScript files
│  └─ stylesheets/                     # Style sheets
├─ partials/
│  ├─ integrations/                    # Third-party integrations
│  │  ├─ analytics/                    # Analytics integrations
│  │  └─ analytics.html                # Analytics setup
│  ├─ languages/                       # Translation languages
│  ├─ content.html                     # Page content
│  ├─ copyright.html                   # Copyright and theme information
│  ├─ footer.html                      # Footer bar
│  ├─ header.html                      # Header bar
│  ├─ language.html                    # Translation setup
│  ├─ logo.html                        # Logo in header and sidebar
│  ├─ nav.html                         # Main navigation
│  ├─ nav-item.html                    # Main navigation item
│  ├─ palette.html                     # Color palette
│  ├─ search.html                      # Search interface
│  ├─ social.html                      # Social links
│  ├─ source.html                      # Repository information
│  ├─ source-file.html                 # Source file information
│  ├─ tabs.html                        # Tabs navigation
│  ├─ tabs-item.html                   # Tabs navigation item
│  ├─ toc.html                         # Table of contents
│  └─ toc-item.html                    # Table of contents item
├─ 404.html                            # 404 error page
├─ base.html                           # Base template
└─ main.html                           # Default page
```

> See the detail of files in : `~/Desktop/dev/docs/templates/mkdocs-material`

[Extending MkDocs Material Docs](https://squidfunk.github.io/mkdocs-material/customization/#extending-the-theme)

# Custom mkdocs-material template

```bash
git clone https://github.com/squidfunk/mkdocs-material
cd mkdocs-material
pip install -e .
pip install mkdocs-minify-plugin
pip install mkdocs-redirect
npm install

mkdocs serve
# ?
mkdocs serve --watch-theme
```

# Doc & source

[mkdocs-material Git](https://github.com/squidfunk/mkdocs-material)

[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)

[Customization - Material for MkDocs](https://squidfunk.github.io/mkdocs-material/customization/)

# Installing the dev

```bash
git clone https://github.com/squidfunk/mkdocs-material
```

Next, all dependencies need to be installed, which is done with:

```bash
cd mkdocs-material
pip install -e .
pip install mkdocs-minify-plugin
pip install mkdocs-redirects
npm install
```

Start the watcher:

```bash
npm start
```

and in a seconde bash launch the preview:

```bash
mkdocs serve --watch-theme
```

[Doc Installing dev of Material for MkDocs](https://squidfunk.github.io/mkdocs-material/customization/#theme-development)
