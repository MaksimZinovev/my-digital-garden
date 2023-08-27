---
{"dg-publish":true,"dg-path":"courses/playwright-intro-js-tau/Chapter 3.3 - Dropdowns in Playwright.md","permalink":"/courses/playwright-intro-js-tau/chapter-3-3-dropdowns-in-playwright/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Chapter 3.3 - Dropdowns in Playwright

## Chapter 3.3 - Dropdowns in Playwright

```JavaScript
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 400 });
  const page = await browser.newPage();
  await page.goto("https://the-internet.herokuapp.com/dropdown");
  const dropdown = await page.$("#dropdown");
  //value
  await dropdown.selectOption({ value: "1" });
  // label
  await dropdown.selectOption({ label: "Option 2" });
  // index
  await dropdown.selectOption({ index: 1 });
  // print text in options elements
  const availableOptions = await dropdown.$$("option");
  for (let i = 0; i < availableOptions.length; i++) {
    console.log(await availableOptions[i].innerText());
  }
  await browser.close();
})();
```