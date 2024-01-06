---
{"dg-publish":true,"dg-path":"courses/playwright-intro-js-tau/Chapter 8 - Recording Videos.md","permalink":"/courses/playwright-intro-js-tau/chapter-8-recording-videos/","tags":["playwright"]}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza MOC\|TAU Course Playwright with JavaScript by Ixchel Meza MOC]]

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