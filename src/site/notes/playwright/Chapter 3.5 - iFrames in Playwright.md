---
{"dg-publish":true,"permalink":"/playwright/chapter-3-5-i-frames-in-playwright/","tags":["playwright"]}
---

links:: [[TAU Course Playwright with JavaScript by Ixchel Meza 1\|TAU Course Playwright with JavaScript by Ixchel Meza 1]]

# Chapter 3.5 - iFrames in Playwright

## Chapter 3.5 - iFrames in Playwright

```JavaScript
const { webkit } = require("playwright");
(async () => {
  // function code
  const browser = await webkit.launch({ headless: false, slowMo: 200 });
  const page = await browser.newPage();
  await page.goto("https://demoqa.com/frames");
  // logic to handle iframe
  const frame1 = await page.frame({ url: /\/sample/ });
  const heading1 = await frame1.$("h1");
  console.log(await heading1.innerText());
  await browser.close();
})();
sole.log(await heading1.innerText());
await browser.close();
})();

```