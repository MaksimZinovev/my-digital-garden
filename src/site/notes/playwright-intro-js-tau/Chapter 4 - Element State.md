---
{"dg-publish":true,"permalink":"/playwright-intro-js-tau/chapter-4-element-state/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Chapter 4 - Element State

## Chapter 4 - Element State

Automatically checked by Playwright. Is Element:

- attached
- visible
- stable
- not being obscured by other elements 
- enabled
- editable

```JavaScript
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ slowMo: 100 });
  const page = await browser.newPage();
  await page.goto("https://demoqa.com/automation-practice-form");

  // print the element state

  const firstName = await page.$("#firstName");
  const sportsCheck = await page.$("#hobbies-checkbox-1");
  const submitBtn = await page.$("#submit");

  console.log(await firstName.isDisabled());
  console.log(await firstName.isEnabled());
  console.log(await firstName.isEditable());

  console.log(await sportsCheck.isChecked());
  console.log(await sportsCheck.isVisible());

  console.log(await submitBtn.isHidden());
  console.log(await submitBtn.isVisible());

  // closing gbrowser
  await browser.close();
})();

```