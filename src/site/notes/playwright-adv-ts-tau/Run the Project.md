---
{"dg-publish":true,"dg-path":"courses/playwright-adv-ts-tau/Run the Project.md","permalink":"/courses/playwright-adv-ts-tau/run-the-project/"}
---

links:: [[playwright-adv-ts-tau/advanced Playwright MOC\|advanced Playwright MOC]]

# Run the Project

## Run the Project

Take a look at the package.json - scripts for more details. The tests are using https://demoqa.com/

```shell
npm run test-ui-c runs all tests on chromium (except the auth)
npm run test-ui-auth-admin runs profile-stored-auth-multi-role-admin.spec.ts
npm run test-ui-auth-user runs profile-stored-auth-multi-role-user.spec.ts
npm run test-ui-auth runs profile-stored-auth-multi-role-example.spec.ts (test will fail due to application limitations)
npm run test-vrt runs visual-regression.spec.ts - visual regression testing with applitools

```