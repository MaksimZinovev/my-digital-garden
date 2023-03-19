---
{"dg-publish":true,"permalink":"/cypress/chapter-5-grouping-tests-with-mocha/","tags":["cypress"],"created":"","updated":""}
---

## Chapter 5 - Grouping Tests with Mocha

```js
/// <reference types="cypress" />
// todomvc-actions.spec.js

// to run the test: npx cypress open

describe("todo actions", () => {
  beforeEach(() => {
    cy.visit("http://todomvc-app-for-testing.surge.sh/");
    cy.get(".new-todo", { timeout: 6000 }).type("Clean room {enter}");
  });
  it("should add a new todo list", () => {
    cy.get("label").should("have.text", "Clean room");
    cy.get(".toggle").should("not.be.checked");
  });

  it("should mark a  todo list as completed", () => {
    cy.get(".toggle").click();
    cy.get("label").should("have.css", "text-decoration-line", "line-through");
  });

  it("should clear all completed items in todo list", () => {
    cy.get(".toggle").click();
    cy.contains("Clear completed").click();
    cy.get(".todo-list").should("not.have.descendants", "li");
  });
});

```


```js
/// <reference types="cypress" />
//todomvc-filtering.spec.js

// to run the test: npx cypress open

describe("todo filtering", () => {
  beforeEach(() => {
    cy.visit("http://todomvc-app-for-testing.surge.sh/");
    cy.get(".new-todo").type("Clean room {enter}");
    cy.get(".new-todo").type("Learn JavaScript {enter}");
    cy.get(".new-todo").type("Have rest{enter}");
    cy.get(".todo-list li:nth-child(2) .toggle").click();
  });
  it("should filter active todos", () => {
    cy.contains("Active").click();
    cy.get(".todo-list li").should("have.length", 2);
  });
  it("should filter completed todos", () => {
    cy.contains("Completed").click();
    cy.get(".todo-list li").should("have.length", 1);
  });
  it("should filter All todos", () => {
    cy.contains("All").click();
    cy.get(".todo-list li").should("have.length", 3);
  });
});

```