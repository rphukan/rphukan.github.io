---
title: 'Build your own website'
date: 2026-08-29T16:59:59+03:00
tags: ['Hugo', 'Github Pages', 'Blogging', "Personal Website"]
draft: false
---

# Github Pages and Hugo

> ### **1. Hosting on Github Pages**
You can create your website for free just using a Github repo. [GitHub Pages](https://docs.github.com/en/pages) is a static site hosting service provided by Github which turn your repository containing your website statc contents like HTML, CSS, and JavaScript files into a live website. 

Github Pages supports two types of sites 
* A site for a user or an organization account

The site is going to be available at `http(s)://<owner>.github.io`. Here `<owner>` is the account name of the account holder and `<owner>.github.io` is the repository name where all the site contents are stored. For eaxmple [this](https://rphukan.github.io/) is my personal website link where you are reading this blog. Since I have my personal domain linked on Github Pages, you will actually see it on `https//ranjanphukan.com`

* A site for your project 

This can be enabled for each of your repository and the site would be available at `http(s)://<owner>.github.io/<repositoryname>`. The contents for the site is stored in the `root` or `docs` folder of your repository. For example [this](https://rphukan.github.io/msr-documentation/) is the documentaion of a sample application that i have in my github account. 

You can write all your website contents in markdown files and GitHub Pages will use Jekyll to build your site by default from the markdown files. With this your site is ready and you should be able to access it on the urls as mentioned above.

But apart form the default Jekyll, we can also use a different static site generators for more flexibility which we will see next.


> ### **2. Generating the static contents of your site using Hugo**
[Hugo](https://gohugo.io/) is a static site generator written in [Go](https://go.dev/doc/) language. We would be using `Hugo` to generate our static contents.

To develop the site on your local, first install `Go` as `Hugo` runs using Go
#### **2.1. Install Go**
To install `Go` on windows you can use the below command. For other operating systems refer the [Go Documentation Page](https://go.dev/doc/)
```shell
PS C:\home\Projects> winget install GoLang.Go
Found Go Programming Language [GoLang.Go] Version 1.27.0
Downloading https://go.dev/dl/go1.27.0.windows-amd64.msi
  ██████████████████████████████  63.0 MB / 63.0 MB
Successfully verified installer hash
Starting package install...
Successfully installed
```

#### **2.2. Install Hugo**
Next you need to install `Hugo`. This is how you can install it on windows. For other Operating Systems refer the  [Hugo installation page](https://gohugo.io/installation/)
```shell
PS C:\home\Projects> winget install Hugo.Hugo.Extended
Do you agree to all the source agreements terms?
[Y] Yes  [N] No: y
Found Hugo (Extended) [Hugo.Hugo.Extended] Version 0.165.0
Downloading https://github.com/gohugoio/hugo/releases/download/v0.165.0/hugo_extended_0.165.0_windows-amd64.zip
  ██████████████████████████████  21.6 MB / 21.6 MB
Successfully verified installer hash
Extracting archive...
Successfully extracted archive
Starting package install...
Path environment variable modified; restart your shell to use the new value.
Command line alias added: "hugo"
Successfully installed
```

#### **2.3. Create your project and add a theme**
Hugo uses a templating system and uses a embeded webserver on local during development to instantly render the content on `http://localhost:1313/` by default. Create the skeleton of your content project in the `<owner>.github.io` folder using the command as shown below. 

```shell
PS C:\home\Projects> hugo new project rphukan.github.io
Congratulations! Your new Hugo project was created in C:\home\Projects\rphukan.github.io.

Just a few more steps...

1. Change the current directory to C:\home\Projects\rphukan.github.io.
2. Create or install a theme:
   - Create a new theme with the command "hugo new theme <THEMENAME>"
   - Or, install a theme from https://themes.gohugo.io/
3. Edit hugo.toml, setting the "theme" property to the theme name.
4. Create new content with the command "hugo new content <SECTIONNAME>\<FILENAME>.<FORMAT>".
5. Start the embedded web server with the command "hugo server --buildDrafts".

See documentation at https://gohugo.io/.
```

Once done select a theme from the [existing themse repo](https://themes.gohugo.io/). You can also add your own theme if you wish.

Now there are two ways to add a theme
* as a [Git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
* as a [Hugo Module](https://gohugo.io/hugo-modules/introduction/)

To keep it simple, we will add it as a Git submodule. For that you initialize your project folder as an empty git repository and add the selected theme repo as the submodule under the `themes/<theme-name>` folder
```shell
PS C:\home\Projects\rphukan.github.io> git init
Initialized empty Git repository in C:/home/Projects/rphukan.github.io/.git/

PS C:\home\Projects\rphukan.github.io> git submodule add https://github.com/hugo-porto/theme themes/hugo-porto
Cloning into 'C:/home/Projects/rphukan.github.io/themes/hugo-porto'...
```
Next to add this theme to your project, update your project's hugo congiguration file `hugo.toml` and add the below line where `<theme-name>` is `'hugo-porto'` in this example
```shell
theme = 'hugo-porto'
```
You can read this [theme's readme file](https://github.com/hugo-porto/theme) if you want to add this as a Hugo Module.

#### **2.4. Start Hugo server**
Now if you start the `Hugo Server` you should see the home page of your theme. We will further edit your site contents next.
You can use your `VS Code` `IDE` for editing the site contents. For testing the generated content on local you can start the `Hugo Server` from the `IDE Terminal` with the below command
```shell
PS C:\home\Projects\rphukan.github.io> hugo server --buildDrafts
Start building sites … 
hugo v0.165.0-76a5e1880ab46688155b02e99bab9be2a6134492+extended windows/amd64 BuildDate=2026-08-12T14:26:28Z VendorInfo=gohugoio
                  │ EN 
──────────────────┼────
 Pages            │  4 
 Paginator pages  │  0 
 Non-page files   │  0 
 Static files     │  0 
 Processed images │  0 
 Aliases          │  0 
 Cleaned          │  0 

Built in 3 ms
Environment: "development"
Serving pages from disk
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1) 
Press Ctrl+C to stop
```
Once tested on local you can push your changes to your Github Pages repo `<owner>.github.io`. We will add automated builds and deployment later.

#### **2.5. Understanding the project skeleton**
So far you only see the home page. next you would want to add some contents. For that first we will need to understand the structure of the content project skeleton that we have created above.

There are different subfolders in your content project that contribute to your content, site structure, behavior, and look and feel. They contain Hugo’s seven component types: static files, content, layouts, data, assets, internationalization (i18n) resources, and archetypes.
```yaml
rphukan.github.io/
├── archetypes/
│   └── default.md
├── assets/
├── content/
├── data/
├── i18n/
├── layouts/
├── static/
├── themes/
└── hugo.toml         <-- project configuration
```

This is what goes in these directories

* [`archetypes`](https://gohugo.io/content-management/archetypes/)
It contains templates for new contents. When you generate your website contents using the command `hugo new content`, Hugo creates a new file in the content directory, using an archetype in this folder as a template.

* [`assets`](https://gohugo.io/hugo-pipes/introduction/)
This contains resources like JavaScripts, CSS, images etc. 

* [`content`](https://gohugo.io/content-management/organization/)
The content folder conatins your site contents. You create your site contents in markup(markdonw mostly) files and structured in the same manner as its rendered on your site. As an example this is how my contents would be structured
```yaml
└── content
    └── about
    |   └── index.md  // <- https://ranjanphukan.com/about/
    ├── posts
    |   ├── personal-website
    |   |   └── index.md  // <- https://ranjanphukan.com/posts/personal-website/
```

* [`data`](https://gohugo.io/content-management/data-sources/)
The data directory contains data in JSON, TOML, YAML, or XML files. Hugo creates a data structure with these data which you can use in a template in your content.

* [`i18n`](https://gohugo.io/content-management/multilingual/)
This directory is for for localizing your contents with different languages.

* [`layouts`](https://gohugo.io/templates/introduction/)
The layout folder would contain the templates for laying out your site structure. Your theme should already provide you a layout but if you want to override that default behaviour, you would do it here with your own layout templates. Start with the default one provided by the theme and if required you can override it later.

*   `static`
The static directory contains files that will be copied to the public directory when you build your project. This can also contain CSS and JavaScript files, though the new aproach for them is the `assets` directory.

* [`themes`](https://gohugo.io/getting-started/directory-structure/#theme-skeleton)
This is where you add your themse as Git submodules. Hogo themes work using the Hugo [unified file system](https://gohugo.io/quick-reference/glossary/#unified-file-system) and uses the same directories that we have discussed here. This allows you to override a theme’s template by adding your own copy of it in the same location within the project directory.

Apart from the above, you may also see the below two folders which Hugo build generates on your local with the generated built contents. You do not push these two folders to your Gitbug Pages repo.
```yaml
rphukan.github.io/
├── public/
├── resources/
```
* `public`
The public directory contains the published website, generated when you run the hugo build or hugo server commands. 

* `resources`
This is generated when you run the hugo build or hugo server commands.It contains cached output and by default includes CSS and images. 


#### **2.6. Adding your contents**
Now that we have understood the skeleton of our content project, lets add our first content. Run the below command from your terminal and it would create your a content under `content/posts`. 
```shell
hugo new content content/posts/my-first-post.md
```
If you open the markdown file `my-first-post.md` file created under `content/posts` you will see that your post starts with some [front matters](https://gohugo.io/content-management/front-matter/). Your write your content after that front matter block
```yaml
---
  title: 'My First Post'
  date: 2026-09-12T11:40:18+05:30
  draft: true
---
your content goes here
```
Notice the `draft=true` front matter. By default, Hugo does not publish draft content when you build the project. Start the Hugo server to include the draft contents with the below commands and you should see your first page.
```shell
hugo server --buildDrafts
hugo server -D
```
The terminal should print the localhost url after the server starts. Use that to view your post on browser.

Congratulations!!!!! You are ready now to write your post.

You can keep editing your post. The server running on local should automatically render the updated content on your browser. Once ready you can change `draft: false` and push the updated contents to the Github Pages repo. If you have the automated build ( which we will see after few steps) configured on Githug Pages, you will see your post on your live site after few moments later.

#### **2.7. Advance(Optional) : Changing the layout**
As explained before `layouts` directory would contain the layout templates for your site. They are already created in your theme. But if we want to change it, we would be doing it in this directory.

A template is a file with template actions, located within the layouts directory of a project, theme, or module. Templates use variables, functions, and methods to transform your content, resources, and data into a published page.

This is a simple structure of templates that we will explain. [Refer for more details](https://gohugo.io/templates/types/)
```yaml
layouts/
├── _default/
│   ├── baseof.html   
│   |── home.html    
│   ├── single.html   
│   └── list.html    
├── _partials/
│   ├── footer.html
│   └── header.html
├── about/
    └── single.html

```
* `baseof` - This is the foundational base template that the other templates would use. It would typically have the common elements of your html pages like html, head, and body. Putting them in a base template allows for consistency and avoids redundancy.

* `home` - A home template renders your site’s home page. 

* `single` - A single template is used to renders a regular page. (This is a fallback for a page template)

* `list` - This template renders a list of pages. (This is a fallback for home, section, taxonomy, and term templates)

Usually you would apply the base template to these above templates.

* `partials` - A partial template is typically used to render a component of your site. Its called from an another template.

Hugo considers below parameters when choosing a template for a given page.

* `Kind`
The Kind of the page, e.g. the home page. This also determines if it is a single page (i.e. a regular content page). We then look for a template in _default/single.html for HTML.  Or a list page (section listings, home page, taxonomy lists, taxonomy terms) in which case we look for a template in _default/list.html for HTML.

* `Layout`
A front matter which can be set in your page.

* `Type`
A front matter which can be set in your page.

Now lets say we want to change the layout of a new `about` page
```yaml
content/
└── about/
    └── index.md
```
We can make this content page to target a template by specify type, layout, or both in front matter as shown below.
In your file `content/about/index.md` add
```yaml
---
title: 'About Me'
draft: false
layout: "single"
type: "about"
---
```


#### **2.8. Advance(Optional) : Using mathematical expressions**
You can write mathematical equations in Markdown using LaTeX markup. [More details](https://gohugo.io/content-management/mathematics/)

#### **2.8. Advance(Optional) : Adding mermaid diagrams**
To display mermaid diagram on your page [refer this](https://gohugo.io/content-management/diagrams/)


> ### **3. Automatic build and deployment of your content using Github actions**
If we use a static site generator other than Jekyll, we need t you write a GitHub Actions to build and publish ous site.

Add the below workflow in a file like `.github/workflows/hugo.yaml` under the root folder of your website repo. Here action `actions/configure-pages@v5` enables the use of GitHub Pages.

In this workflow Hugo reads contents from content, layouts from layouts, data from data, assets, configuration, and the theme. It generates the complete static website in temporary `./public/` folder of the runner. The action `actions/upload-pages-artifact@v3` then uploads the files to GitHub’s temporary Actions artifact storage. They are not committed or pushed back into the repository. Finally the `actions/deploy-pages@v4` action publishes the uploaded artifacts to our Github Pages site.

Refer [this page](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages) for more details

```yaml
name: Build and deploy
on:
  push:
    branches:
      - master
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: pages
  cancel-in-progress: false
defaults:
  run:
    shell: bash
jobs:
  build:
    runs-on: ubuntu-latest
    env:
      DART_SASS_VERSION: 1.98.0
      GO_VERSION: 1.26.1
      HUGO_VERSION: 0.158.0
      NODE_VERSION: 24.14.0
      TZ: Europe/Oslo
    steps:
      - name: Checkout
        uses: actions/checkout@v6
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Go
        uses: actions/setup-go@v6
        with:
          go-version: ${{ env.GO_VERSION }}
          cache: false
      - name: Setup Node.js
        uses: actions/setup-node@v6
        with:
          node-version: ${{ env.NODE_VERSION }}
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Create directory for user-specific executable files
        run: |
          mkdir -p "${HOME}/.local"
      - name: Install Dart Sass
        run: |
          curl -sLJO "https://github.com/sass/dart-sass/releases/download/${DART_SASS_VERSION}/dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          tar -C "${HOME}/.local" -xf "dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          rm "dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          echo "${HOME}/.local/dart-sass" >> "${GITHUB_PATH}"
      - name: Install Hugo
        run: |
          curl -sLJO "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          mkdir "${HOME}/.local/hugo"
          tar -C "${HOME}/.local/hugo" -xf "hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          rm "hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          echo "${HOME}/.local/hugo" >> "${GITHUB_PATH}"
      - name: Verify installations
        run: |
          echo "Dart Sass: $(sass --version)"
          echo "Go: $(go version)"
          echo "Hugo: $(hugo version)"
          echo "Node.js: $(node --version)"
      - name: Install Node.js dependencies
        run: |
          [[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true
      - name: Configure Git
        run: |
          git config core.quotepath false
      - name: Cache restore
        id: cache-restore
        uses: actions/cache/restore@v5
        with:
          path: ${{ runner.temp }}/hugo_cache
          key: hugo-${{ github.run_id }}
          restore-keys:
            hugo-
      - name: Build the site
        run: |
          hugo build \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/" \
            --cacheDir "${{ runner.temp }}/hugo_cache"
      - name: Cache save
        id: cache-save
        uses: actions/cache/save@v5
        with:
          path: ${{ runner.temp }}/hugo_cache
          key: ${{ steps.cache-restore.outputs.cache-primary-key }}
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

> ### **4. Adding your own domain**
Finally you can buy a nice domain from any of the domain registrars and [add it to your Github Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)