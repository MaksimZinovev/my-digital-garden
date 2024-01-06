---
{"dg-publish":true,"permalink":"/playwright-intro-ts-tau/chapter-3-2-coding-like-a-pro-in-playwright/"}
---

links:: [[playwright-intro-ts-tau/introduction to playwright typescript MOC\|introduction to playwright typescript MOC]]

# Chapter 3.2 - Coding Like a Pro in Playwright

## Chapter 3.2 - Coding Like a Pro in Playwright

```typescript
import { test, expect,  type Page } from "@playwright/test";
import { HomePage } from "../pages/home-page";


/* 
test 1:
1. open playwright site 
2. Press Cmd + K 
3. Verify heading search dialog opens
*/

/* 
test 2:
1. open playwright site 
2. Press Cmd + K 
3. Press Enter
4. Search gain
5. Verify head search history is displayed
*/
const URL = "https://playwright.dev/";
let homePage: HomePage;
test.beforeAll(async () => {
  console.log("Starting testing");
});

test.beforeEach(async ({ page }, testInfo ) => {
  await page.goto(URL);
  homePage = new HomePage(page);
  console.log(`Test info: ${testInfo.title}`); 
  console.log(`Test info root dir: ${testInfo.config.rootDir}`); 
});

test.afterAll(async () => {
    console.log("Finished testing"); 
});

test("search modal opens via Cmd+K ", async () => {
  // Act
  await homePage.keyboardPress('Control+k');
  await homePage.waitForInputField();

  // Assert
  await homePage.assertDocSearchListVisible();
});
test("recent search is displayed", async ({ page }) => {
 // Act
 await homePage.keyboardPress('Control+k');
 await homePage.waitForInputField();
 await homePage.typeSearchQuery('locator');
 await homePage.waitForSearchDocsList();
 await homePage.searchListPress('Enter');
 await homePage.clickSearch();
 await homePage.waitForSearchDocsList();

 // Assert
 await homePage.assertDocSearchItemVisible();
 await homePage.assertDocSearchItemText('Locators');
});

```


```typescript
import { type Locator, type Page, expect } from '@playwright/test';

type  Key = 'ArrowDown' | 'ArrowUp' | 'Enter' | 'Control+k';

export class HomePage {
    readonly page: Page;
    readonly getStartedButton: Locator;
    readonly pageTitle: RegExp;
    readonly searchField: Locator;
    readonly searchInputField: Locator;
    readonly searchDocsList: Locator;
    readonly docsSearchItem: Locator;

    constructor(page: Page) {
        this.page = page;
        this.getStartedButton = page.getByRole('link', { name: 'Get started' });
        this.pageTitle = /Playwright/;
        this.searchField = page.getByLabel('Search');
        this.searchInputField = page.getByPlaceholder('Search docs');
        this.searchDocsList = page.getByRole('link', { name: 'Locators', exact: true });
        this.docsSearchItem = page.locator('[id*= docsearch-item]')
    }

    async clickGetStarted() {
        await this.getStartedButton.click();
    }

    async clickSearch() {
        await this.searchField.click();
    }
  async typeSearchQuery(query) {
        await this.searchInputField.fill(query);
    }

  async waitForSearchDocsList() {
        await this.searchDocsList.waitFor();
    }
  async waitForInputField() {
        await this.searchInputField.waitFor();
    }

  async searchListPress(key: Key) {
        await this.searchInputField.press(key);
    }

  async keyboardPress(key: Key) {
        await this.page.keyboard.press(key);
    }

    async assertPageTitle() {
        await expect(this.page).toHaveTitle(this.pageTitle);
    }

    async assertPageUrl(pageUrl: RegExp) {
        await expect(this.page).toHaveURL(pageUrl);
    }  
    
    async assertDocSearchListVisible() {
        await expect(this.searchInputField).toBeVisible();
    } 

    async assertDocSearchItemVisible() {
        await expect(this.docsSearchItem).toBeVisible();
    }
    async assertDocSearchItemText(text) {
        await expect(this.docsSearchItem).toHaveText(text);
    }
}

export default HomePage;
```