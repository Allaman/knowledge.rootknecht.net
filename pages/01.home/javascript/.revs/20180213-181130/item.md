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

## Convert Time
```javascript
let date = moment("01/23/18", ["MM/DD/YY", "M/DD/YY", "MM/D/YY", "M/D/YY"], true)
if (date.isValid()) {
    console.log(date.format("DD.MM.YY"))
}
```

## Check for undefined and not null
```javascript
if (typeof(variable) != "undefined" && variable) {
	console.log("Good")
}
```

## For loops
```javascript
for (let input of inputs) {
    console.log(input)
}
```

## Transpiler error lines mapping
Add to your entrypoint the following snippet
```javascript
require('source-map-support').install()
```
```bash
npm install dev-dependencies source-map-support
```