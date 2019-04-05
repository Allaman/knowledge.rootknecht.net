---
title: Revealjs
taxonomy:
    category:
        - Application
---

[Revealjs](https://github.com/hakimel/reveal.js/) is a framework for producing nice looking HTML presentations.

[Here](https://open.rootknecht.io/revealjs-intro/#/) you can find a presentation which I created to illustrate Revealjs and [here](https://repo.rootknecht.net/open/revealjs-intro) is the repo with its source code.

## Frontmatter

```toml
---
title: Revealjs Introduction
theme : "moon"
transition: "zoom"
highlightTheme: "darkula"
slidenumber: true
separator: ^---
verticalSeparator: ^--
showNotes: true ## Export notes in pdf
## showNotes: "separate-page" for longer notes
---
```

## Image formating

for `reveal-md`
```
![](bad.jpg) <!-- .element height="65%" width="65%" -->
```
for `pandoc`
```
![](image.png){#id .class width=65% height=65%}
```

## Slide background

for `reveal-md`
```html
<!-- .slide: data-background="./background.png" -->
<!-- .slide: style="color:yellow" -->
```
for `pandoc`
```html
# {data-background-image="background.jpg"}
```

## Bulletpoints animation

```markdown
* Emacs, VS Code, Vim <!-- .element: class="fragment" -->
* R Studio, Jupyter <!-- .element: class="fragment" -->
* reveal-md Pandoc <!-- .element: class="fragment" -->
```

## Generate static HTML files

with `reveal-md`
```sh
reveal-md -css custom.css presentation.md --static public
```

with `pandoc`
```sh
pandoc -t revealjs -s -o public/index.html presentation.md -V revealjs-url=reveal.js --css=custom.css --slide-level=2 [--self-contained]
```