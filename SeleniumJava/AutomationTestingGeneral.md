# Automation testing general information

## What is automation testing?

Automation testing is the process of using specialized software tools to execute tests automatically, manage test data, and utilize results to improve software quality. This approach helps in executing repetitive and regression tests efficiently, reducing manual effort, and ensuring higher accuracy and coverage.

### What is re-testing and regretion testing?

**Re-testing** and **regression testing** are two distinct but related concepts in software testing:

### Re-testing
**`Re-testing`** involves testing specific defects that were identified and fixed in the software. The primary goal is to ensure that the previously reported bugs have been successfully resolved. Re-testing is focused on the specific areas of the application where changes were made.

- **`Purpose`**: To verify that specific defects have been fixed.
- **`Scope`**: Narrow, focusing only on the specific defects and their associated functionality.
- **`Execution`**: Performed on the same version of the software where the defects were identified.

### Regression Testing
**`Regression testing`** involves testing the entire application or specific areas of the application to ensure that new code changes have not adversely affected existing functionality. The primary goal is to detect any unintended side effects of the recent changes, enhancements, or bug fixes.

- **`Purpose`**: To verify that new changes have not introduced new bugs or affected existing functionality.
- **`Scope`**: Broad, covering both the new changes and existing functionality.
- **`Execution`**: Typically performed on a new version of the software after changes have been made.

## How automation tools work?

Automation testing tools work by executing predefined scripts that simulate user interactions and test various aspects of the software. Here’s a simplified overview of how they work:

1. **Script Creation**: Test scripts are written using a programming or scripting language supported by the tool (e.g., Java, Python, JavaScript). These scripts define the steps to be performed, including input actions and expected outcomes.

2. **Test Environment Setup**: The testing environment is configured, including the necessary hardware, software, network settings, and data required for the tests.

3. **Test Execution**: The automation tool runs the test scripts automatically. It interacts with the application just like a human tester would, entering data, clicking buttons, and navigating through the software.

4. **Result Recording**: During execution, the tool records the outcomes of each test step, capturing screenshots, logs, and other relevant data for analysis.

5. **Comparison with Expected Results**: The actual results are compared with the expected results predefined in the scripts. Any discrepancies are logged as defects or errors.

6. **Reporting**: The tool generates detailed reports summarizing the test execution, including passed and failed tests, error logs, and other diagnostic information.

7. **Maintenance**: As the application evolves, test scripts may need to be updated to reflect changes in the user interface or functionality. Maintenance ensures that the automation tests remain effective and up-to-date.

Popular automation tools like Selenium, JUnit, TestNG, and others provide various features to support these activities, such as script recording, playback, and integration with other development and testing tools.

## Why programming is required in automation?

Programming is required for automation testing because it allows for the development of test scripts, handling of complex scenarios, customization and flexibility in test execution, integration with CI/CD pipelines, efficient data manipulation, robust error handling, detailed reporting, and tool customization. This ensures that automated tests are effective, efficient, and capable of meeting diverse and complex testing needs.

