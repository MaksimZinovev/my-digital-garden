---
{"dg-publish":true,"permalink":"/playwright-intro-js-tau/chapter-3-2-1-debugging-selectors/","tags":["playwright"],"created":"","updated":""}
---

links:: [[playwright-intro-js-tau/TAU Course Playwright with JavaScript by Ixchel Meza\|TAU Course Playwright with JavaScript by Ixchel Meza]]

# Chapter 3.2.1 - Debugging Selectors

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