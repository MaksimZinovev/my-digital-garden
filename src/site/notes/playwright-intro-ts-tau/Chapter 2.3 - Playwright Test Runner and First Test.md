---
{"dg-publish":true,"permalink":"/playwright-intro-ts-tau/chapter-2-3-playwright-test-runner-and-first-test/","created":"","updated":""}
---

links:: [[playwright-intro-ts-tau/introduction to playwright typescript MOC\|introduction to playwright typescript MOC]]

# Chapter 2.3 - Playwright Test Runner and First Test

## Chapter 2.3 - Playwright Test Runner and First Test

```ts
/* 
1. Open playwright page 
2. Click Docs
3. Click Node.js > Java
4. Verify text is visible: Playwright is distributed as a set of Maven modules. The easiest way to use it is to add one dependency to your project's pom.xml as described below. If you're not familiar with Maven please refer to its documentation
*/
import { test, expect } from "@playwright/test";

test.only("Check Java page", async ({ page }) => {
  const javaDescription = `Playwright is distributed as a set of Maven modules. The easiest way to use it is to add one dependency to your project's pom.xml as described below. If you're not familiar with Maven please refer to its documentation.`;
  await page.goto("https://playwright.dev/");
  await page.getByRole("link", { name: "Docs" }).click();
  await page.getByRole("button", { name: "Node.js" }).hover();
  await page
    .getByLabel("Main", { exact: true })
    .getByRole("link", { name: "Java" })
    .click();
  expect(page).toHaveURL("https://playwright.dev/java/docs/intro");
  expect(page.getByText(javaDescription, { exact: true })).toBeVisible;
});

```