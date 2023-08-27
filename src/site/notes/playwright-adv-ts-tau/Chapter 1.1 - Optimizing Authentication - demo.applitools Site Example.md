---
{"dg-publish":true,"permalink":"/playwright-adv-ts-tau/chapter-1-1-optimizing-authentication-demo-applitools-site-example/","created":"","updated":""}
---

links:: [[playwright-adv-ts-tau/advanced Playwright MOC\|advanced Playwright MOC]]

# Chapter 1.1 - Optimizing Authentication - demo.applitools Site Example

## Chapter 1.1 - Optimizing Authentication - demo.applitools Site Example

applitools-setup.ts:

```ts
import { test as setup, expect } from "@playwright/test";
import { STORAGE_STATE_APPL } from "../../playwright.config";

setup("do login applitools", async ({ page }) => {
  const user = "user";
  const password = "pass";
  await page.goto("https://demo.applitools.com");
  await page.getByPlaceholder(/enter your username/i).fill(user);
  await page.getByPlaceholder(/enter your password/i).fill(password);
  await page.getByRole("link", {
    name: /sign in/i,
  }).click();

  await expect(page).toHaveURL(/app.html/i);
  await page.context().storageState({ path: STORAGE_STATE_APPL });
});

```

login.appl.spec.ts:

```ts
import { test, expect } from "@playwright/test";

// test.describe.configure({ mode: 'serial' });
const BASE_URL_APPL = "https://demo.applitools.com/";
test.beforeEach(async ({ page }) => {
  await page.goto(BASE_URL_APPL);
});

test.only(`successfull login aplitools`, async ({ page }) => {
  await page.goto(BASE_URL_APPL+'/app.html')
  await expect(page).toHaveURL(/app.html/i);
});

```

playwright.config.ts:

```ts
import { defineConfig, devices } from '@playwright/test';
import baseEnvUrl from './tests/utils/environmentBaseUrl';
import path from 'path';

// require('dotenv').config();
export const STORAGE_STATE_APPL = path.join(__dirname, './applitoolsStorageState.json');
require('dotenv').config();

export default defineConfig({
  reporter: [['html'], ['list']],
  // globalSetup: require.resolve('./tests/setup/global-setup'),
  // fullyParallel: false,
  // forbidOnly: !!process.env.CI,
  // retries: 0,
  // workers: undefined,
  // // timeout: 5000,
  // use: {
  //   storageState: 'storageState.json',
  //   trace: 'on',
  //   baseURL: process.env.ENV === 'production' 
  //     ? baseEnvUrl.production.home
  //     : process.env.ENV === 'staging' 
  //       ? baseEnvUrl.staging.home
  //       : baseEnvUrl.local.home
  // },
  projects: [
    
    { 
      name: 'auth-setup', 
      testMatch: /auth-setup\.ts/ 
    },
    {
      name: 'chromium',
      use: { 
        ...devices['Desktop Chrome'],
        storageState: 'storageState.json',
       },
    },
    {
      name: 'chromium-auth',
      use: { 
        ...devices['Desktop Chrome'] ,
        // storageState: '.auth/admin.json', //use this in case you have multiple projects one per user
      },
      dependencies: ['auth-setup'],
    },
    {
      name: 'setup-applitools',
      testMatch: /applitools-setup\.ts/,
    },
    {
      name: 'chromium-appl',
      use: { 
        ...devices['Desktop Chrome'] ,
        storageState: STORAGE_STATE_APPL,
        headless: false,
      
      },
      dependencies: ['setup-applitools']
    },
  ],
});

```