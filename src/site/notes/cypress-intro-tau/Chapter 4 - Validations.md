---
{"dg-publish":true,"permalink":"/cypress-intro-tau/chapter-4-validations/","tags":["cypress"]}
---

## Chapter 4 - Validations

```js
/// <reference types="cypress" />
it("should be able to add a new todo to the list", () => {
  cy.visit("http://todomvc-app-for-testing.surge.sh/");
  cy.get(".new-todo", { timeout: 6000 }).type("Clean room {enter}");
  cy.get("label").should("have.text", "Clean room");
  cy.get(".toggle").should("not.be.checked");
  cy.get(".toggle").click();
  cy.get("label").should("have.css", "text-decoration-line", "line-through");
  cy.contains("Clear completed").click();
  cy.get(".todo-list").should("not.have.descendants", "li");
});

// to run the test: npx cypress open

```