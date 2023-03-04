---
{"dg-publish":true,"permalink":"/cypress/chapter-8-visual-validation-in-cypress/","tags":["cypress"]}
---

## Chapter 8 - Visual Validation in Cypress

Steps 

1. Create Applitools account 
2. Find API key in Applitools account
3. Create environment variable holding API key. Eyes plagun will automatically use it.
4. Install plugin `npm install @applitools/eyeys-cypress@3` 
5. Run `npx eyes-setup` to set up eyes plugin.
6. Write test that uses eys plugin for visual testing
7. Run tests 1st time
8. Check results in Aplitools account - `New` status
9. Run tests 2nd time
10. Check results in Aplitools account - Passed status
11. Add browser section in the test

Sample code

```php
/// <reference types="cypress" />
import * as todoPage from '../page-objects/todo-page'

describe('visual validation', () => {
  before(() =>  cy.visit('http://todomvc-app-for-testing.surge.sh/?different-title-color'))

  beforeEach(() =>
    cy.eyesOpen({
      appName: 'TAU TodoMVC',
      batchName: 'TAU TodoMVC',
      browser: [
        {name: 'chrome', width: 1024, height: 768},
        {name: 'chrome', width: 800, height: 600},
        {name: 'firefox', width: 1024, height: 768},
        {deviceName: 'iPhone X'},
      ]
    })
  )

  afterEach(() => cy.eyesClose())

  it('should look good', () => {
    cy.eyesCheckWindow('empty todo list')

    todoPage.addTodo('Clean room')
    todoPage.addTodo('Learn javascript')

    cy.eyesCheckWindow('two todos')

    todoPage.toggleTodo(0)

    cy.eyesCheckWindow('mark as completed')
  })
})
```