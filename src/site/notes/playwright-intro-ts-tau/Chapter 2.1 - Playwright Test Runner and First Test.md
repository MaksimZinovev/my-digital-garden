---
{"dg-publish":true,"permalink":"/playwright-intro-ts-tau/chapter-2-1-playwright-test-runner-and-first-test/","created":"","updated":""}
---

links:: [[playwright-intro-ts-tau/introduction to playwright typescript MOC\|introduction to playwright typescript MOC]]

# Chapter 2.1 - Playwright Test Runner and First Test

## Chapter 2.1 - Playwright Test Runner and First Test

1. When running tests via UI (VSCode): headed mode
1. When running tests via command line: headless mode

Overview of config.ts file.

```js
import { defineConfig, devices } from '@playwright/test';
import baseEnvUrl from './utils/environmentBaseUrl';

/**
 * Read environment variables from file.
 * https://github.com/motdotla/dotenv
 */
require('dotenv').config();

/**
 * See https://playwright.dev/docs/test-configuration.
 */
export default defineConfig({
  testDir: './tests',

  /* Run tests in files in parallel */
  fullyParallel: true,

  /* Fail the build on CI if you accidentally left test.only in the source code. */
  forbidOnly: !!process.env.CI,

  /* Retry on CI only */
  // retries: process.env.CI ? 2 : 0,
  retries: 2,

  /* Opt out of parallel tests on CI. */
  workers: process.env.CI ? 1 : undefined,

  /* Reporter to use. See https://playwright.dev/docs/test-reporters */
  reporter: 'html',
  // reporter: [['html', { open: 'always' }]], //always, never and on-failure (default).
  // reporter: [['html', { outputFolder: 'my-report' }]], // report is written into the playwright-report folder in the current working directory. override it using the PLAYWRIGHT_HTML_REPORT
  // reporter: 'dot',
  // reporter: 'list',
  /**
    reporter: [
      ['list'],
      ['json', {  outputFile: 'test-results.json' }]
    ],
  */
  /**
   * custom reports: https://playwright.dev/docs/test-reporters#custom-reporters 
  */
  
  /* Shared settings for all the projects below. See https://playwright.dev/docs/api/class-testoptions. */
  use: {
    /* Base URL to use in actions like `await page.goto('/')`. */
    // baseURL: 'http://127.0.0.1:3000',

    /* Collect trace when retrying the failed test. See https://playwright.dev/docs/trace-viewer */
    trace: 'on-first-retry',
    screenshot: 'only-on-failure',
    // headless: false,
    // ignoreHTTPSErrors: true,
    // viewport: { width: 1280, height: 720 },
    // video: 'on-first-retry',
  },
    // timeout: 30000, //https://playwright.dev/docs/test-timeouts
    // expect: {
      /**
       * Maximum time expect() should wait for the condition to be met.
       * For example in `await expect(locator).toHaveText();`
       */
      // timeout: 10000,
    // },

  /* Folder for test artifacts such as screenshots, videos, traces, etc. */
  // outputDir: 'test-results/',

  /* Configure projects for major browsers */
  projects: [
    // {
    //   name: 'chromium',
    //   use: { 
    //     ...devices['Desktop Chrome'],
    //     // viewport: { width: 1280, height: 720 },
    //   },
    // },

    // {
    //   name: 'firefox',
    //   use: { ...devices['Desktop Firefox'] },
    // },

    // {
    //   name: 'webkit',
    //   use: { ...devices['Desktop Safari'] },
    // },

    {
      name: 'all-browsers-and-tests',
      use: { 
        baseURL: 'https://playwright.dev/',
         ...devices['Desktop Chrome']
      },
    },

    // {
    //   name: 'all-browsers-and-tests',
    //   use: { 
    //     baseURL: 'https://playwright.dev/',
    //      ...devices['Desktop Safari']
    //   },
    // },

    // {
    //   name: 'all-browsers-and-tests',
    //   use: { 
    //     baseURL: 'https://playwright.dev/',
    //      ...devices['Desktop Firefox']
    //   },
    // },

    // Example only
    {
      name: 'local',
      use: { 
        baseURL: baseEnvUrl.local.home,
      },
    },

    // Example only
    {
      name: 'ci',
      use: { 
         baseURL: process.env.CI
          ? baseEnvUrl.ci.prefix + process.env.GITHUB_REF_NAME + baseEnvUrl.ci.suffix //https://dev-myapp-chapter-2.mydomain.com
          : baseEnvUrl.staging.home,
      },
      /**
       * GitHub variables: https://docs.github.com/en/actions/learn-github-actions/variables
       * GitLab variables: https://docs.gitlab.com/ee/ci/variables/predefined_variables.html#predefined-variables-reference
       */
    },

    /* Test against mobile viewports. */
    // {
    //   name: 'Mobile Chrome',
    //   use: { ...devices['Pixel 5'] },
    // },
    // {
    //   name: 'Mobile Safari',
    //   use: { ...devices['iPhone 12'] },
    // },

    /* Test against branded browsers. */
    // {
    //   name: 'Microsoft Edge',
    //   use: { ...devices['Desktop Edge'], channel: 'msedge' },
    // },
    // {
    //   name: 'Google Chrome',
    //   use: { ..devices['Desktop Chrome'], channel: 'chrome' },
    // },
  ],

  /* Run your local dev server before starting the tests */
  // webServer: {
  //   command: 'npm run start',
  //   url: 'http://127.0.0.1:3000',
  //   reuseExistingServer: !process.env.CI,
  // },
});

```

The `package.json` file in a Node.js project serves a different purpose compared to the `package-lock.json` file. Here's an explanation of each file's role:

1. `package.json`:
The `package.json` file is the manifest file for your Node.js project. It contains metadata about the project, including the project name, version, description, entry point, scripts, dependencies, and other configuration details. It serves as the primary configuration file for your project and provides essential information for package management and project setup. Developers typically edit the `package.json` file directly to add, update, or remove dependencies, configure scripts, define project metadata, and set up various project-related settings.

The `dependencies` section in `package.json` specifies the required packages and their version ranges. When you run `npm install` or `yarn install`, the package manager reads the `package.json` file to determine the dependencies to install based on the specified version ranges.

2. `package-lock.json`:
The `package-lock.json` file, as mentioned earlier, is automatically generated and maintained by npm or Yarn. It provides a detailed and deterministic view of the project's dependency tree, including the exact resolved versions of all installed packages and their transitive dependencies. It acts as a lock file, ensuring that the same versions of packages are installed consistently across different environments and installations.

The `package-lock.json` file is primarily used by the package manager (npm or Yarn) and should not be manually edited. It is generated and updated automatically whenever there are changes to the dependency tree, such as installing new packages or updating existing ones.

In summary, the `package.json` file contains project metadata, configuration, and high-level dependency information, while the `package-lock.json` file provides a detailed and locked-down view of the project's dependencies with their resolved versions. Both files play crucial roles in managing dependencies and ensuring consistent and reproducible installations of your project.