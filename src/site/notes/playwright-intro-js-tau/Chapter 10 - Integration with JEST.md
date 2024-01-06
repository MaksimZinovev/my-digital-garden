---
{"dg-publish":true,"dg-path":"courses/playwright-intro-js-tau/Chapter 10 - Integration with JEST.md","permalink":"/courses/playwright-intro-js-tau/chapter-10-integration-with-jest/","tags":["playwright"]}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza MOC\|TAU Course Playwright with JavaScript by Ixchel Meza MOC]]

# Chapter 10 - Integration with JEST

## Chapter 10 - Integration with JEST

Install Jest

```Shell
npm install -D jest
```

Update `package.json` => ` "test": "jest"`

```json
{
  "name": "playwright-demo-wywm",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "jest"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "jest": "^28.1.2",
    "playwright": "^1.22.2"
  }
}
```

Jest tests 

```javascript
const { chromium } = require("playwright");

describe(`UI tests for bookstore using playwright`, () => {
  jest.setTimeout(10000);
  let browser = null;
  let page = null;
  let context = null;
  let firstRowCells = null;

  beforeAll(async () => {
    browser = await chromium.launch({ headless: false, slowMo: 100 });
    context = await browser.newContext();
    page = await context.newPage();
    await page.goto("https://demoqa.com/books");
  });

  afterAll(async () => {
    await browser.close();
  });

  test(`Should load page`, async () => {
    expect(page).not.toBeNull();
    expect(await page.title()).not.toBeNull();
  });

  test(`Should be able to search for eloquent javascript`, async () => {
    await page.fill("#searchBox", "eloquent");
    // an assertion could go here
  });

  test(`Should check if book image is ok`, async () => {
    firstRowCells = await page.$$(
      ".ReactTable  .rt-tr-group:nth-child(1) .rt-td"
    );
    let imageURL = await firstRowCells[0].$("img");
    expect(await imageURL.getAttribute("src")).not.toBeNull();
  });

  test(`Should check if book title is ok`, async () => {
    expect(await firstRowCells[1].innerText()).toBe(
      "Eloquent JavaScript, Second Edition"
    );
  });
  test(`Should check if book author is ok`, async () => {
    expect(await firstRowCells[2].innerText()).toBe(
      "Marijn Haverbeke"
    );
  });
  test(`Should check if book publisher is ok`, async () => {
    expect(await firstRowCells[3].innerText()).toBe(
      "No Starch Press"
    );
  });
});

```