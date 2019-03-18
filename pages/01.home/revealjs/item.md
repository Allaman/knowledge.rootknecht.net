---
title: Revealjs
media_order: revealjs-quickstart.html
taxonomy:
    category:
        - Application
---

Revealjs is a framework for producing nice looking HTML presentations.

[Here](https://open.rootknecht.io/revealjs-intro/#/) you can find a presentation which I created to illustrate revealjs.

[Here](https://repo.rootknecht.net/open/revealjs-intro) is the repo with the source code.

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

```
![](bad.jpg) <!-- .element height="65%" width="65%" -->
```

## Slide background

```html
<!-- .slide: data-background="./background.png" -->
<!-- .slide: style="color:yellow" -->
```

## Bulletpoints animation

```markdown
* Emacs, VS Code, Vim <!-- .element: class="fragment" -->
* R Studio, Jupyter <!-- .element: class="fragment" -->
* reveal-md Pandoc <!-- .element: class="fragment" -->
```