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

## NPM proxy

```bash
npm config set proxy http://proxy.company.com:3128
npm config set https-proxy http://proxy.company.com:3128
```

## Convert Time
```javascript
let date = moment("01/23/18", ["MM/DD/YY", "M/DD/YY", "MM/D/YY", "M/D/YY"], true)
if (date.isValid()) {
    console.log(date.format("DD.MM.YY"))
}
```