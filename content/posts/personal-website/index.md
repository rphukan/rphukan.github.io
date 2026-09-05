---
title: 'Build your own website'
date: 2024-04-26T16:59:59+03:00
tags: ['Hugo', 'Github Pages', 'Blogging', "Personal Website"]
draft: true
---
# Hugo and Github pages

Pellentesque congue. Ut in risus volutpat libero pharetra tempor. Cras vestibulum bibendum augue. Praesent egestas leo
in pede. Praesent blandit odio eu enim. Pellentesque sed dui ut augue blandit sodales.

Maecenas ligula massa, varius a, semper congue, euismod non, mi. Cras elementum ultrices diam. Maecenas ligula massa,
varius a, semper congue, euismod non, mi.

<!--more-->

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed non risus. Suspendisse lectus tortor, dignissim sit amet,
adipiscing nec, ultricies sed, dolor. Cras elementum ultrices diam. Maecenas ligula massa, varius a, semper congue,
euismod non, mi.

Proin porttitor, orci nec nonummy molestie, enim est eleifend mi, non fermentum diam nisl sit amet erat. Duis semper.
Duis arcu massa, scelerisque vitae, consequat in, pretium a, enim.

## Install Go
```shell
PS C:\home\Projects> winget install GoLang.Go
Found Go Programming Language [GoLang.Go] Version 1.27.0
This application is licensed to you by its owner.
Microsoft is not responsible for, nor does it grant any licenses to, third-party packages.
Downloading https://go.dev/dl/go1.27.0.windows-amd64.msi
  ██████████████████████████████  63.0 MB / 63.0 MB
Successfully verified installer hash
Starting package install...
Successfully installed
```

## Install Hugo
```shell
PS C:\home\Projects> winget install Hugo.Hugo.Extended
The `msstore` source requires that you view the following agreements before using.
Terms of Transaction: https://aka.ms/microsoft-store-terms-of-transaction
The source requires the current machine's 2-letter geographic region to be sent to the backend service to function properly (ex. "US").

Do you agree to all the source agreements terms?
[Y] Yes  [N] No: y
Found Hugo (Extended) [Hugo.Hugo.Extended] Version 0.165.0
This application is licensed to you by its owner.
Microsoft is not responsible for, nor does it grant any licenses to, third-party packages.
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

## Start Hugo server
```shell
(base) PS C:\home\Projects\Blog\rphukan.github.io> hugo server
WARN  deprecated: project config key languageCode was deprecated in Hugo v0.158.0 and will be removed in a future release. Use locale instead.
hugo: downloading modules …
hugo: collected modules in 35509 ms
Watching for changes in C:/home/Projects/Blog/rphukan.github.io/archetypes, C:/home/Projects/Blog/rphukan.github.io/assets/{css,img}, C:/home/Projects/Blog/rphukan.github.io/content/{about,posts}, C:/home/Projects/Blog/rphukan.github.io/data/sections, C:/home/Projects/Blog/rphukan.github.io/layouts/{_default,_markup,about,partials}, C:/home/Projects/Blog/rphukan.github.io/package.json, C:/home/Projects/Blog/rphukan.github.io/static/{css,files}
Watching for config changes in C:\home\Projects\Blog\rphukan.github.io\hugo.toml, C:\home\Projects\Blog\rphukan.github.io\go.mod
Start building sites … 
hugo v0.165.0-76a5e1880ab46688155b02e99bab9be2a6134492+extended windows/amd64 BuildDate=2026-08-12T14:26:28Z VendorInfo=gohugoio

WARN  deprecated: .Language.LanguageCode was deprecated in Hugo v0.158.0 and will be removed in a future release. Use .Language.Locale instead.
WARN  deprecated: .Language.LanguageDirection was deprecated in Hugo v0.158.0 and will be removed in a future release. Use .Language.Direction instead.
WARN  deprecated: .Site.Data was deprecated in Hugo v0.156.0 and will be removed in a future release. Use hugo.Data instead.

                  │ EN 
──────────────────┼────
 Pages            │ 17 
 Paginator pages  │  0 
 Non-page files   │  1 
 Static files     │  3 
 Processed images │  3 
 Aliases          │  4 
 Cleaned          │  0 

Built in 88 ms
Environment: "development"
Serving pages from disk
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1) 
Press Ctrl+C to stop
```