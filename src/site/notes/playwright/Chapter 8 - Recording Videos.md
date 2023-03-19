---
{"dg-publish":true,"permalink":"/playwright/chapter-8-recording-videos/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Chapter 8 - Recording Videos

## Chapter 8 - Recording Videos

```javascript
const { chromium } = require('playwright');
(async() => {
// function code
const browser = await chromium.launch({headless: false, slowMo: 100});

// creating a page inside  browser
const context = await browser.newContext({
    recordVideo: {
        dir: "./recordings"
    }
});
const page = await context.newPage();


await page.goto('https://the-internet.herokuapp.com/dynamic_loading/1');

// click on button 
await page.click('button'); 
await page.waitForSelector('#loading');
await page.waitForSelector('#loading', {state: 'hidden'});
await page.waitForTimeout(100);

await browser.close();
})();
```