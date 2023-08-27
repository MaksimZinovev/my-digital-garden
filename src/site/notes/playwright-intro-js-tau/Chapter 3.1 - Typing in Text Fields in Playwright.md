---
{"dg-publish":true,"dg-path":"courses/playwright-intro-js-tau/Chapter 3.1 - Typing in Text Fields in Playwright.md","permalink":"/courses/playwright-intro-js-tau/chapter-3-1-typing-in-text-fields-in-playwright/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Chapter 3.1 - Typing in Text Fields in Playwright

## Chapter 3.1 - Typing in Text Fields in Playwright

```js
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, sloMo: 100 });
  const page = await browser.newPage();
  await page.goto("https://the-internet.herokuapp.com/forgot_password");
  // code to type in email textbox
  // const email = page.locator('#email');
  const email = page.$("#email"); 
  await email.type("maxfaber82@gmail.com", { delay: 50 });
  // await page.type('#email', 'masfsdf@dfgfd.com', {delay: 50});
  await browser.close();
})();

```