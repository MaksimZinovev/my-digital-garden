---
{"dg-publish":true,"permalink":"/cypress-intro-tau/chapter-6-cypress-cli/","tags":["cypress"],"created":"","updated":""}
---

## Chapter 6 - Cypress CLI

Run cypress tests in headless mode 

```Shell
npx cypress run
```

View help

```Shell
npx cypress run --help
```

Run single file 

```bash
npx cypress run --spec cypress/integration/todomvc-actions.spec.js
```

`package.json`

`scripts` key allows to specify to run scripts 

No need to prepend `npm` or `npx` in script commands.

```json
{
  "name": "wywm-cypress",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "cypress": "cypress open",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cypress": "^3.8.3"
  }
}

```

To use the above script in CLI 

```bash
npm run cypress                                                   

> wywm-cypress@1.0.0 cypress
> cypress open

```

Shortcut

```Shell
npm tests
```