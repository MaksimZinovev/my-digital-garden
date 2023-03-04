---
{"dg-publish":true,"permalink":"/playwright/chapter-2-writing-your-first-playwright-script/","tags":["playwright"]}
---

links:: [[TAU Course Playwright with JavaScript by Ixchel Meza 1\|TAU Course Playwright with JavaScript by Ixchel Meza 1]]

# Chapter 2 - Writing Your First Playwright Script

## Chapter 2 - Writing Your First Playwright Script

```js
const { chromium } = require('playwright');
(async() => {
// function code
const browser = await chromium.launch({headless: false, sloMo: 100});
const page = await browser.newPage();
await page.goto('http://google.com');
await browser.close();
})();


```

```shell
node first.js
```