---
title: Javascript
taxonomy:
    category:
        - Others
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

## NPM proxy

```bash
npm config set proxy http://proxy.company.com:3128
npm config set https-proxy http://proxy.company.com:3128
```