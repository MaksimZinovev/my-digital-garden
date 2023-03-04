---
{"dg-publish":true,"permalink":"/cypress/chapter-3-accessing-elements-and-interacting-with-them-in-cypress/","tags":["cypress"]}
---

## Chapter 3 - Accessing Elements and Interacting with Them in Cypress

```js
/// <reference types="cypress" />
it("should be able to add a new todo to the list", () => {
  cy.visit("http://todomvc-app-for-testing.surge.sh/");
  cy.get(".new-todo", { timeout: 6000 }).type("Clean room {enter}");
  cy.get(".toggle").click();
  cy.contains("Clear completed").click();
});

// to run the test: npx cypress open

```