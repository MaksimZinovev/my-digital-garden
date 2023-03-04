---
{"dg-publish":true,"permalink":"/cypress/chapter-2-writing-the-first-test-in-cypress/","tags":["cypress"]}
---

## Chapter 2 - Writing the First Test in Cypress

links: [TodoMVC](http://todomvc-app-for-testing.surge.sh/)

This tells VS Code which package to use for autocompletion

```JavaScript
/// <reference types="cypress" />
```

Mocha - built-in test runner for Cypress.

```js
/// <reference types="cypress" />
it("should navigate to TodoMVC App", () => {
  cy.visit("http://todomvc-app-for-testing.surge.sh/fake");
});

// to run the test: npx cypress open
```