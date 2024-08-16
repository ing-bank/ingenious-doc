---
icon: simple/databricks
---


# Store Actions
------------------------

## **storeElementTextinVariable**

**Description**: This function will **store element text** in a variable

**Input Format** : %variableName%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementTextinVariable`](#)  | %variableName%       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store the [<Object>] element's text into the Runtime variable: [<Data>]", input = InputType.YES)
        public void storeElementTextinVariable() {
            String text = "";
            String strObj = Input;
            try {
                text = Locator.textContent();

                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, text);
                    Report.updateTestLog(Action, "Element text " + text + " is stored in variable " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }

    ```

-----------------------------------------------------
## **storeElementTextinDataSheet**

**Description**: This function will **store element text** in a data sheet

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementTextinDataSheet`](#)   | DatasheetName:ColumnName       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store the [<Object>] element's text into datasheet:columname [<Data>]", input = InputType.YES)
        public void storeElementTextinDataSheet() {
            String text = "";
            String strObj = Input;
            try {
                text = Locator.textContent();

                if (strObj.matches(".*:.*")) {
                    String sheetName = strObj.split(":", 2)[0];
                    String columnName = strObj.split(":", 2)[1];
                    userData.putData(sheetName, columnName, text);
                    Report.updateTestLog(Action, "Element text [" + text
                            + "] is stored in " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action,
                            "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]", Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }

    ```

-----------------------------------------------------

## **storeElementInnerHTMLinVariable**

**Description**: This function will **store element innerHTML** in a variable

**Input Format** : %variableName%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementInnerHTMLinVariable`](#)  | %variableName%       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store the [<Object>] element's inner HTML into the Runtime variable: [<Data>]", input = InputType.YES)
        public void storeElementInnerHTMLinVariable() {
            String text = "";
            String strObj = Input;
            try {
                text = Locator.innerHTML();

                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, text);
                    Report.updateTestLog(Action, "Element's inner HTML " + text + " is stored in variable " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }

    ```

-----------------------------------------------------

## **storeElementInnerHTMLinDataSheet**

**Description**: This function will **store element innerHTML** in a data sheet

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementInnerHTMLinDataSheet`](#)   | DatasheetName:ColumnName       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store the [<Object>] element's inner HTML into datasheet:columname [<Data>]", input = InputType.YES)
        public void storeElementInnerHTMLinDataSheet() {
            String text = "";
            String strObj = Input;
            try {
                text = Locator.innerHTML();

                if (strObj.matches(".*:.*")) {
                    String sheetName = strObj.split(":", 2)[0];
                    String columnName = strObj.split(":", 2)[1];
                    userData.putData(sheetName, columnName, text);
                    Report.updateTestLog(Action, "Element's inner HTML [" + text + "] is stored in " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action,
                            "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
                            Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }

    ```

-----------------------------------------------------


## **storeElementInnerTextinVariable**

**Description**: This function will **store element innerText** in a variable

**Input Format** : %variableName%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementInnerTextinVariable`](#)  | %variableName%       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store the [<Object>] element's inner Text into the Runtime variable: [<Data>]", input = InputType.YES)
        public void storeElementInnerTextinVariable() {
            String text = "";
            String strObj = Input;
            try {
                text = Locator.innerText();

                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, text);
                    Report.updateTestLog(Action, "Element's inner Text " + text + " is stored in variable " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }
    ```

-----------------------------------------------------

## **storeElementInnerTextinDataSheet**

**Description**: This function will **store element innerText** in a data sheet

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementInnerTextinDataSheet`](#)  | DatasheetName:ColumnName       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store the [<Object>] element's inner Text into datasheet:columname [<Data>]", input = InputType.YES)
        public void storeElementInnerTextinDataSheet() {
            String text = "";
            String strObj = Input;
            try {
                text = Locator.innerText();

                if (strObj.matches(".*:.*")) {
                    String sheetName = strObj.split(":", 2)[0];
                    String columnName = strObj.split(":", 2)[1];
                    userData.putData(sheetName, columnName, text);
                    Report.updateTestLog(Action, "Element's inner Text [" + text + "] is stored in " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action,
                            "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
                            Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }
    ```
----------------------------------


## **storeElementInputValueinVariable**

**Description**: This function will **store element Input Value** in a variable

**Input Format** : %variableName%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementInputValueinVariable`](#)  | %variableName%       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store the [<Object>] element's input Value into the Runtime variable: [<Data>]", input = InputType.YES)
        public void storeElementInputValueinVariable() {
            String text = "";
            String strObj = Input;
            try {
                text = Locator.inputValue();

                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, text);
                    Report.updateTestLog(Action, "Element's input Value " + text + " is stored in variable " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }
    ```

-----------------------------------------------------

## **storeElementInputValueinDataSheet**

**Description**: This function will **store element Input Value** in a data sheet

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     | :green_circle: [`storeElementInputValueinDataSheet`](#)  | DatasheetName:ColumnName       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store the [<Object>] element's input Value into datasheet:columname [<Data>]", input = InputType.YES)
        public void storeElementInputValueinDataSheet() {
            String text = "";
            String strObj = Input;
            try {
                text = Locator.inputValue();

                if (strObj.matches(".*:.*")) {
                    String sheetName = strObj.split(":", 2)[0];
                    String columnName = strObj.split(":", 2)[1];
                    userData.putData(sheetName, columnName, text);
                    Report.updateTestLog(Action, "Element's input Value [" + text + "] is stored in " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action,
                            "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
                            Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }

    ```

-------------------------------------------------

## **storeElementAttributeinVariable**

**Description**: This function will **store element's attribute** in a variable

**Input Format** : @AttributeName [Can come from a datasheet or a variable as well]

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementAttributeinVariable`](#)  | @AttributeNName |  %variableName%        | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store [<Object>] element's  attribute into Runtime variable ->  [<Data>]", input = InputType.YES, condition = InputType.YES)
        public void storeElementAttributeinVariable() {
            try {
                addVar(Condition, Locator.getAttribute(Data));
                Report.updateTestLog(Action, "Element's attribute value is stored in variable", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }

    ```
----------------------


## **storeElementValueinVariable**

**Description**: This function will **store element's value** in a variable

**Input Format** :   %variableName%  

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeElementValueinVariable`](#)  |  %variableName%   |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store [<Object>] element's  value  into Runtime variable: -> [<Data>]", input = InputType.YES)
        public void storeElementValueinVariable() {
            try {
                String strObj = Input;
                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, Locator.getAttribute("value"));
                    Report.updateTestLog(Action, "Element's value " + Locator.getAttribute("value")
                            + " is stored in variable '" + strObj + "'", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
                }
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            }
        }

    ```
------------------------------------------------------

## **StoreElementCount**

**Description**: This function will **store element's count** in a variable

**Input Format** :   %variableName%  

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`StoreElementCount`](#)  |  %variableName%   |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Store Element count in Variable", input = InputType.YES)
        public void StoreElementCount() {
            try {
                String variableName = Data;
                String count = String.valueOf(Locator.count());
                if (variableName.matches("%.*%")) {
                    addVar(variableName, count);
                    Report.updateTestLog(Action, "Element count ["+count+"] stored in variable ["+variableName+"]", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error Storing Element count:" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
---------------------------------------------------    

## **storeVariableInDataSheet**

**Description**: This function will **store a variable** in a data sheet

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`storeVariableInDataSheet`](#)  | DatasheetName:ColumnName       |%variableName% | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "store variable value [<Condition>] in data sheet[<Data>]", input = InputType.YES, condition = InputType.YES)
        public void storeVariableInDataSheet() {
            if (Input != null && Condition != null) {
                if (!getVar(Condition).isEmpty()) {
                    System.out.println(Condition);
                    String[] sheetDetail = Input.split(":");
                    String sheetName = sheetDetail[0];
                    String columnName = sheetDetail[1];
                    userData.putData(sheetName, columnName, getVar(Condition));
                    Report.updateTestLog(Action, "Value of variable " + Condition + " has been stored into " + "the data sheet", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "The variable " + Condition + " does not contain any value", Status.FAIL);
                }
            } else {
                Report.updateTestLog(Action, "Incorrect input format", Status.DEBUG);
                System.out.println("Incorrect input format " + Condition);
            }
        }

    ```

-----------------------------------------------------

## **storeVariable**

**Description**: This function will **store data in variable**

**Input Format** : @Data

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`storeVariable`](#)  | @Data       |%variableName% | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "store  value [<Data>] in Variable [<Condition>]", input = InputType.YES, condition = InputType.YES)
        public void storeVariable() {
            if (Condition.startsWith("%") && Condition.endsWith("%")) {
                addVar(Condition, Data);
                Report.updateTestLog(Action, "Value" + Data + "' is stored in Variable '" + Condition + "'", Status.DONE);
            } else {
                Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
            }
        }
    ```

-----------------------------------------------------

## **StoreStorageState**

**Description**: This function will **store storage state** of the page in json file

**Input Format** : @FilePath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`StoreStorageState`](#)  | @FilePath       | | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Store Storage State in JSON file", input = InputType.YES)
        public void StoreStorageState() {
            try {
                BrowserContext.storageState(new BrowserContext.StorageStateOptions().setPath(Paths.get(Data)));
                Report.updateTestLog(Action, "Storage State successfully stored ", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error storing storage state :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

-----------------------------------------------------