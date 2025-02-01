# **Scroll Actions** 

## **scrollInAndroid**

**Description**: This function will scroll to element text in Android

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`scrollInAndroid`](#)   | @Data       |  | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`scrollInAndroid`](#)   | DatasheetName:ColumnName |  | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`scrollInAndroid`](#)   | %variableName% |  | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc ="Scroll to Element Text in Android", input = InputType.YES)
    public void scrollInAndroid() {
        try {
            mDriver.findElement(AppiumBy.androidUIAutomator("new UiScrollable(new UiSelector().scrollable(true)).scrollIntoView(new UiSelector().text(\"" + Data + "\"))"));
            Report.updateTestLog(Action, "Scrolled to '" + Data + "'", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog("Could not perfom [" + Action + "] action", "Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
----------------------


## **scrollInIOS**

**Description**: This function will scroll to element in IOS

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`scrollInIOS`](#)   | @Data       |  | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`scrollInIOS`](#)   | DatasheetName:ColumnName |  | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`scrollInIOS`](#)   | %variableName% |  | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc ="Scroll to Element in iOS", input = InputType.YES, condition = InputType.YES)
    public void scrollInIOS() {
        try {
            HashMap<String, Object> scrollObject = new HashMap<>();
            scrollObject.put("direction", Condition.toLowerCase());
            String attribute = Data.split("=")[0];
            String value = Data.split("=")[1];
            scrollObject.put(attribute,value);
            IOSDriver driver = (IOSDriver) mDriver;
            driver.executeScript("mobile:scroll",scrollObject);
            Report.updateTestLog(Action, "Scrolled to '" + Data + "'", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog("Could not perfom [" + Action + "] action", "Error: " + e.getMessage(), Status.FAIL);
        }
    }

    ```
----------------------

