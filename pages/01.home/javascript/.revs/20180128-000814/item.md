---
title: Javascript
taxonomy:
    category:
        - Others
    author:
        - Knecht
---

## File globbing

```javascript
glob.sync("../*/*.xlsm").forEach(function (file) {
    console.log(file)
});
```

## Read subfolders

```javascript
dirs = FS.readdirSync(path)
```