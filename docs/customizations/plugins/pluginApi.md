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