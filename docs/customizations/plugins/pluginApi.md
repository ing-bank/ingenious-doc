# Plugin API Reference

This page documents the available methods for each INGenious plugin API.

---
## Test Domain APIs

#### CommandPluginApi Methods (General Purpose)
!!!note "All methods listed in this section are also available to the other test domain APIs (Browser, Database, Mobile, Webservice)."

| Method              | Description                                  |
|---------------------|----------------------------------------------|
| getData()           | Returns the test data input for the current action. |
| getAction()         | Returns the current action name.              |
| getInput()          | Returns the input parameter for the action.   |
| getCondition()      | Returns the condition parameter for the action. |
| getReport()         | Returns the TestCaseReportApi for logging test results. |
| getObjectName()     | Returns the current object name.              |
| addVar(name, value) | Stores a value in a runtime variable.         |
| getVar(name)        | Retrieves the value of a runtime variable.    |
| getUserData()       | Returns the UserDataAccessApi for data sheet operations. |
| getExecutionContext() | Returns the ExecutionContextApi for accessing the current run, project, and settings. |

---

#### BrowserPluginApi Methods

| Method              | Description                                  |
|---------------------|----------------------------------------------|
| getPage()           | Returns the Playwright Page object for browser automation. |
| getLocator()        | Returns the Playwright Locator object for element selection. |


---

#### DatabasePluginApi Methods

| Method              | Description                                  |
|---------------------|----------------------------------------------|
| executeDML()        | Executes a DML (INSERT/UPDATE/DELETE) query. |
| executeSelect()     | Executes a SELECT query.                     |
| getResult()         | Returns the ResultSet from the last SELECT query. |


---

#### MobilePluginApi Methods

| Method              | Description                                  |
|---------------------|----------------------------------------------|
| getElement()        | Returns the WebElement for the current action. |
| getMDriver()        | Returns the WebDriver for mobile automation.  |
| getMObject()        | Returns the MobileObjectApi for mobile-specific operations. |
| elementEnabled()    | Checks if the current element is enabled.     |
| checkIfDriverIsAlive() | Checks if the mobile driver is alive.      |

---

#### WebservicePluginApi Methods

| Method              | Description                                  |
|---------------------|----------------------------------------------|
| createHttpRequest(method) | Creates and sends an HTTP request (GET, POST, PUT, etc.). |
| ResponseCode()      | Returns the HTTP response code from the last request. |
| ResponseBody()      | Returns the HTTP response body from the last request. |
| ResponseMessage()   | Returns the HTTP response message from the last request. |
| Endpoint()          | Returns the endpoint URL for the request.     |
| getKey()            | Returns the key for the current request context. |
| getEndPointsMap()   | Returns the map of endpoint names to URLs.    |
| getHeadersMap()     | Returns the map of HTTP headers.              |
| getUrlParamsMap()   | Returns the map of URL parameters.            |
| getResponseBodiesMap() | Returns the map of response bodies.        |
| getResponseCodesMap()  | Returns the map of response codes.         |
| getResponseMessagesMap() | Returns the map of response messages.    |
| getUserData()       | Returns the UserDataAccessApi for data sheet operations. |

---

## Execution Context API

The `getExecutionContext()` method returns an `ExecutionContextApi` instance, the entry point for accessing the current test run, project, and settings from within a plugin action.

#### Control

| Original | INGenious-API Class | INGenious-API Method | Description |
|---|---|---|---|
| `Control.exe` | `ExecutionContextApi` | `getRunner()` → returns `TestRunnerApi` | Returns the `TestRunnerApi` representing the currently executing test run. |
| `Control.ReportManager` | `ExecutionContextApi` | `getReportManager()` → returns `SummaryReportApi` | Returns the `SummaryReportApi` used to access the overall execution summary report. |
| `Control.triggerId` | `ExecutionContextApi` | `getTriggerId()` | Returns the trigger ID associated with the current execution. |
| `Control.executionStartTime` | `ExecutionContextApi` | `getExecutionStartTime()` | Returns the timestamp when the current execution started. |
| `Control.getCurrentProject()` | `ExecutionContextApi` | `getCurrentProject()` → returns `ProjectApi` | Returns the `ProjectApi` for the project currently being executed. |

#### RunSettings

Reached via `getExecutionContext().getRunner().getExecSettings().getRunSettings()`

| Original | INGenious-API Class | INGenious-API Method | Description |
|---|---|---|---|
| `.isVideoEnabled()` | `RunSettingsApi` | `isVideoEnabled()` | Returns whether video recording is enabled for the run. |
| `.isTracingEnabled()` | `RunSettingsApi` | `isTracingEnabled()` | Returns whether Playwright tracing is enabled for the run. |
| `.isHARrecordingEnabled()` | `RunSettingsApi` | `isHARrecordingEnabled()` | Returns whether HAR (HTTP Archive) recording is enabled for the run. |
| `.isPerformanceLogEnabled()` | `RunSettingsApi` | `isPerformanceLogEnabled()` | Returns whether performance logging is enabled for the run. |
| `.isBddReportEnabled()` | `RunSettingsApi` | `isBddReportEnabled()` | Returns whether BDD-style reporting is enabled for the run. |
| `.isModernReport()` | `RunSettingsApi` | `isModernReport()` | Returns whether the modern HTML report format is enabled. |
| `.isGridExecution()` | `RunSettingsApi` | `isGridExecution()` | Returns whether the run is executing against a remote grid. |
| `.getRemoteGridURL()` | `RunSettingsApi` | `getRemoteGridURL()` | Returns the URL of the remote grid used for execution. |
| `.useExistingDriver()` | `RunSettingsApi` | `useExistingDriver()` | Returns whether the run reuses an existing driver instance instead of creating a new one. |
| `.getTakeFullPageScreenShot()` | `RunSettingsApi` | `getTakeFullPageScreenShot()` | Returns whether full-page screenshots are captured. |
| `.getScreenShotFor()` | `RunSettingsApi` | `getScreenShotFor()` | Returns the configured condition(s) for when screenshots are captured. |
| `.getThreadCount()` | `RunSettingsApi` | `getThreadCount()` | Returns the number of threads configured for parallel execution. |
| `.getExecutionTimeOut()` | `RunSettingsApi` | `getExecutionTimeOut()` | Returns the configured execution timeout. |
| `.getExecutionMode()` | `RunSettingsApi` | `getExecutionMode()` | Returns the configured execution mode (e.g., sequential, parallel). |
| `.getIterationMode()` | `RunSettingsApi` | `getIterationMode()` | Returns the configured iteration mode for data-driven execution. |
| `.getRerunTimes()` | `RunSettingsApi` | `getRerunTimes()` | Returns the number of configured rerun attempts for failed tests. |
| `.getTestEnv()` | `RunSettingsApi` | `getTestEnv()` | Returns the configured test environment name (e.g., QA, Prod). Not the same as `getPaths().project().getTestEnv()`, which returns a filesystem path. |
| `.getProperty("key")` | `RunSettingsApi` | `getProperty("key")` | Returns the value of a run setting property by key. |
| `.put("key", "value")` | `RunSettingsApi` | `put("key", "value")` | Sets a run setting property value by key. |

#### Test Management Settings

Reached via `.getExecSettings().getTestMgmgtSettings()`

| Original | INGenious-API Class | INGenious-API Method | Description |
|---|---|---|---|
| `.getTestMgmgtSettings()` | `ExecutionSettingsApi` | `getTestMgmgtSettings()` → returns `TestMgmtSettingsApi` | Returns the `TestMgmtSettingsApi` for accessing test management tool integration settings. |
| `.getTestMgmgtSettings().put("key","value")` | `TestMgmtSettingsApi` | `put("key","value")` | Sets a test management settings property value by key. |

#### ProjectRunner

Reached via `getExecutionContext().getRunner()`

| Original | INGenious-API Class | INGenious-API Method | Description |
|---|---|---|---|
| `Control.exe.getProject()` | `TestRunnerApi` | `getProject()` → returns `ProjectApi` | Returns the `ProjectApi` for the project associated with the current run. |
| `Control.exe.getExecSettings()` | `TestRunnerApi` | `getExecSettings()` → returns `ExecutionSettingsApi` | Returns the `ExecutionSettingsApi` for the current run's execution settings. |
| `Control.exe.getTestSet()` | `TestRunnerApi` | `getTestSet()` → returns `TestSetApi` | Returns the `TestSetApi` representing the test set being executed. |
| `Control.exe.getTestSet().getTestSteps()` | `TestSetApi` | `getTestSteps()` → returns `List<TestStepApi>` | Returns the list of test steps contained in the test set. |
| `Control.exe.getTestSet().getExecSettings()` | `TestSetApi` | `getExecSettings()` → returns `ExecutionSettingsApi` | Returns the execution settings scoped to the test set. |
| `Control.exe.runEnv()` | `TestRunnerApi` | `runEnv()` | Returns the environment the run is executing against. |
| `Control.exe.dataProvider()` | `TestRunnerApi` | `dataProvider()` → returns `ProjectTestDataApi` | Returns the `ProjectTestDataApi` used to access project test data. |
| `Control.exe.dataProvider().defEnv()` | `ProjectTestDataApi` | `defEnv()` | Returns the default environment configured for the project test data. |
| `Control.exe.isContinueOnError()` | `TestRunnerApi` | `isContinueOnError()` | Returns whether the run is configured to continue execution after an error. |
| `Control.exe.useExistingBrowser()` | `TestRunnerApi` | `useExistingBrowser()` | Returns whether the run reuses an existing browser instance. |
| `Control.exe.isDebugExe()` | `TestRunnerApi` | `isDebugExe()` | Returns whether the run is executing in debug mode. |
| `Control.exe.getIterater(scenario, testCase)` | `TestRunnerApi` | `getIterater(scenario, testCase)` → returns `DataIteratorApi` | Returns the `DataIteratorApi` for the given scenario and test case. |
| `Control.exe.getIterater("Scenario#TestCase")` | `TestRunnerApi` | `getIterater("Scenario#TestCase")` → returns `DataIteratorApi` | Returns the `DataIteratorApi` for the given combined scenario#testcase key. |
| `Control.exe.retryExecution()` | `TestRunnerApi` | `retryExecution()` | Returns whether the run is configured to retry execution on failure. |
| `Control.exe.afterExecution(true)` | `TestRunnerApi` | `afterExecution(true)` | Signals that post-execution processing should run after the test completes. |

#### Project

Reached via `getExecutionContext().getCurrentProject()`

| Original | INGenious-API Class | INGenious-API Method | Description |
|---|---|---|---|
| `.getLocation()` | `ProjectApi` | `getLocation()` | Returns the filesystem location of the project. |
| `.getInfo()` | `ProjectApi` | `getInfo()` → returns `ProjectInfoApi` | Returns the `ProjectInfoApi` containing project metadata. |
| `.getInfo().getData()` | `ProjectInfoApi` | `getDataItemNames()` | Returns the list of data item names defined for the project. Returns item names only, not the full nested Data/Attributes/Tags/Meta structure. |
| `.getObjectRepository()` | `ProjectApi` | `getObjectRepository()` → returns `ObjectRepositoryApi` | Returns the `ObjectRepositoryApi` for checking object existence. Minimal surface — only `isObjectPresent`/`isMobileObjectPresent`/`isStructuredDataObjectPresent` are exposed; design-time authoring operations (rename/copy/move/save) are not. |
| `.getTestData()` | `ProjectApi` | `getTestData()` → returns `ProjectTestDataApi` | Returns the `ProjectTestDataApi` for the project. |
| `.getTestData().getTestDataFor(env)` | `ProjectTestDataApi` | `getTestDataFor(env)` → returns `TestDataSetApi` | Returns the `TestDataSetApi` for the specified environment. |
| `.getProjectSettings()` | `ProjectApi` | `getProjectSettings()` → returns `ProjectSettingsApi` | Returns the `ProjectSettingsApi` for the project. |
| `.getReleaseByName("Release1")` | `ProjectApi` | `getReleaseByName("Release1")` → returns `ReleaseApi` | Returns the `ReleaseApi` for the named release. |
| `.getReleaseByName("Release1").getTestSetByName("TS1")` | `ReleaseApi` | `getTestSetByName("TS1")` → returns `TestSetApi` | Returns the `TestSetApi` for the named test set within the release. |

#### ProjectSettings

Reached via `getProjectSettings()`

| Original | INGenious-API Class | INGenious-API Method | Description |
|---|---|---|---|
| `.getExecSettings()` | `ProjectSettingsApi` | `getExecSettings()` → returns `ExecutionSettingsApi` | Returns the `ExecutionSettingsApi` configured at the project level. |
| `.getLocation()` | `ProjectSettingsApi` | `getLocation()` | Returns the filesystem location of the project settings. |
| `.getDriverSettings()` | `ProjectSettingsApi` | `getDriverSettings()` → returns `DriverSettingsApi` | Returns the `DriverSettingsApi` for browser/driver configuration. |
| `.getDriverSettings().useProxy()` | `DriverSettingsApi` | `useProxy()` | Returns whether a proxy is configured for the driver. |
| `.getDriverSettings().selfSigned()` | `DriverSettingsApi` | `selfSigned()` | Returns whether self-signed certificates are accepted by the driver. |
| `.getDriverSettings().put("key","value")` | `DriverSettingsApi` | `put("key","value")` | Sets a driver settings property value by key. |
| `.getUserDefinedSettings()` | `ProjectSettingsApi` | `getUserDefinedSettings()` → returns `UserDefinedSettingsApi` | Returns the `UserDefinedSettingsApi` for accessing user-defined global settings. |

---

## Test Report API

The `getReport()` method returns a `TestCaseReportApi` instance for logging test results. This is essential for providing feedback in the test execution reports.

#### Reporting Methods

| Method Signature | Description |
|------------------|-------------|
| updateTestLog(String stepName, String stepDescription, Status state) | Updates the test log with a step name, description, and status. |
| updateTestLog(String stepName, String stepDescription, Status state, String optionalLink) | Updates the test log with a step name, description, status, and an optional link (e.g., screenshot). |
| updateTestLog(String stepName, String stepDescription, Status state, List<String> optional) | Updates the test log with a step name, description, status, and a list of optional details. |
| updateTestLog(String stepName, String stepDescription, Status state, String optionalLink, List<String> optional) | Updates the test log with a step name, description, status, an optional link, and a list of optional details. |

All plugin APIs can use these methods via the `getReport()` method.

#### **Common reporting examples**

```java
// Get the report instance (typically in constructor)
TestCaseReportApi report = gen.getReport();

// Log test results with different statuses
report.updateTestLog(action, message, Status.PASS);   // Success
report.updateTestLog(action, message, Status.FAIL);   // Failure
report.updateTestLog(action, message, Status.DONE);   // Completed
report.updateTestLog(action, message, Status.PASSNS); // Pass (no screenshot)
report.updateTestLog(action, message, Status.FAILNS); // Fail (no screenshot)
```

**Example from BrowserTestPlugin:**

```java
try {
    Page.navigate(Data, navigateOptions);
    report.updateTestLog("Open", "Opened Url: " + Data, Status.DONE);
} catch (TimeoutError e) {
    report.updateTestLog("Open",
        "Opened Url: " + Data + " and cancelled page load after " + Condition + " seconds", 
        Status.DONE);
} catch (Exception e) {
    report.updateTestLog("Open", e.getMessage(), Status.FAIL);
}
```

**Available Status values:**

- `Status.PASS` - Action passed (with screenshot)
- `Status.FAIL` - Action failed (with screenshot)
- `Status.PASSNS` - Pass without screenshot
- `Status.FAILNS` - Fail without screenshot
- `Status.DONE` - Indicates a message that is logged into the results for informational purposes
- `Status.COMPLETE` - Indicates submission of API Request and generation of Response
- `Status.Warning` - Indicates a warning message   
- `Status.Debug` - Indicates a debug-level message, typically used by automation developers to troubleshoot any errors that may occur

---

## User Data Access

The `getUserData()` method returns a `UserDataAccessApi` instance for accessing and updating test data, global data, and iteration context. Use these methods to dynamically read from or write to your test data sheets and global variables during plugin execution.


####  User Data Access Methods (`UserDataAccessApi`)
| Method Signature | Description |
|------------------|-------------|
| String getCurrentScenario() | Gets the current scenario name in execution context. |
| String getCurrentTestCase() | Gets the current test case name in execution context. |
| String getScenario() | Gets the scenario name for the current data context. |
| String getTestCase() | Gets the test case name for the current data context. |
| String getIteration() | Gets the current iteration value. |
| String getTestCaseSubIteration() | Gets the sub-iteration value for the current test case. |
| String getSubIteration() | Gets the current sub-iteration value. |
| int getSubIterationAsNumber() | Gets the current sub-iteration as an integer. |
| String getGlobalData(String globalDataID, String columnName) | Retrieves a value from the global data store. |
| void putGlobalData(String globalDataID, String columnName, String value) | Updates a value in the global data store. |
| String getData(String sheet, String column) | Retrieves a value from the test data sheet for the current context. |
| String getData(String sheet, String column, String iteration, String subIteration) | Retrieves a value from the test data sheet for a specific iteration and sub-iteration. |
| String getData(String sheet, String column, String scenario, String testcase, String iteration, String subiteration) | Retrieves a value from the test data sheet for a specific scenario, testcase, iteration, and sub-iteration. |
| void putData(String sheet, String column, String value) | Updates a value in the test data sheet for the current context. |
| void putData(String sheet, String column, String value, String iteration, String subIteration) | Updates a value in the test data sheet for a specific iteration and sub-iteration. |
| void putData(String sheet, String column, String value, String scenario, String testcase, String iteration, String subIteration) | Updates a value in the test data sheet for a specific scenario, testcase, iteration, and sub-iteration. |
| TestDataViewApi getTestData(String sheetName) | Gets a view of the test data for the specified sheet. |

All plugin APIs can use these methods via the `getUserData()` method.

---

#### Example Usage of UserDataAccessApi

Here are real-world examples from the plugin templates showing how to use `UserDataAccessApi` methods in your plugin actions:

**Store element text in a data sheet (Browser Plugin Template):**
    ```java
    String text = Locator.textContent();
    String sheetName = Data;
    String columnName = Input;
    userData.putData(sheetName, columnName, text);
    ```

**Retrieve data from a data sheet (Webservice Plugin Template):**
    ```java
    String value = userData.getData(sheetName, columnName);
    ```

You can use these methods to read and write test data dynamically during your test execution. See the plugin templates for more advanced patterns.