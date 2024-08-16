# Verify
------------------------------------

## **verifyPageSource**

**Description**: This function will verify if the page source content of the current page is matching with the expected page source content provided by the user.

**Input Format** : @Expected PageSource content

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*verifyPageSource*| @value       |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*verifyPageSource*| Sheet:Column |       | PageName|<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*verifyPageSource*| %dynamicVar% |       | PageName|<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify if Page source of current page is: [<Data>]", input = InputType.YES)
    public void verifyPageSource() {
        boolean value = Driver.getPageSource().equals(Data);
        Report.updateTestLog(
                Action,
                "Current Page Source is" + (value ? "" : " not") + " matched with the expected Page Source",
                Status.getValue(value));
    }
```

---------------------------------------


## **verifyVariable**

**Description**:  This function will verify a `stored variable's` value with the value given by the user.

**Input Format** : @%var_name%=Expected Value

**Usage:**

| ObjectName | Action            | Input        | Condition |Reference|  |
|------------|-------------------|--------------|-----------|---------|--|
| Browser     |*verifyVariable*   | @value       |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span>
| Browser     |*verifyVariable*   | Sheet:Column |       | PageName|<span style="color:Blue"><< *Input from Datasheet*</span>
| Browser     |*verifyVariable*   | %dynamicVar% |       | PageName|<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify if the specific [<Data>] is present", input = InputType.YES)

    public void verifyVariable() {
        String strObj = Data;
        String[] strTemp = strObj.split("=", 2);
        String strAns = getVar(strTemp[0]);
        if (strAns.equals(strTemp[1])) {
            System.out.println("Variable " + strTemp[0] + " equals "
                    + strTemp[1]);
            Report.updateTestLog(Action,
                    "Variable is matched with the expected result", Status.PASS);
        } else {
            System.out.println("Variable " + strTemp[0] + " not equals "
                    + strTemp[1]);
            Report.updateTestLog(Action,
                    "Variable doesn't match with the expected result",
                    Status.FAIL);
        }
    }
```

----------------------


## **verifyCookiePresent**

**Description**: This function will verify the presence of a `cookie` by it's specified name.

**Input Format** :   @CookieName

**Usage:**

| ObjectName | Action                 | Input        | Condition   |Reference|  |
|------------|------------------------|--------------|-------------|---------|--|
| Browser    |*verifyCookiePresent*   | @value       |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
| Browser    |*verifyCookiePresent*   | Sheet:Column |       | PageName|<span style="color:Blue"><< *Input from Datasheet*<span> 
| Browser    |*verifyCookiePresent*   | %dynamicVar% |      | PageName|<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify if cookie: [<Data>] is present", input = InputType.YES)

    public void verifyCookiePresent() {
        try {

            String strCookieName = Data;
            if ((Driver.manage().getCookieNamed(strCookieName) != null)) {
                System.out.println(Action + " Passed");
                Report.updateTestLog(Action,
                        "Cookie with name [" + Data + "] is available",
                        Status.PASS);
            } else {
                System.out.println(Action + " Failed");
                Report.updateTestLog(Action,
                        "Cookie with name [" + Data + "] is not available",
                        Status.FAIL);
            }
        } catch (Exception e) {
            Report.updateTestLog(Action, e.getMessage(),
                    Status.FAIL);
            Logger.getLogger(Verifications.class.getName()).log(Level.SEVERE, null, e);
        }
    }
```
----------------------


## **verifyCookieByName**

**Description**:  This function will verify the `cookie's` (the name of the cookie is given is specified in the input column) value with the one in the input column

**Input Format** :   @CookieName:CookieValue

**Usage:**

| ObjectName | Action                 | Input      | Condition   |Reference|  |
|------------|------------------------|------------|-------------|---------|--|
| Browser    |*verifyCookieByName*    |  @data     |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
     
Inputs in the Input column can be passed from `hardcoded` (in this case the data is preceded by a "**@**"), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify if cookie by name: [<Data>] is present ", input = InputType.YES)

    public void verifyCookieByName() {
        try {

            String strCookieName = Data.split(":", 2)[0];
            String strCookieValue = Data.split(":", 2)[1];
            Cookie cookie = Driver.manage().getCookieNamed(strCookieName);
            if (cookie != null) {
                if ((strCookieValue.equals(cookie.getValue()))) {
                    System.out.println(Action + " Passed");
                    Report.updateTestLog(Action,
                            "Cookie value  is matched with the expected result",
                            Status.PASS);
                } else {
                    Report.updateTestLog(Action, "Cookie value doesn't match with the expected result",
                            Status.FAIL);
                }
            } else {
                System.out.println(Action + " Failed");
                Report.updateTestLog(Action,
                        "Cookie with name [" + Data + "] is not available",
                        Status.FAIL);
            }
        } catch (Exception e) {
            Report.updateTestLog(Action, e.getMessage(),
                    Status.FAIL);
            Logger.getLogger(Verifications.class.getName()).log(Level.SEVERE, null, e);
        }
    }
```
----------------------


## **verifyAlertText**

**Description**:  This function will verify the text present in alert with the given text.

**Input Format** :  @Expected Text

**Usage:**

| ObjectName | Action                 | Input        | Condition   |Reference|  |
|------------|------------------------|--------------|-------------|---------|--|
| Browser    |*verifyAlertText*       | @value       |        | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
| Browser    |*verifyAlertText*       | Sheet:Column |        | PageName|<span style="color:Blue"><< *Input from Datasheet*<span> 
| Browser    |*verifyAlertText*       | %dynamicVar% |        | PageName|<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify the specified [<Data>] text is present in the alert pop up box [<Object>]", input = InputType.YES)

    public void verifyAlertText() {
        try {

            String strExpAlertText = Data;
            if ((Driver.switchTo().alert().getText().equals(strExpAlertText))) {
                System.out.println(Action + " Passed");
                Report.updateTestLog(Action,
                        "Alert text is matched with the expected result",
                        Status.PASSNS);
            } else {
                Report.updateTestLog(Action,
                        "Alert text doesn't match with the expected result",
                        Status.FAILNS);
            }
        } catch (Exception e) {
            Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
            Logger.getLogger(Verifications.class.getName()).log(Level.SEVERE, null, e);
        }
    }
```
----------------------


## **verifyAlertPresent**

**Description**:  This function will verify the presence of an `alert`

**Usage:**

| ObjectName | Action                 | Input        | Condition   |Reference|  |
|------------|------------------------|--------------|-------------|---------|--|
| Browser    |*verifyAlertPresent*    |              |             | 

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify if the specific alert[<Object>] is present ")

    public void verifyAlertPresent() {
        try {
            if ((isAlertPresent(Driver))) {
                System.out.println(Action + " Passed");
                Report.updateTestLog(Action,
                        "Alert is present",
                        Status.PASSNS);
            } else {
                Report.updateTestLog(Action,
                        "Alert is not present",
                        Status.FAILNS);
            }
        } catch (Exception e) {
            Report.updateTestLog(Action, e.getMessage(),
                    Status.FAILNS);
            Logger.getLogger(Verifications.class.getName()).log(Level.SEVERE, null, e);
        }
    }
```

----------------------


## **verifyVariableFromDataSheet**

**Description**:   This function will verify if the `variable` given in the condition column has a value equals to the value from the datasheet mentioned in the input column. 

**Input Format** :   Datasheet name:Column name

**Condition Format**: %Variable name%

**Usage:**


| ObjectName | Action                       | Input        | Condition   |Reference|  |
|------------|------------------------------|--------------|-------------|---------|--|
| Browser    |*verifyVariableFromDataSheet* | Sheet:Column | %variable% |PageName|<span style="color:Blue"><< *Input from Datasheet*</span> 

Inputs in the Input column can be either passed from the data sheet (`datasheet name : column name`)  as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify of variable [<Data>] from given datasheet", input = InputType.YES, condition = InputType.YES)
    public void verifyVariableFromDataSheet() {
        String strAns = getVar(Condition);
        if (strAns.equals(Data)) {
            System.out.println("Variable " + Condition + " equals "
                    + Input);
            Report.updateTestLog(Action,
                    "Variable is matched with the expected result", Status.DONE);

        } else {
            System.out.println("Variable " + Condition + " is not equal "
                    + Input);
            Report.updateTestLog(Action,
                    "Variable doesn't matched with the expected result",
                    Status.DEBUG);
        }
    }
```

----------------------


## **verifyTitle**

**Description**:  This function will verify if the title of the current page is equals the user-provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*verifyTitle*   | @value       |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*verifyTitle*   | Sheet:Column |       | PageName|<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*verifyTitle*   | %dynamicVar% |       | PageName|<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify if the title is [<Input>]", input = InputType.YES)
    public void verifyTitle() {
        String strObj = Data;
        if (Driver.getTitle().equals(strObj)) {
            System.out.println(Action + " Passed");
            Report.updateTestLog(Action,
                    "Element Title value " + Driver.getTitle()
                    + " is matched with the expected result",
                    Status.PASS);
        } else {
            System.out.println(Action + " failed");
            Report.updateTestLog(Action,
                    "Element Title value " + Driver.getTitle()
                    + " doesn't match with the expected result",
                    Status.FAIL);

        }
    }
```

----------------------


## **verifyTextPresentInPage**

**Description**:  This function will search for the expected `text` within the html tag of the page and verify the same.

**Input Format** :   @Expected Text

**Usage:**

| ObjectName | Action                     | Input         | Condition |Reference|  |
|------------|----------------------------|---------------|-----------|---------|--|
| Browser     |*verifyTextPresentInPage*   | @value       |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
| Browser     |*verifyTextPresentInPage*   | Sheet:Column |       | PageName|<span style="color:Blue"><< *Input from Datasheet*</span>
| Browser     |*verifyTextPresentInPage*   | %dynamicVar% |       | PageName|<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Assert if text: [<Data>] is present on the page", input = InputType.YES)

    public void verifyTextPresentInPage() {
        String strObj = Data;
        if (Driver.findElement(By.tagName("html")).getText().contains(strObj)) {
            Report.updateTestLog(Action, "Expected text "
                    + Data + " is present in the page", Status.PASS);
        } else {
            Report.updateTestLog(Action, "Expected text "
                    + Data + " is not present in the page", Status.FAIL);

        }
    }
```

------------------


## **verifyHScrollBarPresent**

**Description**: This function will verify if horizontal scrollbar is present.

**Usage:**

| ObjectName | Action                    | Input           | Condition |Reference| 
|------------|--------                   |--------------   |-----------|---------|
| Object     |*verifyHScrollBarPresent*  |                 |           | PageName|

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify if the HScrollBar is present")
    public void verifyHScrollBarPresent() {
        verifyHScorllBar("", isHScrollBarPresent());
    }
```
**Internally uses the following** `Javascript` **logic**:

Checks whether the scroll bar is present ( see code below ),then using the derived Boolean result in the above method:
```javascript
 document.documentElement.scrollWidth>document.documentElement.clientWidth
```

---------------------------


## **verifyHScrollBarNotPresent**

**Description**: This function will check if horizontal scrollbar is not present.

**Usage:**

| ObjectName | Action                       | Input           | Condition |Reference| 
|------------|--------                      |--------------   |-----------|---------|
| Object     |*verifyHScrollBarNotPresent*  |                 |           | PageName|

**Corresponding Code:**

```java
   @Action(object = ObjectType.BROWSER, desc = "Verify if the HScrollBar is not present")
    public void verifyHScrollBarNotPresent() {
        verifyHScorllBar("not", !isHScrollBarPresent());
    }
```
**Internally uses the following** `Javascript` **logic**:

Checks whether the scroll bar is present ( see code below ),then uses the derived Boolean result in the above method:
```java
document.documentElement.scrollWidth>document.documentElement.clientWidth
```

---------------------------


## **verifyVScrollBarPresent**

**Description**:   This function will verify if vertical scrollbar is present.

**Usage:**

| ObjectName | Action                    | Input           | Condition |Reference| 
|------------|--------                   |--------------   |-----------|---------|
| Object     |*verifyVScrollBarPresent*  |                 |           | PageName|

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER, desc = "Verify if the VScrollBar is present")
    public void verifyVScrollBarPresent() {
        verifyVScorllBar("", isvScrollBarPresent());
    }
```
**Internally uses the following** `Javascript` **logic**:

Checks whether the scroll bar is present ( see code below ),then uses the derived Boolean result in the above method:
```java
document.documentElement.scrollHeight>document.documentElement.clientHeight
```

---------------------------


## **verifyVScrollBarNotPresent**

**Description**: This function will verify if vertical scrollbar is not present.

**Usage:**

| ObjectName | Action                    | Input           | Condition |Reference| 
|------------|--------                   |--------------   |-----------|---------|
| Object     |*verifyVScrollBarNotPresent*  |                 |           | PageName|

**Corresponding Code:**

```java
	@Action(object = ObjectType.BROWSER, desc = "Verify if the VScrollBar is not present")
    public void verifyVScrollBarNotPresent() {
        verifyVScorllBar("not", !isvScrollBarPresent());
    }
```
**Internally uses the following** `Javascript` **logic**:

Checks whether the scroll bar is present ( see code below ),then negates the derived Boolean result in the above method:
```java
document.documentElement.scrollHeight>document.documentElement.clientHeight
```

---------------------------