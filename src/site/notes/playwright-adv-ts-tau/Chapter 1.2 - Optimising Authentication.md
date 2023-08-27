---
{"dg-publish":true,"dg-path":"courses/playwright-adv-ts-tau/Chapter 1.2 - Optimising Authentication.md","permalink":"/courses/playwright-adv-ts-tau/chapter-1-2-optimising-authentication/","created":"","updated":""}
---

links:: [[playwright-adv-ts-tau/advanced Playwright MOC\|advanced Playwright MOC]]

# Chapter 1.2 - Optimising Authentication

## Chapter 1.2 - Optimising Authentication

profile-stored-auth-multi-role-user.spec.ts: 

```javascript
import { test } from '@playwright/test';
import ProfilePage from '../pages/profile-page';
import pages from '../../utils/pages';

let profilePage: ProfilePage;

// test.use({ storageState: '.auth/user.json' });

test.beforeEach(async ({ page }) => {
    await page.goto(pages.profile);
});

test.describe('Book Store Application - Profile', () => {
    test.use({ storageState: '.auth/user.json' });
    test('Sort books - user', async ( { page } ) => { 
        profilePage = new ProfilePage(page);
        await profilePage.checkLoggedInUser();
    });
});

```

profile-stored-auth-multi-role-example.spec.ts:

```javascript
import { test } from '@playwright/test';
import ProfilePage from '../pages/profile-page';
import pages from '../../utils/pages';

let profilePage: ProfilePage;

test.beforeEach(async ({ page }) => {
    await page.goto(pages.profile);
});

test.describe('Book Store Application - Profile - Admin', () => {
    test('admin and user', async ({ browser }) => {
        const adminContext = await browser.newContext({ storageState: '.auth/admin.json' });
        const adminPage = await adminContext.newPage();
        profilePage = new ProfilePage(adminPage);
        await profilePage.checkLoggedInAdmin();
        
        const userContext = await browser.newContext({ storageState: '.auth/user.json' });
        const userPage = await userContext.newPage();
        profilePage = new ProfilePage(userPage);
        await profilePage.checkLoggedInUser();
        
        await adminContext.close();
        await userContext.close();
    });
});

```

Global setup should not be used in this case

playwright.config.ts:

```ts
import { defineConfig, devices } from '@playwright/test';
import baseEnvUrl from './tests/utils/environmentBaseUrl';
import path from 'path';

// require('dotenv').config();
export const STORAGE_STATE_APPL = path.join(__dirname, './applitoolsStorageState.json');
export const STORAGE_STATE_API = path.join(__dirname, './apiStorageState.json');
require('dotenv').config();

export default defineConfig({
  reporter: [['html'], ['list']],
  // globalSetup: require.resolve('./tests/setup/global-setup'),
  fullyParallel: false,
  forbidOnly: !!process.env.CI,
  retries: 0,
  workers: undefined,
  // timeout: 5000,
  use: {
    // storageState: 'storageState.json',
    trace: 'on',
    baseURL: process.env.ENV === 'production' 
      ? baseEnvUrl.production.home
      : process.env.ENV === 'staging' 
        ? baseEnvUrl.staging.home
        : baseEnvUrl.local.home
  },
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
    {
      name: 'setup-api-login',
      testMatch: /api-setup\.ts/,
    },
    {
      name: 'chromium-api',
      use: { 
        ...devices['Desktop Chrome'] ,
        storageState: STORAGE_STATE_API,
        headless: false,
      
      },
      dependencies: ['setup-api-login']
    },
  ],
});

```

Use auth-setup.ts to store storageState for each user role:

```typescript
import { test as setup, type Page } from '@playwright/test';
import LoginPage from '../ui/pages/login-page';
import uiPages from '../utils/uiPages';

const adminFile = '.auth/admin.json';

setup('authenticate as admin', async ({ page }) => {
  const user = process.env.USERNAME_ADMIN!;
  const password = process.env.PASSWORD!;
  await doLogin(page, user, password);

  await page.context().storageState({ path: adminFile });
});

const userFile = '.auth/user.json';

setup('authenticate as user', async ({ page }) => {
    const user = process.env.USERNAME_USER!;
    const password = process.env.PASSWORD!;
    await doLogin(page, user, password);
    await page.context().storageState({ path: userFile });
});

async function doLogin(page: Page, user:string, password: string) {
    const baseURL = setup.info().project.use.baseURL!;
    const loginPage = new LoginPage(page);
  
    await page.goto(baseURL!+uiPages.login);
    await loginPage.doLogin(user, password);
    await page.waitForURL(baseURL+uiPages.login);
    await loginPage.checkLoggedIn();
}

```