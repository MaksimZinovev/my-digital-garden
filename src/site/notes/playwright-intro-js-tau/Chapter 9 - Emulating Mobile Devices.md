---
{"dg-publish":true,"dg-path":"courses/playwright-intro-js-tau/Chapter 9 - Emulating Mobile Devices.md","permalink":"/courses/playwright-intro-js-tau/chapter-9-emulating-mobile-devices/","tags":["playwright"]}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza MOC\|TAU Course Playwright with JavaScript by Ixchel Meza MOC]]

# Chapter 9 - Emulating Mobile Devices

## Chapter 9 - Emulating Mobile Devices

```js
const { chromium, devices } = require("playwright");
const iPhone = devices["iPhone 11"];
(async () => {
  // mobile code
  const browser = await chromium.launch({ headless: false, slowMo: 100 });
  const context = await browser.newContext({
    ...iPhone,
    permissions: ["geolocation"],
    geolocation: { latitude: 39, longitude: 116 }, // Mexico City coordinates
    locale: "fr-FR",
  });
  const page = await context.newPage();
  await page.goto("https://google.com/maps");
  await page.waitForTimeout(5000);

  await browser.close();
})();

```