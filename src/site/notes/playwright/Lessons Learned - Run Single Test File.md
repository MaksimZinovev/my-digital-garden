---
{"dg-publish":true,"permalink":"/playwright/lessons-learned-run-single-test-file/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Lessons Learned - Run Single Test File

## Lessons Learned - Run Single Test File

Run single file with test `bookstore.test.js`. This works, but note, that `expect` cannot be used because it requires `test` module.

```javascript
const { chromium } = require("playwright");

describe(`UI tests for bookstore using playwright`, () => {
  jest.setTimeout(10000);
  let browser = null;
  ...
```


```bash
npm test -- bookstore
```

Run all test in `test` folder

```bash
npm test 
```

This does not work for script `third.js`, because file name does not include `test` suffix:

```bash
▶ npm test -- third

> playwright-demo-wywm@1.0.0 test
> jest "third"

No tests found, exiting with code 1
```

This does not work.

Install `playwright/test`

```shell
npm i -D @playwright/test
```


```javascript
const { test, expect } = require('@playwright/test');


describe(`UI tests for bookstore using playwright`, () => {
  jest.setTimeout(10000);
  let browser = null;
  let page = null;
```


```bash
pm test -- bookstore3   

> playwright-demo-wywm@1.0.0 test
> jest "bookstore3"

 FAIL  tests/bookstore3.spec.js
  ● Test suite failed to run

    Playwright Test needs to be invoked via 'npx playwright test' and excluded from Jest test runs.
    Creating one directory for Playwright tests and one for Jest is the recommended way of doing it.
    See https://playwright.dev/docs/intro for more information about Playwright Test.
```

Instead, use this to run test

```bash
npx playwright test tests/bookstore.test.js
```