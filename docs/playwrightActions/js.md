---
icon: simple/javascript
---

# JavaScript Actions
------------------------

## **BrowserExecuteEval**

**Description**: This function is used to **execute a Java Script** on the browser

**Input Format** : @Java Script to be executed

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`BrowserExecuteEval`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`BrowserExecuteEval`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`BrowserExecuteEval`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "To execute the JavaScript commands", input = InputType.YES)
        public void BrowserExecuteEval() {
            try {
                Page.evaluate(Data);
                Report.updateTestLog(Action, "Javascript executed", Status.DONE);

            } catch (Exception ex) {
                Logger.getLogger(JSCommands.class.getName()).log(Level.SEVERE, null, ex);

                Report.updateTestLog(Action, "Javascript execution failed", Status.DEBUG);

            }
        }
    ```

----------------------

## **LocatorExecuteEval**

**Description**: This function is used to **execute a Java Script** on the element

**Input Format** : @Java Script to be executed

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`LocatorExecuteEval`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`LocatorExecuteEval`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`LocatorExecuteEval`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "To execute the JavaScript commands", input = InputType.YES)
        public void LocatorExecuteEval() {
            try {
                Locator.evaluate(Data);
                Report.updateTestLog(Action, "Javascript executed", Status.DONE);

            } catch (Exception ex) {
                Logger.getLogger(JSCommands.class.getName()).log(Level.SEVERE, null, ex);

                Report.updateTestLog(Action, "Javascript execution failed", Status.DEBUG);

            }
        }
    ```

----------------------

## **StoreEval**

**Description**: This function is used to **execute and store the value from a Java Script command** in variable

**Input Format** : @Java Script to be executed

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`StoreEval`](#)   | @value       | %var%      | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`StoreEval`](#)   | Sheet:Column | %var%      | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`StoreEval`](#)   | %dynamicVar% | %var%      | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "To Store value from the JavaScript command", input = InputType.YES, condition=InputType.YES)
        public void StoreEval() {
            try {
                String variableName = Condition;
                String value = "";
                if (variableName.matches("%.*%")) {
                    value = (String) Page.evaluate(Data);
                    addVar(variableName, value);
                    Report.updateTestLog(Action, "JS evaluated value stored", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
                }

            } catch (Exception ex) {
                Logger.getLogger(JSCommands.class.getName()).log(Level.SEVERE, null, ex);
                Report.updateTestLog(Action, "Javascript execution failed", Status.DEBUG);

            }
        }
    ```

----------------------


## **fillByJS**

**Description**: This function will `set` data into an input field using `JavaScript`.

**Input Format** : @Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`fillByJS`](#)| @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`fillByJS`](#)| Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`fillByJS`](#)| %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Enter the value [<Data>] in the Field [<Object>]", input = InputType.YES)
        public void fillByJS() {
        try {
                Locator.clear();
                Locator.evaluate("element => element.value='"+Data+"'");
                Report.updateTestLog(Action, "Entered Text '" + Data + "' on '"
                        + "["+ObjectName+"]" + "'", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```    
---------------------------------------------

## **clickByJS**

**Description**: This function will **click** on an element using `JavaScript`.


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`clickByJS`](#)|        |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Click the [<Object>] using JavaScript ")
        public void clickByJS() {
        try {
                Locator.evaluate("element => element.click()");
                Report.updateTestLog(Action, "Clicking on " + "["+ObjectName+"]", Status.DONE);
            } catch(PlaywrightException e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```    
---------------------------------------------
## **clickByJSifVisible**

**Description**: This function will **click** on an element using `JavaScript` if the element is visible.


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`clickByJSifVisible`](#)|        |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Click the [<Object>] if it is displayed")
        public void clickByJSifVisible() {
            if (Locator != null) {
                if (Locator.isVisible()) {
                    clickByJS();
                } else {
                    Report.updateTestLog(Action, "[" + ObjectName + "] is not Visible", Status.DONE);
                }
            } else {
                Report.updateTestLog(Action, "[" + ObjectName + "] does not Exist", Status.DONE);
            }
        }
    ```    