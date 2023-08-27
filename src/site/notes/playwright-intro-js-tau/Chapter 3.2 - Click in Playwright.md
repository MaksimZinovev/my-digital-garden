---
{"dg-publish":true,"permalink":"/playwright-intro-js-tau/chapter-3-2-click-in-playwright/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Chapter 3.2 - Click in Playwright

## Chapter 3.2 - Click in Playwright

- [First Music Lesson - Frequency, Octave, Semitone, Sound Names, Major Scale](https://www.apronus.com/music/lessons/unit01.htm)

```js
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 2000 });
  const page = await browser.newPage();
  // await page.goto("https://www.apronus.com/music/lessons/unit01.htm");
  await page.goto("https://www.apronus.com/music/lessons/unit01.htm");
  // code to type click 
  // page.pause() will open Playwright Inspector
  // await page.pause();
  await page.click('#t1 > table > tr:nth-child(1) > td:nth-child(1) > button');
  await browser.close();
})();await browser.close();
})();

```