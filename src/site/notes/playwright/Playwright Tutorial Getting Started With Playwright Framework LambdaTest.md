---
{"dg-publish":true,"permalink":"/playwright/playwright-tutorial-getting-started-with-playwright-framework-lambda-test/","tags":["playwright"]}
---


Links: [[Playwright MOC\|Playwright MOC]], [Playwright Tutorial: Getting Started With Playwright Framework | LambdaTest](https://www.lambdatest.com/blog/playwright-framework/)

<br ><br >

# Playwright Tutorial Getting Started With Playwright Framework LambdaTest

## 1. Getting Started - Install Playwright in VS Code

1. Open VS Code
2. Install Playwright from marketplace 
3. Run command palette: install playwright
4. Observe result 

```Shell
✔ Success! Created a Playwright Test project at /Users/maksim/repos/playwright-wywm

Inside that directory, you can run several commands:

  npx playwright test
    Runs the end-to-end tests.

  npx playwright test --project=chromium
    Runs the tests only on Desktop Chrome.

  npx playwright test example.spec.ts
    Runs the tests in the specific file.

  npx playwright test --debug
    Runs the tests in debug mode.

We suggest that you begin by typing:

    npx playwright test

And check out the following files:
  - ./example.spec.ts - Example end-to-end test
  - ./playwright.config.ts - Playwright Test configuration

Visit https://playwright.dev/docs/intro for more information. ✨

Happy hacking! 🎭
```

## 2. Run Sample Tests

1. Run sample tests 

```Shell
npx playwright test
```

2. Show report

```Shell
npx playwright show-report
```

## 3. Show Trace

There are a few different ways these reports can be viewed.

- In your web browser through [https://trace.playwright.dev/](https://trace.playwright.dev/), where you can drag and drop the trace files.
- By executing the following command in your CLI:

```bash
npx playwright  show-trace test-results/example-Counter-should-display-the-current-number-of-todo-items-firefox/trace.zip
```

## 4. How to Select N-th Element When Locator Points to a List

[Locators | Playwright](https://playwright.dev/docs/locators#strictness)

Locators are strict. This means that all operations on locators that imply some target DOM element will throw an exception if more than one element matches given selector.

```js
await page.locator("#user-message").first().fill(text);
```

## 5. How to Organise Test Suites in Playwright

links::[Grouping and Organising Test Suite in Playwright | by Ganesh Hegde | Geek Culture | Medium](https://medium.com/geekculture/grouping-and-organising-test-suite-in-playwright-dccf2c55d776)

Run tests in folder

```bash
npx playwright test tests/home/
```

Run tagged tests

```shell
npx playright test --grep @smoke
```



## 6. Generate tests - Codegen command

```shell
npx playwright codegen wikipedia.org
```



## 7. Handle multiple pages (tabs)


```javascript
import { test, expect, chromium } from "@playwright/test";

const baseUrl = "https://potential-qa.withyouwithme.team";
const rallypointUrl = "https://rallypoint.withyouwithme.com/";

test("rallypoint link should redirect to Rallypoint page @smoke", async ({browser}) => {
  const browserInstance = await chromium.launch({ slowMo: 500 });
  const context = await browserInstance.newContext();
  const homePage = await context.newPage();
  await homePage.goto(baseUrl);

  // await homePage.locator("text=Rallypoint").click();

  const [newPage] = await Promise.all([
    context.waitForEvent("page"),
    homePage.click("text=Rallypoint"), // Opens a new tab
  ]);
  await newPage.waitForLoadState();
  console.log(await newPage.title());

  // Should remain on the same page - Home
  await expect(newPage).toHaveURL(rallypointUrl);

  // Check 'Kyewords' input field is present
  await expect(newPage.locator("body h1")).toHaveText("Get a tech job.");
});

```
