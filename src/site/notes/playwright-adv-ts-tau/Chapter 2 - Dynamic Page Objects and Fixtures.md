---
{"dg-publish":true,"permalink":"/playwright-adv-ts-tau/chapter-2-dynamic-page-objects-and-fixtures/","created":"","updated":""}
---

links:: [[playwright-adv-ts-tau/advanced Playwright MOC\|advanced Playwright MOC]]

# Chapter 2 - Dynamic Page Objects and Fixtures

## Chapter 2 - Dynamic Page Objects and Fixtures

### Dynamic Page Objects

hooks.ts: 

```typescript
import { Page } from '@playwright/test';
import { buildUrl } from './uiUrlBuilder';
import BookPage from '../ui/pages/book-page';
import LoginPage from '../ui/pages/login-page';
import ProfilePage from '../ui/pages/profile-page';

async function beforeEach(
  page: Page,
  PageObjectParam: LoginPage|BookPage|ProfilePage,
  targetPage: string,
  params?: Record<any, any>
) {
  await page.goto(buildUrl(targetPage, params));
  const pageObject = await new PageObjectParam(page);
  return pageObject;
}

export default { beforeEach };

```

uiUrlBuilder.ts: 

```typescript
import uiPages from '../utils/uiPages';

export function buildUrl(page: string, params?: Record<any, any>) {
  const uiPath = uiPages[page];
    
  const qParams = new URLSearchParams(params);
  
  const url = params
  ? `${uiPath.concat('?')}${qParams.toString()}`
  : uiPath;

  /**
    * page  bookStore
    * uiPath  /books
    * params  { book: '9781449337711' }
    * qParams  URLSearchParams { 'book' => '9781449337711' }
    * url  /books?book=9781449337711
  */

  return url;
}

```

profile-with-dynamic-pom.spec.ts:

```javascript
import { test } from '@playwright/test';
import ProfilePage from '../pages/profile-page';
import hooks from '../../utils/hooks';
import pages from '../../utils/pages';

let profilePage: ProfilePage;

test.beforeEach(async ({ page }) => {
    // await page.goto(pages.profile);
    // profilePage = new ProfilePage(page);
    profilePage = await hooks.beforeEach(page, ProfilePage, pages.profile);
});

test.describe('Profile - Dynamic Page Object Model', () => {
    test('Check logged in', async () => {
        await profilePage.checkLoggedIn();
    });
});

```

### Fixtures

```typescript
// boos-store-fixture.ts
import { test as base } from "@playwright/test";
import BookStorePage from "../pages/book-store-page";
import hooks from "../../utils/hooks";
import pages from "../../utils/pages";

type MyFixtures = {
  bookStorePage: BookStorePage;
};

export const test = base.extend<MyFixtures>({
  bookStorePage: async ({ page }, use) => {
    const bookStorePage = await hooks.beforeEach(
      page,
      BookStorePage,
      pages.bookStorePage
    );

    await use(bookStorePage);
  },
});

export { expect } from "@playwright/test";

```


```typescript
//book-store-page.ts
import { type Page, type Locator, expect } from "@playwright/test";

class BookStorePage {
  readonly page: Page;
  readonly searchInput: Locator;
  readonly logoutButton: Locator;
  readonly userNameLabel: Locator;
  readonly resultRows: Locator;
  readonly resultCellsImage: Locator;
  readonly resultCellsTitle: Locator;
  readonly header: Locator;

  constructor(page: Page) {
    this.page = page;
    this.searchInput = page.getByPlaceholder(/type to search/i);
    this.userNameLabel = page.locator("#userName-value");
    this.resultRows = page.getByRole("row");
    this.resultCellsTitle = page.getByRole("row").getByRole("link");
    this.header = page.getByText("Book Store", { exact: true }).first();
  }

  async typeToSearch(searchQuery: string) {
    if (searchQuery) {
      await this.searchInput.fill(searchQuery);
    }
  }

  async checkSearchResultsTitles(expectedTitles: string[]) {
    await expect(this.resultCellsTitle as Locator).toHaveText(expectedTitles);

    console.log(await (this.resultCellsTitle as Locator).all());

    (await (this.resultCellsTitle as Locator).all()).map(
      async (title) => await expect(title).not.toBeVisible()
    );
  }
  async checkHeader() {
    await expect(this.header).toHaveText("Book Store");
    await expect(this.header).toBeVisible();
  }
}

export default BookStorePage;

```


```ts
//book-store.spec.ts
import { test } from "../fixtures/books-store-fixture";

test.describe.configure({ mode: "serial" });

const EXPECTED_SEARCH_RESULTS = {
  java: {
    query: "java",
    expectedTitles: [
      "Learning JavaScript Design Patterns",
      "Speaking JavaScript",
      "Programming JavaScript Applications",
      "Eloquent JavaScript, Second Edition",
    ],
  },
};

test.describe("Book store  - Fixture", () => {
  test("Open book store pages", async ({ bookStorePage }) => {
    await bookStorePage.checkHeader();
  });

  test.only("Search java books in Book store", async ({ bookStorePage }) => {
    await bookStorePage.typeToSearch("java");
    await bookStorePage.checkSearchResultsTitles(
      EXPECTED_SEARCH_RESULTS.java.expectedTitles
    );
  });
});

```