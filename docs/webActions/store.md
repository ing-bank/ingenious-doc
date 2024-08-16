# Store
------------------------------------

## **storePageSource**

**Description**: This function will store the page source content of the current page.

**Input Format** : @Expected PageSource content

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*storePageSource*| @value       |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*storePageSource*| Sheet:Column |       | PageName|<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*storePageSource*| %dynamicVar% |       | PageName|<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Store the [<Object>] page source into the Runtime variable: -> [<Data>]", input = InputType.YES)
    public void storePageSource() {
        String strObj = Input;
        if (strObj.startsWith("%") && strObj.endsWith("%")) {
            addVar(strObj, Driver.getPageSource());
            Report.updateTestLog(Action,
                    "Page source is stored in variable '" + strObj + "'",
                    Status.DONE);
        } else {
            Report.updateTestLog(Action,
                    "Variable format is not correct", Status.FAIL);
        }
    }
```

-------------------------------------------------------------------------------------

## **storeVariable**

**Description**:  This function will store a `variable` value in the variable given by the user.

**Input Format** : @%var_name%=Expected Value

**Usage:**

| ObjectName | Action            | Input        | Condition |Reference|  |
|------------|-------------------|--------------|-----------|---------|--|
| Browser     |*storeVariable*   | @value       |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span>
| Browser     |*storeVariable*   | Sheet:Column |       | PageName|<span style="color:Blue"><< *Input from Datasheet*</span>
| Browser     |*storeVariable*   | %dynamicVar% |       | PageName|<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "store  value [<Data>] in Variable [<Condition>]", input = InputType.YES, condition = InputType.YES)
    public void storeVariable() {
        if (Condition.startsWith("%") && Condition.endsWith("%")) {
            addVar(Condition, Data);
            Report.updateTestLog(Action, "Value" + Data
                    + "' is stored in Variable '" + Condition + "'",
                    Status.DONE);
        } else {
            Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
        }
    }
```
----------------------


## **storeCookiePresent**

**Description**: This function will store the presence of a `cookie` by it's specified name.

**Input Format** :   @CookieName

**Usage:**

| ObjectName | Action                 | Input        | Condition   |Reference|  |
|------------|------------------------|--------------|-------------|---------|--|
| Browser    |*storeCookiePresent*   | @value       | %variable%       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
| Browser    |*storeCookiePresent*   | Sheet:Column | %variable%       | PageName|<span style="color:Blue"><< *Input from Datasheet*<span> 
| Browser    |*storeCookiePresent*   | %dynamicVar% | %variable%       | PageName|<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Store in Runtime variable Exist/Not Exist based on the  presence of cookie ->[<Data>]", input = InputType.YES, condition = InputType.YES)
    public void storeCookiePresent() {
        String variableName = Condition;
        String cookieName = Data;
        if (variableName.matches("%.*%")) {
            if (Driver.manage().getCookieNamed(cookieName) != null) {
                addVar(variableName, "Exist");
            } else {
                addVar(variableName, "Not Exist");
            }
            Report.updateTestLog(Action,
                    "Cookie presense flag is stored in variable " + variableName + "",
                    Status.DONE);
        } else {
            Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
        }
    }
```
----------------------

## **storeCookieByName**

**Description**:  This function will store the `cookie's` value (the name of the cookie is specified in the input column).

**Input Format** :   @CookieName:CookieValue

**Usage:**

| ObjectName | Action                 | Input      | Condition   |Reference|  |
|------------|------------------------|------------|-------------|---------|--|
| Browser    |*storeCookieByName*    |  @data     |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
     
Inputs in the Input column can be passed from `hardcoded` (in this case the data is preceded by a "**@**"), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Store value of cookie into Runtime variable -> [<Data>]", input = InputType.YES, condition = InputType.YES)
    public void storeCookieByName() {
        String variableName = Condition;
        String cookieName = Data;
        if (variableName.matches("%.*%")) {
            addVar(variableName, Driver.manage().getCookieNamed(cookieName)
                    .getValue());
            Report.updateTestLog(Action, "Cookie Stored", Status.DONE);
        } else {
            Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
        }
    }
```
----------------------


## **storeAlertText**

**Description**:  This function will store the text present in alert.

**Input Format** :  @Expected Text

**Usage:**

| ObjectName | Action                 | Input        | Condition   |Reference|  |
|------------|------------------------|--------------|-------------|---------|--|
| Browser    |*storeAlertText*       | @value       |        | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
| Browser    |*storeAlertText*       | Sheet:Column |        | PageName|<span style="color:Blue"><< *Input from Datasheet*<span> 
| Browser    |*storeAlertText*       | %dynamicVar% |        | PageName|<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Store the text of alert present into -> [<Data>] Runtime variable", input = InputType.YES)
    public void storeAlertText() {
        String strObj = Input;
        if (strObj.startsWith("%") && strObj.endsWith("%")) {
            addVar(strObj, Driver.switchTo().alert().getText());
            Report.updateTestLog(Action, "Alert Text "
                    + Driver.switchTo().alert().getText()
                    + " is Stored in variable " + strObj + "", Status.DONE);
        } else {
            Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
        }
    }
```
----------------------

## **storeAlertPresent**

**Description**:  This function will store the presence of an `alert`

**Usage:**

| ObjectName | Action                 | Input        | Condition   |Reference|  |
|------------|------------------------|--------------|-------------|---------|--|
| Browser    |*storeAlertPresent*    | Sheet:Column |        | PageName|<span style="color:Blue"><< *Input from Datasheet*<span> |

**Corresponding Code:**

```java
 @Action(object = ObjectType.BROWSER, desc = "Store \"Exist\" or \"Not Exist\" based on the alert presence into -> [<Data>] Runtime variable", input = InputType.YES)
    public void storeAlertPresent() {
        String strObj = Input;
        if (strObj.startsWith("%") && strObj.endsWith("%")) {
            if (isAlertPresent(Driver)) {
                addVar(strObj, "Exist");
            } else {
                addVar(strObj, "Not Exist");
            }
            Report.updateTestLog(Action, "Alert Text Status Stored", Status.DONE);
        } else {
            Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
        }
    }
```
----------------------


## **storeCurrentUrl**

**Description**:   This function will store the URL of current page.

**Input Format** :   Datasheet name:Column name

**Usage:**


| ObjectName | Action                       | Input        | Condition   |Reference|  |
|------------|------------------------------|--------------|-------------|---------|--|
| Browser    |*storeCurrentUrl* | Sheet:Column |  | |<span style="color:Blue"><< *Input from Datasheet*</span> 

Inputs in the Input column can be either passed from the data sheet (`datasheet name : column name`)  as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Store the current page url into the Runtime variable: [<Data>]", input = InputType.YES)
    public void storeCurrentUrl() {
        String strObj = Input;
        if (strObj.startsWith("%") && strObj.endsWith("%")) {
            addVar(strObj, Driver.getCurrentUrl());
            Report.updateTestLog(Action, "Current URL '" + Driver.getCurrentUrl()
                    + "' is stored in variable '" + strObj + "'", Status.PASS);
        } else {
            Report.updateTestLog(Action, "Variable format is not correct", Status.FAIL);
        }
    }
```
----------------------


## **storeData**

**Description**:   This function will store the data.

**Input Format** :   Datasheet name:Column name

**Usage:**


| ObjectName | Action                       | Input        | Condition   |Reference|  |
|------------|------------------------------|--------------|-------------|---------|--|
| Browser    |*storeData* | Sheet:Column |  | |<span style="color:Blue"><< *Input from Datasheet*</span> 

Inputs in the Input column can be either passed from the data sheet (`datasheet name : column name`)  as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.ANY, desc = "Store variable value in to datasheet", input = InputType.YES)
    public void storeData() {
        try {
            String sheet = Data.split(",", -1)[0];
            String col = Data.split(",", -1)[1];
            String val = Data.split(",", -1)[2];
            if (val.startsWith("%") && val.endsWith("%")) {
                val = this.getVar(val);
            }
            userData.putData(sheet, col, val);
            Report.updateTestLog(Action, "Store  action is done", Status.DONE);
        } catch (Exception ex) {
            Report.updateTestLog(Action, ex.getMessage(), Status.FAIL);
            Logger.getLogger(Application.class.getName()).log(Level.SEVERE, null, ex);
        }
    }
```
----------------------

## **storeTitle**

**Description**:   This function will store the Title.

**Input Format** :   Datasheet name:Column name

**Usage:**


| ObjectName | Action                       | Input        | Condition   |Reference|  |
|------------|------------------------------|--------------|-------------|---------|--|
| Browser    |*storeTitle* | Sheet:Column |  | |<span style="color:Blue"><< *Input from Datasheet*</span> 

Inputs in the Input column can be either passed from the data sheet (`datasheet name : column name`)  as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "store the webpage title in variable named [<Data>].", input = InputType.YES)
    public void storeTitle() {
        String strObj = Input;
        if (strObj.startsWith("%") && strObj.endsWith("%")) {
            addVar(strObj, Driver.getTitle());
            Report.updateTestLog(Action, "Page title '" + Driver.getTitle() + "' is stored in '"
                    + strObj + "'", Status.PASS);
        } else {
            Report.updateTestLog(Action, "Variable format is not correct", Status.FAIL);
        }
    }
```
----------------------