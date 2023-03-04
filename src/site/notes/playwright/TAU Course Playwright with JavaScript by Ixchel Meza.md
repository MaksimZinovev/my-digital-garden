---
{"dg-publish":true,"permalink":"/playwright/tau-course-playwright-with-java-script-by-ixchel-meza/","tags":["playwright"]}
---


Links: 

- [[playwright/Playwright MOC\|Playwright MOC]]
- [Playwright with JavaScript](https://testautomationu.applitools.com/js-playwright-tutorial/) , [TAU Course - Introduction to JavaScript](https://testautomationu.applitools.com/javascript-tutorial/)
- [Your 80 Questions about Playwright, Answered](https://applitools.com/blog/top-playwright-questions-answered/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Node JS](https://nodejs.org/)
- [Playwright Tutorial: Getting Started With Playwright Framework | LambdaTest](https://www.lambdatest.com/blog/playwright-framework/)
- [Your 80 Questions about Playwright, Answered - Automated Visual Testing | Applitools](https://applitools.com/blog/top-playwright-questions-answered/)

<br ><br >

# TAU Course Playwright With JavaScript

**The topics we will be covering are:**

* What is Playwright?

* Installation and Setup

* Interacting with elements

* Element state

* Managing a virtual keyboard

* Interacting with mouse events

* Taking screenshots

* Recording videos

* Visual testing

* Playwright Command Line Interface (CLI)

* Page Object Model (POM) with Playwright

# Notes

1. Typical mistakes in code
	
	- missing await

## Chapter 1.1 - About Playwright

- Node.js library 
- created by Microsoft
- automate Chromium, Firefox, WebKit and single API
- open source 
- free
- supports headless and headful modes 
- device emulation for mobile devices
- locally and in CI cloud

Fast reliable execution

- auto-wait API
- timeout-free
- resilient element selectors

Limitations 

- no legacy MS Edge or IE11 support 
- desktop browsers are used to emulate mobile devices 

## Chapter 1.2 - Installing Playwright

```bash
npm --version
```

```
node -v
```

Open VSCode

run terminal

Skip questions and init package

```
npm init -y
```

Install playwright

```
npm i -D playwright 
```

## Chapter 2 - Writing Your First Playwright Script

```js
const { chromium } = require('playwright');
(async() => {
// function code
const browser = await chromium.launch({headless: false, sloMo: 100});
const page = await browser.newPage();
await page.goto('http://google.com');
await browser.close();
})();


```

```shell
node first.js
```

## Chapter 3.1 - Typing in Text Fields in Playwright

```js
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, sloMo: 100 });
  const page = await browser.newPage();
  await page.goto("https://the-internet.herokuapp.com/forgot_password");
  // code to type in email textbox
  // const email = page.locator('#email');
  const email = page.$("#email"); 
  await email.type("maxfaber82@gmail.com", { delay: 50 });
  // await page.type('#email', 'masfsdf@dfgfd.com', {delay: 50});
  await browser.close();
})();

```

## Chapter 3.2 - Click in Playwright

- [First Music Lesson - Frequency, Octave, Semitone, Sound Names, Major Scale](https://www.apronus.com/music/lessons/unit01.htm)

```js
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 2000 });
  const page = await browser.newPage();
  // await page.goto("https://www.apronus.com/music/lessons/unit01.htm");
  await page.goto("https://www.apronus.com/music/lessons/unit01.htm");
  // code to type click 
  // page.pause() will open Playwright Inspector
  // await page.pause();
  await page.click('#t1 > table > tr:nth-child(1) > td:nth-child(1) > button');
  await browser.close();
})();await browser.close();
})();

```

## Chapter 3.2.1 - Debugging Selectors

```Shell
npx playwright-cli open https://www.wikipedia.org/ 
Need to install the following packages:
  playwright-cli
Ok to proceed? (y) y
playwright-cli has moved to playwright. Use npx playwright instead.
```

```Shell
npx playwright open https://www.wikipedia.org/ 
```

In console type 

```JavaScript
playwright.$('#js-link-box-en > strong')
```

`playwright.$$(selector)` - Same as `playwright.$`, but returns all matching elements

`playwright.inspect('#js-link-box-en > strong` Reveal element in the Elements panel (if DevTools of the respective browser supports it).

## Chapter 3.2.2 - Recording Scripts

At any moment, clicking Record action in [Playwright Inspector](https://playwright.dev/docs/inspector) enables [codegen mode](https://playwright.dev/docs/codegen). Every action on the target page is turned into the generated script:

<br >

## Chapter 3.3 - Dropdowns in Playwright

```JavaScript
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 400 });
  const page = await browser.newPage();
  await page.goto("https://the-internet.herokuapp.com/dropdown");
  const dropdown = await page.$("#dropdown");
  //value
  await dropdown.selectOption({ value: "1" });
  // label
  await dropdown.selectOption({ label: "Option 2" });
  // index
  await dropdown.selectOption({ index: 1 });
  // print text in options elements
  const availableOptions = await dropdown.$$("option");
  for (let i = 0; i < availableOptions.length; i++) {
    console.log(await availableOptions[i].innerText());
  }
  await browser.close();
})();
```

## Chapter 3.4 - Checkboxes and Radiobuttons Dropdowns in Playwright

```JavaScript
const { firefox } = require("playwright");
(async () => {
  // function code
  const browser = await firefox.launch({ headless: false, slowMo: 600 });
  const page = await browser.newPage();
  await page.goto(
    "https://www.w3schools.com/howto/howto_css_custom_checkbox.asp"
  );
  // check the second checkbox
  checks = await page.$$(
    '#main > div.w3-row > div:nth-child(1) > input[type="checkbox"]'
  );
  await checks[1].check();
  await checks[0].uncheck();

  // select the 2nd radio button
  radios = await page.$$(
    '#main > div.w3-row > div:nth-child(1) > input[type="radio"]'
  );
  await radios[1].check();

  await page.pause();
  await browser.close();
})();

```

## Chapter 3.5 - iFrames in Playwright

```JavaScript
const { webkit } = require("playwright");
(async () => {
  // function code
  const browser = await webkit.launch({ headless: false, slowMo: 200 });
  const page = await browser.newPage();
  await page.goto("https://demoqa.com/frames");
  // logic to handle iframe
  const frame1 = await page.frame({ url: /\/sample/ });
  const heading1 = await frame1.$("h1");
  console.log(await heading1.innerText());
  await browser.close();
})();
sole.log(await heading1.innerText());
await browser.close();
})();

```

## Chapter 3.5 - Alerts in Playwright

```JavaScript
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 500 });
  const page = await browser.newPage();
  await page.goto("https://demoqa.com/alerts");
  // code to handle alerts
  // click 3rd button
  page.once("dialog", async (dialog) => {
    console.log(dialog.message());
    await dialog.accept();
  });
  await page.click("#confirmButton");
  // click 4th button
  page.once("dialog", async (dialog) => {
    console.log(dialog.message());
    await dialog.accept("my text is this");
  });
  await page.click("#promtButton");
  await browser.close();
})();

```

## Chapter 4 - Element State

Automatically checked by Playwright. Is Element:

- attached
- visible
- stable
- not being obscured by other elements 
- enabled
- editable

```JavaScript
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ slowMo: 100 });
  const page = await browser.newPage();
  await page.goto("https://demoqa.com/automation-practice-form");

  // print the element state

  const firstName = await page.$("#firstName");
  const sportsCheck = await page.$("#hobbies-checkbox-1");
  const submitBtn = await page.$("#submit");

  console.log(await firstName.isDisabled());
  console.log(await firstName.isEnabled());
  console.log(await firstName.isEditable());

  console.log(await sportsCheck.isChecked());
  console.log(await sportsCheck.isVisible());

  console.log(await submitBtn.isHidden());
  console.log(await submitBtn.isVisible());

  // closing gbrowser
  await browser.close();
})();

```

## Chapter 5 - Managing a Virtual Keyboard

```js
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 100 });
  const page = await browser.newPage();
  await page.goto("https://the-internet.herokuapp.com/key_presses");

  // handling keyboard

  await page.click("input");
  await page.keyboard.type("one does not simply exit vim");
  await page.keyboard.down("Shift");

  for (let i = 0; i < " exit vim".length; i++) {
    await page.keyboard.press("ArrowLeft");
  }
  await page.keyboard.up("Shift");
  await page.keyboard.press("Backspace");
  await page.keyboard.type(" walk into Mordor");

  await browser.close();
})();

```

## Chapter 6 - Mouse Events

```js
const { chromium } = require('playwright');
(async() => {
// function code
const browser = await chromium.launch({headless: false, slowMo: 300});
const page = await browser.newPage();
await page.goto('https://paint.js.org/');

// interacting with mouse
await page.mouse.move(200,200); 
await page.mouse.down();
await page.mouse.move(400,200);
await page.mouse.move(400,400);
await page.mouse.move(200,400);
await page.mouse.move(200,200);
await page.mouse.up();

await browser.close();
})();
```

## Chapter 7 - Taking a Screenshot

```javascript
const { chromium } = require("playwright");
(async () => {
  // function code
  const browser = await chromium.launch({ headless: false, slowMo: 300 });
  const page = await browser.newPage();
  await page.goto("https://applitools.com/");

  // take screenshot code

  // await page.screenshot({ path: "screenshot.png" });

  // take screenshot of the element
  const logo = await page.$(".logo");
 // await logo.screenshot({ path: "logo.png" });

  // take screenshot of the full page

  await page.screenshot({ path: "fullpage.png", fullPage: true });

  await browser.close();
})();
```

## Chapter 8 - Recording Videos

```javascript
const { chromium } = require('playwright');
(async() => {
// function code
const browser = await chromium.launch({headless: false, slowMo: 100});

// creating a page inside  browser
const context = await browser.newContext({
    recordVideo: {
        dir: "./recordings"
    }
});
const page = await context.newPage();


await page.goto('https://the-internet.herokuapp.com/dynamic_loading/1');

// click on button 
await page.click('button'); 
await page.waitForSelector('#loading');
await page.waitForSelector('#loading', {state: 'hidden'});
await page.waitForTimeout(100);

await browser.close();
})();
```

## Chapter 9 - Emulating Mobile Devices

```js
const { chromium, devices } = require("playwright");
const iPhone = devices["iPhone 11"];
(async () => {
  // mobile code
  const browser = await chromium.launch({ headless: false, slowMo: 100 });
  const context = await browser.newContext({
    ...iPhone,
    permissions: ["geolocation"],
    geolocation: { latitude: 39, longitude: 116 }, // Mexico City coordinates
    locale: "fr-FR",
  });
  const page = await context.newPage();
  await page.goto("https://google.com/maps");
  await page.waitForTimeout(5000);

  await browser.close();
})();

```

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

## Chapter 11 - Visual Testing with Playwright

- Requires Applitools account
- Tests take longer time

## Chapter 12 - Record and Playback with Playwright CLI

Launches Playwright inspector

```Shell
npx playwright codegen www.saucedemo
```

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

## Lessons Learned - Most Common Mistakes When Script Does Not Work

- missing `await` in statement
- `conts` or `let` - make sure you use the correct one 
- missing `async` or it should not be used here
- other typos

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


