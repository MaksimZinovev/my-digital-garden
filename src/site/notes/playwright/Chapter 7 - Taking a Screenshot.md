---
{"dg-publish":true,"permalink":"/playwright/chapter-7-taking-a-screenshot/","tags":["playwright"]}
---

links:: [[TAU Course Playwright with JavaScript by Ixchel Meza 1\|TAU Course Playwright with JavaScript by Ixchel Meza 1]]

# Chapter 7 - Taking a Screenshot

## Chapter 7 - Taking a Screenshot

```javascript
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 300 });
  const page = await browser.newPage();
  await page.goto("https://applitools.com/");

  // take screenshot code

  // await page.screenshot({ path: "screenshot.png" });

  // take screenshot of the element
  const logo = await page.$(".logo");
 // await logo.screenshot({ path: "logo.png" });

  // take screenshot of the full page

  await page.screenshot({ path: "fullpage.png", fullPage: true });

  await browser.close();
})();
```