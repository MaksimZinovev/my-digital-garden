---
{"dg-publish":true,"dg-path":"courses/playwright-intro-js-tau/Chapter 5 - Managing a Virtual Keyboard.md","permalink":"/courses/playwright-intro-js-tau/chapter-5-managing-a-virtual-keyboard/","tags":["playwright"]}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza MOC\|TAU Course Playwright with JavaScript by Ixchel Meza MOC]]

# Chapter 5 - Managing a Virtual Keyboard

## Chapter 5 - Managing a Virtual Keyboard

```js
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 100 });
  const page = await browser.newPage();
  await page.goto("https://the-internet.herokuapp.com/key_presses");

  // handling keyboard

  await page.click("input");
  await page.keyboard.type("one does not simply exit vim");
  await page.keyboard.down("Shift");

  for (let i = 0; i < " exit vim".length; i++) {
    await page.keyboard.press("ArrowLeft");
  }
  await page.keyboard.up("Shift");
  await page.keyboard.press("Backspace");
  await page.keyboard.type(" walk into Mordor");

  await browser.close();
})();

```