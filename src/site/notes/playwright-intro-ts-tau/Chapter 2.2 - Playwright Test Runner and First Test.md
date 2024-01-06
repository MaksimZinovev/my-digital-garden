---
{"dg-publish":true,"permalink":"/playwright-intro-ts-tau/chapter-2-2-playwright-test-runner-and-first-test/"}
---

links:: [[playwright-intro-ts-tau/introduction to playwright typescript MOC\|introduction to playwright typescript MOC]]

# Chapter 2.2 - Playwright Test Runner and First Test

## Chapter 2.2 - Playwright Test Runner and First Test

package.json shows dependencies sand version.

package.json can include scripts.

`npx playwright test tests` - run all the folders that start from `test`

Notes: 

- running all tests
	- workers: 1, time: 58
	- workers: 10, time: 20
	- workers: 36, time: 22

Running tests with reporter parameter

  ```Shell
npx playwright test --reporter=list
```

Run single test 

```bash
npm run test:e2e:exp
```

config.ts:

```json
 projects: [
    {
      name: 'experiment',
      use: { 
        ...devices['iPhone 8'],
        // viewport: { width: 1280, height: 720 },
      },
      ]
```

package.json:

```bash
test:e2e:exp": "npx playwright test example.spec.ts --project=experiment --headed -g 'has title' --reporter=line",
```



```json
{
  "name": "tau-introduction-to-playwright",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test:e2e": "npx playwright test tests/",
    "test:e2e:all": "npx playwright test tests --project=all-browsers-and-tests",
    "test:e2e:ci": "CI=1 npx playwright test --project=ci --shard=$CI_NODE_INDEX/$CI_NODE_TOTAL",
    "test:e2e:dev": "npx playwright test tests-examples/ --project=chromium --headed --retries=0 --reporter=line",
    "test:e2e:smoke": "npx playwright test tests-examples/ --grep @smoke --project=chromium",
    "test:e2e:non-smoke": "npx playwright test tests-examples/ --grep-invert @smoke --project=firefox",
    "test:visual:acme": "npx playwright test example-applitools.spec.ts --project=chromium",
    "test:visual:playwright": "npx playwright test example3.spec.ts --project=all-browsers-and-tests"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@applitools/eyes-playwright": "^1.17.0",
    "@playwright/test": "^1.36.0",
    "dotenv": "^16.0.3"
  }
}

```



- Running all tests
    
    ```
    npx playwright test
    ```
    
- Running a single test file
    
    ```
    npx playwright test landing-page.spec.ts
    ```
    
- Run a set of test files
    
    ```
    npx playwright test tests/todo-page/ tests/landing-page/
    ```
    
- Run files that have `landing` or `login` in the file name
    
    ```
    npx playwright test landing login
    ```
    
- Run the test with the title
    
    ```
    npx playwright test -g "add a todo item"
    ```
    
- Running tests in headed mode
    
    ```
    npx playwright test landing-page.spec.ts --headed
    ```
    
- Running tests on a specific project
    
    ```
    npx playwright test landing-page.ts --project=chromium
    ```