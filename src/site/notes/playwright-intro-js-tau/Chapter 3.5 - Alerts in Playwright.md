---
{"dg-publish":true,"dg-path":"courses/playwright-intro-js-tau/Chapter 3.5 - Alerts in Playwright.md","permalink":"/courses/playwright-intro-js-tau/chapter-3-5-alerts-in-playwright/","tags":["playwright"]}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza MOC\|TAU Course Playwright with JavaScript by Ixchel Meza MOC]]

# Chapter 3.5 - Alerts in Playwright

## Chapter 3.5 - Alerts in Playwright

```JavaScript
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 500 });
  const page = await browser.newPage();
  await page.goto("https://demoqa.com/alerts");
  // code to handle alerts
  // click 3rd button
  page.once("dialog", async (dialog) => {
    console.log(dialog.message());
    await dialog.accept();
  });
  await page.click("#confirmButton");
  // click 4th button
  page.once("dialog", async (dialog) => {
    console.log(dialog.message());
    await dialog.accept("my text is this");
  });
  await page.click("#promtButton");
  await browser.close();
})();

```