---
{"dg-publish":true,"dg-path":"courses/playwright-intro-js-tau/Chapter 6 - Mouse Events.md","permalink":"/courses/playwright-intro-js-tau/chapter-6-mouse-events/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Chapter 6 - Mouse Events

## Chapter 6 - Mouse Events

```js
const { chromium } = require('playwright');
(async() => {
// function code
const browser = await chromium.launch({headless: false, slowMo: 300});
const page = await browser.newPage();
await page.goto('https://paint.js.org/');

// interacting with mouse
await page.mouse.move(200,200); 
await page.mouse.down();
await page.mouse.move(400,200);
await page.mouse.move(400,400);
await page.mouse.move(200,400);
await page.mouse.move(200,200);
await page.mouse.up();

await browser.close();
})();
```