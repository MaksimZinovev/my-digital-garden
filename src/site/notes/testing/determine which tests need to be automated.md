---
{"dg-publish":true,"permalink":"/testing/determine-which-tests-need-to-be-automated/","tags":["testing"]}
---

Links: [[canva software tester interview 2\|canva software tester interview 2]]
<br ><br >

# Determine Which Tests Need To Be Automated



1. Factor: Test Frequency and Repetitiveness
	- Testing Level: All levels (unit, integration, system, acceptance, end-to-end, application production monitoring)
	- Description: Automated tests are most valuable when they need to be executed frequently and consistently. Tests that are run repeatedly and require little to no modification over time are ideal candidates for automation. Frequent execution ensures timely feedback, and repetitive tests help catch regressions early in the development process.
	- Best Practices: Identify tests that are executed frequently during development and release cycles. Prioritize automating tests for critical and frequently changed features or modules. Consider automating smoke test and sanity checks for quick feedback on basic functionality.
2. Factor: Test Data Dependency and Isolation
	- Testing Level: Unit and integration tests
	- Description: Automated tests should be self-contained and not rely heavily on external dependencies, especially in the case of unit and integration testing. Tests with minimal data dependencies and isolation ensure stability and reduce the likelihood of false positives or negatives.
	- Best Practices: Use mock objects or test doubles to simulate external dependencies in unit tests. For integration tests, set up a dedicated test environment with pre-defined and isolated test data. Avoid using production data in automated tests to prevent unintended side effects.
3. Factor: Test Execution Time
	- Testing Level: All levels (unit, integration, system, acceptance, end-to-end, application production monitoring)
	- Description: Automated tests should be efficient and complete their execution within a reasonable timeframe. Long-running tests can slow down the development process and delay feedback, making them less suitable for automation.
	- Best Practices: Aim for faster execution times in automated tests. Parallelize test execution when possible, especially for end-to-end and acceptance tests that involve multiple interactions with the application. Regularly monitor and optimize test execution time to maintain the effectiveness of the automated test suite.
4. Factor: Complexity and Stability of Test Cases
	- Testing Level: All levels (unit, integration, system, acceptance, end-to-end, application production monitoring)
	- Description: Complex test cases, especially those that require significant maintenance due to frequent application changes, may be challenging to automate. Conversely, stable and straightforward test cases are better candidates for automation.
	- Best Practices: Start with automating simpler and more stable test cases, which are less prone to changes. Invest in refactoring complex test cases to make them more maintainable before automating. Create a balance between automating existing test cases and designing new ones to achieve optimal test coverage.
5. Factor: Impact and Criticality of Features
	- Testing Level: All levels (unit, integration, system, acceptance, end-to-end, application production monitoring)
	- Description: Automated tests should focus on features that have a significant impact on the user experience and the overall functionality of the application. High-priority and critical features should be thoroughly tested through automation.
	- Best Practices: Collaborate with product managers and stakeholders to identify critical features that require automated testing. Create a risk-based testing strategy to prioritize automated test coverage for critical and high-impact areas.
6. Factor: Integration with Continuous Integration (CI) Pipeline
	- Testing Level: All levels (unit, integration, system, acceptance, end-to-end, application production monitoring)
	- Description: For efficient and timely feedback, automated tests should seamlessly integrate with the CI pipeline. The tests should be triggered automatically on each code commit or as part of the regular build process.
	- Best Practices: Choose testing frameworks and tools that support easy integration with your CI/CD system. Configure the CI pipeline to execute automated tests at appropriate stages, such as after each code merge or before deployment to production.
7. Factor: Cost and Return on Investment (ROI)
	- Testing Level: All levels (unit, integration, system, acceptance, end-to-end, application production monitoring)
	- Description: Automating tests incurs costs in terms of development, maintenance, and infrastructure. Evaluate the potential benefits and ROI of automation for each test to ensure that the effort invested is justified.
	- Best Practices: Conduct a cost-benefit analysis for test automation, considering factors like test stability, execution time, and the likelihood of catching critical defects. Prioritize automation for high-ROI tests that provide significant value in terms of identifying defects early, reducing manual testing efforts, and improving software quality.
8. Factor: User Interface (UI) Changes and Compatibility
	- Testing Level: End-to-end and acceptance tests
	- Description: User interface changes, especially in a rich and complex UI application, can impact the functionality and user experience. Automated tests should consider the compatibility of the application across different devices and browsers.
	- Best Practices: Utilize robust and maintainable UI testing frameworks that can adapt to UI changes. Implement responsive design testing to ensure compatibility across various devices and screen sizes. Perform cross-browser testing to validate the application's behavior on different browsers commonly used by the target audience.