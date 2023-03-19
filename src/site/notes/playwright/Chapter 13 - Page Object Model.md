---
{"dg-publish":true,"permalink":"/playwright/chapter-13-page-object-model/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Chapter 13 - Page Object Model

## Chapter 13 - Page Object Model
Run tests

```bash
npm test pom/specs/demo.test.js   
```


Pages

```javascript

// pom>models>BasePage.js

class BasePage {
  constructor(page) {
    this.page = page;
  }
  async navigate(path) {
    await this.page.goto(`https://demo.applitools.com/${path}`);
  }
}
module.exports = BasePage;

```


```javascript
// pom>models>HomePage.js

const BasePage = require("./Base.page");
class HomePage extends BasePage {
  constructor(page) {
    super(page);

    //locators

    this.loggedUser = ".logged-user-name";
    this.balances = ".balance-value";
  }
  async getUserName() {
    let user = await this.page.$(this.loggedUser);
    return await user.innerText();
  }

  async getBalance(balType) {
    let balArray = await this.page.$$(this.balances);
    if (balType == "total") {
      return (await balArray[0].$("span")).innerText();
    } else if (balType == "credit") {
      return (await balArray[1]).innerText();
    } else {
      return (await balArray[2]).innerText();
    }
  }
}
module.exports = HomePage;

```


```javascript

// pom>models>LoginPage.js

const BasePage = require("./Base.page");
class LoginPage extends BasePage {
  constructor(page) {
    super(page);

    // locators
    this.userNameTxt = "#username";
    this.passwordTxt = "#password";
    this.loginBtn = "#log-in";
  }
  async navigate() {
    await super.navigate("index.html");
  }

  async login(username, password) {
    await this.page.fill(this.userNameTxt, username);
    await this.page.fill(this.passwordTxt, password);
    await this.page.click(this.loginBtn);
  }
}
module.exports = LoginPage;
```

Tests

```javascript

// pom>specs>demo.tests.js

const { chromium } = require("playwright");
const HomePage = require("../models/Home.page");
const LoginPage = require("../models/Login.page");

describe("Aplitools demo page", () => {
  jest.setTimeout(30000);
  let browser = null;
  let context = null;
  let page = null;

  beforeAll(async () => {
    browser = await chromium.launch({ headless: false });
    context = await browser.newContext();
    page = await context.newPage();
    homePage = new HomePage(page);
    loginPage = new LoginPage(page);
    await loginPage.navigate();
  });

  afterAll(async () => {
    await context.close();
    await browser.close();
  });

  it("Should be able to login", async () => {
    await loginPage.login("username", "password");
    expect(await page.title()).not.toBeNull();
  });
  it("Should be logged in as Jack Gomez", async () => {
    expect(await homePage.getUserName()).toBe("Jack Gomez");
  });
  it("Should have total balance of $350", async () => {
    expect(await homePage.getBalance("total")).toBe("$350");
  });
  it("Should have credit available of $17800", async () => {
    expect(await homePage.getBalance("credit")).toBe("$17,800");
  });
  it("Should have due today of $180", async () => {
    expect(await homePage.getBalance("due")).toBe("$180");
  });
});

```