---
{"dg-publish":true,"permalink":"/cypress-intro-tau/chapter-7-page-objects-in-cypress/","tags":["cypress"]}
---

## Chapter 7 - Page Objects in Cypress

No need to use `class` if class has no variables. In this case we can just use functions:

```javascript
/// <reference types="cypress" />

export function navigate() {
  cy.visit("http://todomvc-app-for-testing.surge.sh/");
}

export function addTodo(todoText) {
  cy.get(".new-todo").type(todoText + "{enter}");
}

export function toggleTodo(todoIndex) {
  cy.get(`.todo-list li:nth-child(${todoIndex + 1}) .toggle`).click();
}

export function showOnlyCompletedTodos() {
  cy.contains("Completed").click();
}

export function showOnlyActiveTodos() {
  cy.contains("Active").click();
}

export function showAllTodos() {
  cy.contains("All").click();
}

export function clearCompleted() {
  cy.contains("Clear completed").click();
}

export function validateNumberOfTodosShown(expectedNumberOfTodos) {
  cy.get(".todo-list li").should("have.length", expectedNumberOfTodos);
}

export function validateTodoCompletedState(todoIndex, shouldBeCompleted) {
  const l = cy.get(`.todo-list li:nth-child(${todoIndex + 1}) label`);
Ï  l.should(
    `${shouldBeCompleted ? "" : "not."}have.css`,
    "text-decoration-line",
    "line-through"
  );
}

export function validateTodoText(todoIndex, expectedText) {
  cy.get(`.todo-list li:nth-child(${todoIndex + 1}) label`).should(
    "have.text",
    expectedText
  );
}

export function validateToggleState(todoIndex, shouldBeToggled) {
  const label = cy.get(`.todo-list li:nth-child(${todoIndex + 1}) label`);
  label.should(`${shouldBeToggled ? "" : "not."}be.checked`);
}

```

Then use functions like this to make tests more readable and concise: 

```javascript
/// <reference types="cypress" />
import {
  navigate,
  addTodo,
  validateTodoText,
  toggleTodo,
  clearCompleted,
  validateTodoCompletedState,
  validateToggleState,
  validateNumberOfTodosShown,
} from "../pom/todo-page";

describe("todo actions", () => {
  beforeEach(() => {
    navigate();
    addTodo("Clean room");
  });

  it("should add a new todo to the list", () => {
    validateTodoText(0, "Clean room");
    validateToggleState(0, false);
  });

  describe("toggling todos", () => {
    it("should toggle test correctly", () => {
      toggleTodo(0);
      validateTodoCompletedState(0, true);
    });

    it("should clear completed", () => {
      toggleTodo(0);
      clearCompleted();
      validateNumberOfTodosShown(0);
    });
  });
});

```