---
{"dg-publish":true,"permalink":"/playwright/chapter-9-emulating-mobile-devices/","tags":["playwright"]}
---

links:: [[TAU Course Playwright with JavaScript by Ixchel Meza 1\|TAU Course Playwright with JavaScript by Ixchel Meza 1]]

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