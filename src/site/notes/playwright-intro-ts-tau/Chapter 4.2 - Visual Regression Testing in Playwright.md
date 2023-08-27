---
{"dg-publish":true,"permalink":"/playwright-intro-ts-tau/chapter-4-2-visual-regression-testing-in-playwright/","created":"","updated":""}
---

links:: [[playwright-intro-ts-tau/introduction to playwright typescript MOC\|introduction to playwright typescript MOC]]

# Chapter 4.2 - Visual Regression Testing in Playwright

## Chapter 4.2 - Visual Regression Testing in Playwright

```typescript
import { test, expect, type Page } from "@playwright/test";
import { HomePage } from "../pages/home-page";

/* 
test 1:
1. open playwright site homepage
2.Verify the page has not changed visually
*/

const URL = "https://playwright.dev/";
let homePage: HomePage;
test.beforeAll(async () => {
  console.log("Starting testing");
});

test.beforeEach(async ({ page }, testInfo) => {
  await page.goto(URL);
  homePage = new HomePage(page);
});

test.afterAll(async () => {
  console.log("Finished testing");
});

test("playwright homepage visual test", async () => {
  // Assert
  const starsLocator = homePage.page.getByLabel('stargazers on GitHub') 
  // Compare the full page screenshot with the baseline. Mask the stars number on the screenshot.
  await expect(homePage.page).toHaveScreenshot({ fullPage: true, mask: [starsLocator] });
});

```

If you are not on the same operating system as your CI system, you can use Docker to generate/update the screenshots:

```
docker run --rm --network host -v $(pwd):/work/ -w /work/ -it mcr.microsoft.com/playwright:v1.36.0-jammy /bin/bashnpm installnpx playwright test --update-snapshots
```

It was observed that `--update-snapshots` command does not always work. In this case, can remove existing screenshot and run test again.

![playwright-homepage-visual-test-1-chrome-desktop-94be78-darwin.jpg](/img/user/playwright-intro-js-tau/attachments/playwright-homepage-visual-test-1-chrome-desktop-94be78-darwin.jpg)