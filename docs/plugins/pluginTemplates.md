# Complete Plugin Template

## Using the Templates

1. **Choose the appropriate template** based on your plugin type:
    - **General Purpose Plugin Template**: For general purpose operations
    - **Browser Plugin Template**: For web browser automation
    - **Database Plugin Template**: For database testing
    - **Mobile Plugin Template**: For mobile app testing
    - **Webservice Plugin Template**: For REST API and web service testing

2. **Customize the package name** to match your project structure

3. **Add your custom actions** following the patterns shown

4. **Update the POM.xml** with your plugin entry classes

5. **Build and deploy**: `mvn clean install`



---


## Plugin Class Examples

Below are complete, production-ready plugin entry class templates for different use cases. Each demonstrates proper initialization, error handling, and reporting patterns.
#### General Purpose Plugin Template

Use this template for general testing actions and utility operations:

```{.java .copy}
package com.ing.plugin.general;

import com.ing.ingenious.api.contract.CommandPluginApi;
import com.ing.ingenious.api.contract.reports.TestCaseReportApi;
import com.ing.ingenious.api.contract.data.UserDataAccessApi;
import com.ing.ingenious.api.status.Status;
import com.ing.ingenious.api.types.InputType;
import com.ing.ingenious.api.types.ObjectType;
import com.ing.ingenious.api.annotation.Action;

/**
 * General purpose plugin for text assertions and utility operations
 * 
 * @author Your Name
 */
public class TextAsserts {
    
    CommandPluginApi gen;
    public String Data;
    public String Action;
    public String Input;
    public TestCaseReportApi Report;
    public UserDataAccessApi UserData;

    public TextAsserts(CommandPluginApi gen) {
        System.out.println("TextAsserts Plugin initialized with CommandPluginApi: " + gen);
        this.gen = gen;
        this.Data = gen.getData();
        this.Action = gen.getAction();
        this.Input = gen.getInput();
        this.Report = gen.getReport();
    }

    /**
     * Assert text is in lowercase
     */
    @Action(object = "Text Assertions", desc = "Assert if input is in lower case", input = InputType.YES, condition = InputType.NO)
    public void assertTextInLowerCase() {
        System.out.println("Hello World! This is the assertTextInLowerCase action");
        String var = gen.getVar(Input);
        System.out.println("Input is " + var);
        if (var.equals(var.toLowerCase())) {
            Report.updateTestLog(Action, "The input " + Data + " is in lower case.", Status.PASSNS);
        } else {
            Report.updateTestLog(Action, "The input " + Data + " is not in lower case.", Status.FAILNS);
        }
    }

    /**
     * Assert text is in uppercase
     */
    @Action(object = "Text Assertions", desc = "Assert if input is in upper case", input = InputType.YES, condition = InputType.NO)
    public void assertTextInUpperCase() {
        System.out.println("Hello World! This is the assertTextInUpperCase action");
        String var = gen.getVar(Input);
        System.out.println("Input is " + var);
        if (var.equals(var.toUpperCase())) {
            Report.updateTestLog(Action, "The input " + Data + " is in upper case.", Status.PASSNS);
        } else {
            Report.updateTestLog(Action, "The input " + Data + " is not in upper case.", Status.FAILNS);
        }
    }
    
    /**
     * General action demonstrating ObjectType enum usage
     */
    @Action(object = ObjectType.GENERAL, desc = "General purpose action", input = InputType.YES, condition = InputType.NO)
    public void testObjectypeUsingEnum() {
        String var = gen.getVar(Input);
        System.out.println("This is stored in the variable: " + var);
        Report.updateTestLog(Action, "Status code is : " + Data, Status.DONE);
    }
}
```

---

#### Browser Plugin Template

Use this template for browser automation actions with Playwright:

```{.java .copy}
package com.ing.plugin.browser;

import com.ing.ingenious.api.annotation.Action;
import com.ing.ingenious.api.contract.BrowserPluginApi;
import com.ing.ingenious.api.contract.data.UserDataAccessApi;
import com.ing.ingenious.api.contract.reports.TestCaseReportApi;
import com.ing.ingenious.api.exception.ForcedException;
import com.ing.ingenious.api.types.ObjectType;
import com.ing.ingenious.api.types.InputType;
import com.ing.ingenious.api.status.Status;

import com.microsoft.playwright.Page;
import com.microsoft.playwright.Locator;
import com.microsoft.playwright.PlaywrightException;
import com.microsoft.playwright.TimeoutError;
import com.microsoft.playwright.assertions.LocatorAssertions;
import static com.microsoft.playwright.assertions.PlaywrightAssertions.assertThat;

import java.util.logging.Level;
import java.util.logging.Logger;
import org.apache.commons.lang3.StringUtils;
import org.opentest4j.AssertionFailedError;

/**
 * Browser automation plugin for Playwright-based actions
 * 
 * @author Your Name
 */
public class BrowserTestPlugin {
    
    BrowserPluginApi gen;
    
    public String Data;
    public String Action;
    public String Input;
    public String Condition;
    public TestCaseReportApi Report;
    public UserDataAccessApi UserData;
    public String ObjectName;
    
    public Page Page;
    public Locator Locator;

    public BrowserTestPlugin(BrowserPluginApi gen) {
        System.out.println("BrowserTestPlugin initialized with BrowserPluginApi: " + gen);
        this.gen = gen;
        this.Data = gen.getData();
        this.Action = gen.getAction();
        this.Input = gen.getInput();
        this.Condition = gen.getCondition();
        this.Report = gen.getReport();
        this.UserData = gen.getUserData();
        this.ObjectName = gen.getObjectName();
        this.Page = (Page) gen.getPage();
        this.Locator = (Locator) gen.getLocator();
    }

    /**
     * Navigate to URL with timeout support
     */
    @Action(object = ObjectType.BROWSER, desc = "Open the Url [<Data>] in the Browser", input = InputType.YES, condition = InputType.OPTIONAL)
    public void Open() {
        try {
            Page.NavigateOptions options = new Page.NavigateOptions();
            if (Condition != null && !Condition.isEmpty() && Condition.matches("[0-9]+")) {
                options.setTimeout(Double.parseDouble(Condition) * 1000);
            }
            Page.navigate(Data, options);
            Report.updateTestLog(Action, "Opened " + Data + " in the Browser", Status.DONE);
        } catch (TimeoutError e) {
            if (Condition != null && !Condition.isEmpty()) {
                Report.updateTestLog(Action, 
                    "Opened URL: " + Data + " and cancelled page load after " + Condition + " seconds", 
                    Status.DONE);
            } else {
                Report.updateTestLog(Action, "Page load timed out for URL: " + Data, Status.FAIL);
            }
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
            throw new ForcedException(Action, e.getMessage());
        }
    }

    /**
     * Assert element contains text with visual feedback
     */
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] contains the text [<Data>]", input = InputType.YES)
    public void assertElementContains() {
        String actualText = "";
        try {
            LocatorAssertions.ContainsTextOptions options = new LocatorAssertions.ContainsTextOptions();
            options.setTimeout(getTimeoutValue());
            actualText = Locator.innerHTML();
            highlightElement();
            assertThat(Locator).containsText(Data, options);
            Report.updateTestLog(Action, "Element [" + ObjectName + "] Contains text '" + Data + "'", Status.PASS);
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, actualText);
        } finally {
            removeHighlightFromElement();
        }
    }

    /**
     * Click on element
     */
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Click on [<Object>]")
    public void Click() {
        try {
            highlightElement();
            Locator.click();
            Report.updateTestLog(Action, "Clicked on '" + ObjectName + "'", Status.DONE);
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } finally {
            removeHighlightFromElement();
        }
    }

    /**
     * Fill element with data
     */
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Enter the value [<Data>] in [<Object>]", input = InputType.YES)
    public void Fill() {
        try {
            highlightElement();
            Locator.fill(Data);
            Report.updateTestLog(Action, "Entered '" + Data + "' in '" + ObjectName + "'", Status.DONE);
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } finally {
            removeHighlightFromElement();
        }
    }

    /**
     * Store element text in variable
     */
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store [<Object>] element's text into variable [<Data>]", input = InputType.YES)
    public void storeElementTextinVariable() {
        try {
            String text = Locator.textContent();
            String variableName = Data;
            if (!variableName.matches("%.*%")) {
                Report.updateTestLog(Action, "Variable format incorrect. Expected: %variableName%", Status.FAIL);
                return;
            }
            gen.addVar(variableName, text);
            Report.updateTestLog(Action, "Stored text '" + text + "' in variable " + variableName, Status.DONE);
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        }
    }

    /**
     * Store element text in data sheet
     */
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store [<Object>] element's text into data sheet [<Data>] under column [<Input>]", input = InputType.YES)
    public void storeElementTextinDataSheet() {
        try {
            String text = Locator.textContent();
            String sheetName = Data;
            String columnName = Input;
            UserData.putData(sheetName, columnName, text);
            Report.updateTestLog(Action, "Stored text '" + text + "' in data sheet '" + sheetName + "' under column '" + columnName + "'", Status.DONE);
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Error storing text in data sheet: " + e.getMessage(), Status.FAIL);
        }
    }

    // ========== Helper Methods ==========

    private void highlightElement() {
        Locator.scrollIntoViewIfNeeded();
        Locator.evaluate("element => element.style.outline = '2px solid red'");
    }

    private void removeHighlightFromElement() {
        Locator.evaluate("element => element.style.outline = ''");
    }

    private double getTimeoutValue() {
        double timeout = 5000;
        if (StringUtils.isNotBlank(Condition)) {
            try {
                timeout = Double.parseDouble(Condition) * 1000;
            } catch (NumberFormatException e) {
                // Use default timeout
            }
        }
        return timeout;
    }

    private void PlaywrightExceptionLogging(PlaywrightException e) {
        Report.updateTestLog(Action, "Element [" + ObjectName + "] not found. Error: " + e.getMessage(), Status.FAIL);
        Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
    }

    private void assertionLogging(AssertionFailedError err, String actualText) {
        if (err.getMessage().contains("locator resolved to")) {
            Report.updateTestLog(Action, "[" + ObjectName + "] does not contain text '" + Data + "'. Actual text is '" + actualText + "'", Status.FAIL);
        } else {
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not found on Page", Status.FAIL);
        }
        Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, err);
    }
}
```

---

#### Database Plugin Template

Use this template for database testing actions:

```{.java .copy}
package com.ing.plugin.database;

import com.ing.ingenious.api.contract.DatabasePluginApi;
import com.ing.ingenious.api.contract.data.UserDataAccessApi;
import com.ing.ingenious.api.contract.reports.TestCaseReportApi;
import com.ing.ingenious.api.status.Status;
import com.ing.ingenious.api.types.InputType;
import com.ing.ingenious.api.types.ObjectType;
import com.ing.ingenious.api.annotation.Action;

import java.sql.SQLException;
import java.sql.ResultSet;
import java.util.logging.Level;
import java.util.logging.Logger;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * Database testing plugin for SQL operations
 * 
 * @author Your Name
 */
public class DatabasePlugin {
    
    // API contract instance
    DatabasePluginApi gen;
    
    // Test data fields
    public String Data;
    public String Action;
    public String Input;
    public String Condition;
    public TestCaseReportApi Report;
    public UserDataAccessApi UserData;
    public String ObjectName;

    /**
     * Constructor - receives DatabasePluginApi from framework
     */
    public DatabasePlugin(DatabasePluginApi gen) {
        this.gen = gen;
        this.Data = gen.getData();
        this.Action = gen.getAction();
        this.Input = gen.getInput();
        this.Condition = gen.getCondition();
        this.Report = gen.getReport();
        this.UserData = gen.getUserData();
        this.ObjectName = gen.getObjectName();
    }

    /**
     * Execute DML query with variable substitution
     * Demonstrates processQuery() helper method
     */
    @Action(object = ObjectType.DATABASE, 
            desc = "Execute DML Query Example [<Data>]", 
            input = InputType.YES)
    public void executeDMLQueryExample() {
        try {
            if (Data == null || Data.trim().isEmpty()) {
                Report.updateTestLog(Action, "Query is empty or null", Status.FAIL);
                return;
            }
            
            // Process query for variable substitution using helper method
            String processedQuery = processQuery(Data);
            String originalData = this.Data;
            this.Data = processedQuery;
            
            // Execute DML through framework API
            DMLResult dmlResult = gen.executeDML();
            
            // Restore original data
            this.Data = originalData;
            
            if (dmlResult.isSuccess()) {
                Report.updateTestLog(Action, "DML Query executed successfully: " + processedQuery, Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "DML Query executed but returned false: " + processedQuery, Status.DONE);
            }
                
        } catch (SQLException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, 
                "SQL Error: " + ex.getMessage(), 
                Status.FAIL);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, 
                "Unexpected error: " + ex.getMessage(), 
                Status.FAIL);
        }
    }

    /**
     * Execute SELECT and store column value from result
     * Demonstrates complex query handling with result extraction
     */
    @Action(object = ObjectType.DATABASE, 
            desc = "Execute Query Example [<Data>] and Store Column [<Input>] in [<Condition>]", 
            input = InputType.YES, 
            condition = InputType.YES)
    public void executeQueryAndStoreValueExample() {
        try {
            if (Data == null || Data.trim().isEmpty()) {
                Report.updateTestLog(Action, "Query is empty or null", Status.FAIL);
                return;
            }
            
            String columnName = Input;
            String variableName = Condition;
            
            if (!variableName.matches("%.*%")) {
                Report.updateTestLog(Action, 
                    "Variable format incorrect. Expected: %variableName%", 
                    Status.FAIL);
                return;
            }
            
            // Process and execute query using helper method
            String processedQuery = processQuery(Data);
            String originalData = this.Data;
            this.Data = processedQuery;
            
            gen.executeSelect();
            ResultSet rs = gen.getResult();
            
            if (rs != null && rs.next()) {
                String value = rs.getString(columnName);
                gen.addVar(variableName, value);
                
                Report.updateTestLog(Action, 
                    "Value [" + value + "] from column [" + columnName + 
                    "] stored in " + variableName, 
                    Status.PASS);
            } else {
                Report.updateTestLog(Action, "Query returned no results", Status.DONE);
            }
            
            this.Data = originalData;
            
        } catch (SQLException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, 
                "SQL Error: " + ex.getMessage(), 
                Status.FAIL);
        }
    }

    // ========== Helper Methods ==========

    /**
     * Process query - handles variable substitution
     * Replaces %variableName% with actual values
     */
    private String processQuery(String query) {
        if (query == null) return null;
        
        // Find all variables in format %variableName%
        Pattern pattern = Pattern.compile("%([^%]+)%");
        Matcher matcher = pattern.matcher(query);
        StringBuffer result = new StringBuffer();
        
        while (matcher.find()) {
            String variableName = "%" + matcher.group(1) + "%";
            String value = gen.getVar(variableName);
            
            if (value == null || value.equals(variableName)) {
                // Variable not found, keep original
                matcher.appendReplacement(result, 
                    Matcher.quoteReplacement(variableName));
            } else {
                // Replace with actual value
                matcher.appendReplacement(result, 
                    Matcher.quoteReplacement(value));
            }
        }
        matcher.appendTail(result);
        
        return result.toString();
    }
}
```

---

#### Mobile Plugin Template

Use this template for mobile testing with Appium:

```{.java .copy}
package com.ing.plugin.mobile;

import com.ing.ingenious.api.annotation.Action;
import com.ing.ingenious.api.contract.MobilePluginApi;
import com.ing.ingenious.api.contract.data.UserDataAccessApi;
import com.ing.ingenious.api.contract.drivers.MobileObjectApi;
import com.ing.ingenious.api.contract.reports.TestCaseReportApi;
import com.ing.ingenious.api.types.ObjectType;
import com.ing.ingenious.api.types.InputType;
import com.ing.ingenious.api.status.Status;
import com.ing.ingenious.api.exception.mobile.ElementException;
import com.ing.ingenious.api.exception.mobile.ElementException.ExceptionType;

import java.util.HashMap;
import java.util.logging.Level;
import java.util.logging.Logger;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import io.appium.java_client.AppiumBy;
import io.appium.java_client.ios.IOSDriver;

/**
 * Mobile testing plugin for Appium-based mobile automation
 * 
 * @author Your Name
 */
public class MobileTestPlugin {
    
    MobilePluginApi gen;
    
    public String Data;
    public String Action;
    public String Input;
    public String Condition;
    public TestCaseReportApi Report;
    public UserDataAccessApi UserData;
    public String ObjectName;
    
    public WebDriver mDriver;
    public WebElement Element;
    public MobileObjectApi mObject;

    public MobileTestPlugin(MobilePluginApi gen) {
        System.out.println("MobileTestPlugin initialized with MobilePluginApi: " + gen);
        this.gen = gen;
        this.Data = gen.getData();
        this.Action = gen.getAction();
        this.Input = gen.getInput();
        this.Condition = gen.getCondition();
        this.Report = gen.getReport();
        this.UserData = gen.getUserData();
        this.ObjectName = gen.getObjectName();
        this.Element = (WebElement) gen.getElement();
        this.mDriver = (WebDriver) gen.getMDriver();
        this.mObject = gen.getMObject();
    }

    /**
     * Tap on mobile element
     */
    @Action(object = ObjectType.APP, desc = "Tap on [<Object>]")
    public void Tap() {
        if (gen.elementEnabled()) {
            Element.click();
            Report.updateTestLog(Action, "Tapped on " + ObjectName, Status.DONE);
        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }

    /**
     * Set value in mobile element
     */
    @Action(object = ObjectType.APP, desc = "Enter the value [<Data>] in [<Object>]", input = InputType.YES)
    public void Set() {
        if (gen.elementEnabled()) {
            Element.sendKeys(Data);
            Report.updateTestLog(Action, "Entered '" + Data + "' in '" + ObjectName + "'", Status.DONE);
        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }

    /**
     * Scroll to text in Android
     */
    @Action(object = ObjectType.MOBILE, desc = "Scroll to Text [<Data>] in Android", input = InputType.YES)
    public void scrollInAndroid() {
        try {
            mDriver.findElement(AppiumBy.androidUIAutomator(
                "new UiScrollable(new UiSelector().scrollable(true))" +
                ".scrollIntoView(new UiSelector().text(\"" + Data + "\").instance(0))"
            ));
            Report.updateTestLog(Action, "Scrolled to '" + Data + "'", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog("Could not perform [" + Action + "] action", "Error: " + e.getMessage(), Status.FAIL);
        }
    }

    /**
     * Scroll to element in iOS
     */
    @Action(object = ObjectType.MOBILE, desc = "Scroll to Text [<Data>] in IOS", input = InputType.YES)
    public void scrollInIOS() {
        try {
            HashMap<String, String> scrollObject = new HashMap<>();
            scrollObject.put("direction", "down");
            scrollObject.put("name", Data);
            ((IOSDriver) mDriver).executeScript("mobile: scroll", scrollObject);
            Report.updateTestLog(Action, "Scrolled to '" + Data + "'", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog("Could not perform [" + Action + "] action", "Error: " + e.getMessage(), Status.FAIL);
        }
    }

    /**
     * Assert element is displayed
     */
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is displayed", condition = InputType.OPTIONAL)
    public void assertElementDisplayed() {
        try {
            if (Element.isDisplayed()) {
                Report.updateTestLog(Action, "Element [" + ObjectName + "] is displayed", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element [" + ObjectName + "] is not displayed", Status.FAILNS);
            }
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not found. Error: " + e.getMessage(), Status.FAILNS);
        }
    }

    // ========== Helper Methods ==========

    public boolean elementPresent() {
        return gen.checkIfDriverIsAlive() && Element != null;
    }
}
```

---

#### Webservice Plugin Template

Use this template for REST API and web service testing:

```{.java .copy}
package com.ing.plugin.webservice;

import com.ing.ingenious.api.annotation.Action;
import com.ing.ingenious.api.contract.WebservicePluginApi;
import com.ing.ingenious.api.contract.data.UserDataAccessApi;
import com.ing.ingenious.api.contract.reports.TestCaseReportApi;
import com.ing.ingenious.api.types.ObjectType;
import com.ing.ingenious.api.types.InputType;
import com.ing.ingenious.api.types.RequestMethodType;
import com.ing.ingenious.api.status.Status;

import com.jayway.jsonpath.JsonPath;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.logging.Level;
import java.util.logging.Logger;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * Webservice Test Plugin for REST API testing
 * 
 * @author Your Name
 */
public class WebserviceTestPlugin {

    WebservicePluginApi gen;

    public String Data;
    public String Action;
    public String Input;
    public String Condition;
    public TestCaseReportApi Report;
    public UserDataAccessApi UserData;
    public String ObjectName;

    // Webservice-specific fields
    public String endpoint;
    public String responseCode;
    public String responseMessage;
    public String responseBody;
    public Object connection;
    public String httpAgent;

    // Shared storage - direct access to framework's static maps
    private String key;
    private Map<String, String> endPoints;
    private Map<String, ArrayList<String>> headers;
    private Map<String, ArrayList<String>> urlParams;
    private Map<String, String> responseBodies;
    private Map<String, String> responseCodes;
    private Map<String, String> responseMessages;

    public WebserviceTestPlugin(WebservicePluginApi gen) {
        System.out.println("WebserviceTestPlugin initialized with WebservicePluginApi: " + gen);
        this.gen = gen;
        this.Data = gen.getData();
        this.Action = gen.getAction();
        this.Input = gen.getInput();
        this.Condition = gen.getCondition();
        this.Report = gen.getReport();
        this.UserData = gen.getUserData();
        this.ObjectName = gen.getObjectName();
        
        // Initialize webservice-specific fields from API
        this.endpoint = gen.Endpoint();
        this.responseCode = gen.ResponseCode();
        this.responseMessage = gen.ResponseMessage();
        this.responseBody = gen.ResponseBody();
        this.connection = gen.Connection();
        this.httpAgent = gen.HttpAgent();
        
        // Get references to shared maps from framework
        this.key = gen.getKey();
        this.endPoints = gen.getEndPointsMap();
        this.headers = gen.getHeadersMap();
        this.urlParams = gen.getUrlParamsMap();
        this.responseBodies = gen.getResponseBodiesMap();
        this.responseCodes = gen.getResponseCodesMap();
        this.responseMessages = gen.getResponseMessagesMap();
    }

    /**
     * Execute GET REST request
     */
    @Action(object = ObjectType.WEBSERVICE, desc = "GET Rest Request ", input = InputType.NO, condition = InputType.OPTIONAL)
    public void getRestRequest() {
        try {
            gen.createHttpRequest(RequestMethodType.GET);
            
            // Update local fields with response
            this.responseCode = gen.ResponseCode();
            this.responseBody = gen.ResponseBody();
            this.responseMessage = gen.ResponseMessage();
            
            /** 
             * Report here is optional. createHttpRequest already updates the report with request and response details. 
             * This is just an additional log entry if you want to explicitly log the successful execution of the GET request
             */
            // Report.updateTestLog(Action, "GET request executed successfully. Response code: " + responseCode, Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action,
                    "An unexpected error occurred while executing the GET request : " + "\n" + e.getMessage(),
                    Status.FAIL);
        }
    }

    /**
     * Store JSON element value in runtime variable
     */
    @Action(object = ObjectType.WEBSERVICE, desc = "Store JSON Element", input = InputType.YES, condition = InputType.YES)
    public void storeJSONelement() {
        try {
            String variableName = Condition;
            String jsonpath = Data;
            
            if (variableName.matches("%.*%")) {
                // Get the current response body
                String currentResponseBody = gen.ResponseBody();
                
                if (currentResponseBody != null && !currentResponseBody.isEmpty()) {
                    String value = JsonPath.read(currentResponseBody, jsonpath).toString();
                    gen.addVar(variableName, value);
                    Report.updateTestLog(Action, "JSON element value [" + value + "] stored in variable " + variableName, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Response body is empty or null", Status.DEBUG);
                }
            } else {
                Report.updateTestLog(Action, "Variable format is not correct. Expected format: %variableName%", Status.DEBUG);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error Storing JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    /**
     * Add HTTP header to request
     */
    @Action(object = ObjectType.WEBSERVICE, desc = "Add Header ", input = InputType.YES)
    public void addHeader() {
        try {
            String headerData = Data;

            // Handle datasheet variable substitution: {sheetName:columnName}
            Pattern datasheetPattern = Pattern.compile("\\{([^:]+):([^}]+)\\}");
            Matcher datasheetMatcher = datasheetPattern.matcher(headerData);
            
            while (datasheetMatcher.find()) {
                String sheetName = datasheetMatcher.group(1);
                String columnName = datasheetMatcher.group(2);
                try {
                    String value = UserData.getData(sheetName, columnName);
                    if (value != null) {
                        headerData = headerData.replace("{" + sheetName + ":" + columnName + "}", value);
                    }
                } catch (Exception e) {
                    Report.updateTestLog(Action, "Could not find data for {" + sheetName + ":" + columnName + "}", Status.DEBUG);
                }
            }

            // Handle runtime variable substitution: %variable%
            Pattern variablePattern = Pattern.compile("%\\w+%");
            Matcher variableMatcher = variablePattern.matcher(headerData);

            while (variableMatcher.find()) {
                String variable = variableMatcher.group();
                String value = gen.getVar(variable);
                if (value != null) {
                    headerData = headerData.replaceAll(Pattern.quote(variable), value);
                } else {
                    Report.updateTestLog(Action, "Variable " + variable + " not found", Status.DEBUG);
                }
            }

            // Store the header in shared map
            if (headers.containsKey(key)) {
                headers.get(key).add(headerData);
            } else {
                ArrayList<String> toBeAdded = new ArrayList<>();
                toBeAdded.add(headerData);
                headers.put(key, toBeAdded);
            }
            
            Report.updateTestLog(Action, "Header added [" + headerData + "]", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error adding Header :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    /**
     * POST REST request
     */
    @Action(object = ObjectType.WEBSERVICE, desc = "POST Rest Request ", input = InputType.YES, condition = InputType.OPTIONAL)
    public void postRestRequest() {
        try {
            gen.createHttpRequest(RequestMethodType.POST);
            
            // Update local fields with response
            this.responseCode = gen.ResponseCode();
            this.responseBody = gen.ResponseBody();
            this.responseMessage = gen.ResponseMessage();
            
            /** 
             * Report here is optional. createHttpRequest already updates the report with request and response details. 
             * This is just an additional log entry if you want to explicitly log the successful execution of the POST request
             */
            // Report.updateTestLog(Action, "POST request executed successfully. Response code: " + responseCode, Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action,
                    "An unexpected error occurred while executing the POST request : " + "\n" + e.getMessage(),
                    Status.FAIL);
        }
    }

    /**
     * PUT REST request
     */
    @Action(object = ObjectType.WEBSERVICE, desc = "PUT Rest Request ", input = InputType.YES, condition = InputType.OPTIONAL)
    public void putRestRequest() {
        try {
            System.out.println("Executing PUT request with key: " + key);
            gen.createHttpRequest(RequestMethodType.PUT);
            
            // Update local fields with response
            this.responseCode = gen.ResponseCode();
            this.responseBody = gen.ResponseBody();
            this.responseMessage = gen.ResponseMessage();
            
            /** 
             * Report here is optional. createHttpRequest already updates the report with request and response details. 
             * This is just an additional log entry if you want to explicitly log the successful execution of the PUT request
             */
            // Report.updateTestLog(Action, "PUT request executed successfully. Response code: " + responseCode, Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action,
                    "An unexpected error occurred while executing the PUT request : " + "\n" + e.getMessage(),
                    Status.FAIL);
        }
    }

    /**
     * Assert response code matches expected value
     */
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert Response Code ", input = InputType.YES)
    public void assertResponseCode() {
        try {
            String currentResponseCode = gen.ResponseCode();
            
            if (currentResponseCode != null && currentResponseCode.equals(Data)) {
                Report.updateTestLog(Action, "Status code is : " + Data, Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Status code is : " + currentResponseCode + " but should be " + Data,
                        Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating response code :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    /**
     * Assert response body contains specific text
     */
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert Response Body contains ", input = InputType.YES)
    public void assertResponseBodyContains() {
        try {
            String currentResponseBody = gen.ResponseBody();
            
            if (currentResponseBody != null && currentResponseBody.contains(Data)) {
                Report.updateTestLog(Action, "Response body contains : " + Data, Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Response body does not contain : " + Data, Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating response body :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    /**
     * Assert JSON element equals expected value
     */
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert JSON Element Equals ", input = InputType.YES, condition = InputType.YES)
    public void assertJSONelementEquals() {
        try {
            String currentResponseBody = gen.ResponseBody();
            String jsonpath = Condition;
            String value = JsonPath.read(currentResponseBody, jsonpath).toString();
            
            if (value.equals(Data)) {
                Report.updateTestLog(Action, "Element text [" + value + "] is as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text is [" + value + "] but is expected to be [" + Data + "]",
                        Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    /**
     * Get stored headers for current context
     */
    public List<String> getHeaders() {
        return headers.getOrDefault(key, new ArrayList<>());
    }
}
```

---
## POM.xml Template

Here is a comprehensive `pom.xml` template for creating plugins:

```{.xml .copy}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <groupId>com.ing.plugin</groupId>
    <artifactId>my-custom-plugin</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>
    
    <name>My INGenious Custom Plugin</name>
    <description>Custom plugin for INGenious Playwright Framework</description>
    
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        
        <!-- Version properties for easier maintenance -->
        <ingenious.api.version>3.0</ingenious.api.version>
        <playwright.version>1.50.0</playwright.version>
    </properties>
    
    <dependencies>
        <!-- ============================================= -->
        <!-- REQUIRED: Framework API (provided scope)      -->
        <!-- ============================================= -->
        <dependency>
            <groupId>com.ing</groupId>
            <artifactId>ingenious-api</artifactId>
            <version>${ingenious.api.version}</version>
            <scope>provided</scope>
        </dependency>
        
        <!-- ============================================= -->
        <!-- REQUIRED FOR BROWSER Plugins                  -->
        <!-- Playwright with provided scope                -->
        <!-- ============================================= -->
        <dependency>
            <groupId>com.microsoft.playwright</groupId>
            <artifactId>playwright</artifactId>
            <version>${playwright.version}</version>
            <scope>provided</scope>
        </dependency>

        <!-- ============================================= -->
        <!-- REQUIRED FOR Mobile Plugins                   -->
        <!-- Playwright with provided scope                -->
        <!-- ============================================= -->
        <dependency>
            <groupId>io.appium</groupId>
            <artifactId>java-client</artifactId>
            <version>10.0.0</version>
            <scope>provided</scope>
        </dependency>
        
        <!-- ============================================= -->
        <!-- OPTIONAL: Plugin-specific dependencies       -->
        <!-- Use compile scope - will be packaged in lib  -->
        <!-- ============================================= -->
        
        <!-- Example: Apache Commons for utility functions -->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
            <version>3.12.0</version>
            <scope>compile</scope>
        </dependency>
        
        <!-- Example: JSON processing -->
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.10.1</version>
            <scope>compile</scope>
        </dependency>
        
        <!-- Example: JSONPath for webservice plugins -->
        <dependency>
            <groupId>com.jayway.jsonpath</groupId>
            <artifactId>json-path</artifactId>
            <version>2.8.0</version>
            <scope>compile</scope>
        </dependency>
        
        <!-- Appium for mobile plugins (includes Selenium) -->
        <dependency>
            <groupId>io.appium</groupId>
            <artifactId>java-client</artifactId>
            <version>9.1.0</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>
    
    <build>
        <plugins>
            <!-- ============================================= -->
            <!-- Copy plugin dependencies to lib folder       -->
            <!-- Only compile-scoped dependencies are copied  -->
            <!-- ============================================= -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <version>3.6.0</version>
                <executions>
                    <execution>
                        <id>copy-dependencies</id>
                        <phase>package</phase>
                        <goals>
                            <goal>copy-dependencies</goal>
                        </goals>
                        <configuration>
                            <outputDirectory>${project.build.directory}/lib</outputDirectory>
                            <excludeScope>provided</excludeScope>
                            <excludeTransitive>true</excludeTransitive>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
            
            <!-- ============================================= -->
            <!-- Configure JAR manifest with entry classes    -->
            <!-- List ALL plugin entry classes here           -->
            <!-- ============================================= -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.3.0</version>
                <configuration>
                    <archive>
                        <manifestEntries>
                            <!-- Comma-separated list of fully qualified class names -->
                            <pluginEntryClasses>com.ing.plugin.browser.BrowserTestPlugin,com.ing.plugin.database.DatabasePlugin,com.ing.plugin.mobile.MobileTestPlugin,com.ing.plugin.webservice.WebserviceTestPlugin</pluginEntryClasses>
                            <ImplementationVersion>${project.version}</Implementation-Version>
                        </manifestEntries>
                    </archive>
                </configuration>
            </plugin>
            
            <!-- ============================================= -->
            <!-- Optional: Auto-deploy plugin to target dir   -->
            <!-- Update deploy.dir to your INGenious location -->
            <!-- ============================================= -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-antrun-plugin</artifactId>
                <version>3.1.0</version>
                <executions>
                    <execution>
                        <id>copy-artifacts</id>
                        <phase>package</phase>
                        <configuration>
                            <target>
                                <!-- ⚠️ UPDATE THIS PATH to your INGenious plugins directory -->
                                <property name="deploy.dir" 
                                          value="/path/to/INGenious"/>
                                
                                <!-- Copy plugin JAR -->
                                <copy file="${project.build.directory}/${project.build.finalName}.jar"
                                    tofile="${deploy.dir}/plugins/${project.artifactId}/${project.artifactId}.jar"/>

                                <!-- Copy lib folder only if it exists -->
                                <mkdir dir="${deploy.dir}/plugins/${project.artifactId}/lib"/>
                                <copy todir="${deploy.dir}/plugins/${project.artifactId}/lib">
                                    <fileset dir="${project.build.directory}/lib"/>
                                </copy>

                                <echo message="Plugin deployed to: ${deploy.dir}"/>
                            </target>
                        </configuration>
                        <goals>
                            <goal>run</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```
