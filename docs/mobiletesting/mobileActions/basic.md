# Mobile Actions
------------------------

## **Tap**

**Description**: This function is used to tap the element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`Tap`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap the [<Object>] ")
    public void Tap() {
        if (elementEnabled()) {
            Element.click();
            Report.updateTestLog(Action, "Taping on " + ObjectName, Status.DONE);

        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }
    ```

----------------------


## **TapIfExists**

**Description**: This function will tap the element if it exists.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`TapIfExists`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap the [<Object>] if it exists")
    public void TapIfExists() {
        if (Element != null) {
            Tap();
        } else {
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not Exists", Status.DONE);
        }
    }
    ```

----------------------
## **TapIfVisible**

**Description**: This function will tap the element if it is displayed.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`TapIfVisible`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap the [<Object>] if it is displayed")
    public void TapIfVisible() {
        if (Element != null) {
            if (Element.isDisplayed()) {
                Tap();
            } else {
                Report.updateTestLog(Action, "Element [" + ObjectName + "] not Visible", Status.DONE);
            }
        } else {
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not Exists", Status.DONE);
        }
    }
    ```
----------------------
## **Submit**

**Description**: This function is used to submit action on the browser.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`Submit`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Submit action on the browser")
    public void Submit() {
        if (elementEnabled()) {
            Element.submit();
            Report.updateTestLog(Action, "[" + ObjectName + "] Submitted successfully ", Status.DONE);

        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }
    ```
----------------------
## **SubmitIfExists**

**Description**: This function is used to submit the element if it exists.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`SubmitIfExists`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Submit the [<Object>] if it exists")
    public void SubmitIfExists() {
        if (Element != null) {
            Submit();
        } else {
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not Exists", Status.DONE);
        }
    }
    ```
----------------------

## **Set**

**Description**: This function is used to set the value.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`Set`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`Set`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`Set`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Enter the value [<Data>] in the Field [<Object>]", input = InputType.YES)
    public void Set() {
        if (elementEnabled()) {
            Element.clear();
            Element.sendKeys(Data);
            Report.updateTestLog(Action, "Entered Text '" + Data + "' on '"
                    + ObjectName + "'", Status.DONE);
        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }
    ```
----------------------------------------

## **SetIfExists**

**Description**: This function is used to set the value if the element exists.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`SetIfExists`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`SetIfExists`](#)  | Sheet:Column |      | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`SetIfExists`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Enter the value [<Data>] in the [<Object>] if it exists", input = InputType.YES)
    public void SetIfExists() {
        if (Element != null) {
            Set();
        } else {
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not Exists", Status.DONE);
        }
    }
    ```
----------------------------------------

## **SetAndCheck**

**Description**: This function is used to set the value and check the expected text matches with element value.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`SetAndCheck`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`SetAndCheck`](#)   | Sheet:Column |   | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`SetAndCheck`](#)   | %dynamicVar% |   | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Enter the value [<Data>] in the Field [<Object>] and check [<Data>] matches with [<Object>] value", input = InputType.YES)
    public void SetAndCheck() {
        if (elementEnabled()) {
            Element.clear();
            Element.sendKeys(Data);
            if (Element.getAttribute("value").equals(Data)) {
                Report.updateTestLog("Set", "Entered Text '" + Data + "' on '"
                        + ObjectName + "'", Status.DONE);
            } else {
                Report.updateTestLog("Set", "Unable Enter Text '" + Data
                        + "' on '" + ObjectName + "'", Status.FAIL);
            }
        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }
    ```
-------------------------------

## **clear**

**Description**: This function is used to clear text from the element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`clear`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Clear text [<Data>] from object [<Object>].")
    public void clear() {
        if (elementEnabled()) {
            Element.clear();
            Report.updateTestLog("Clear", "Cleared Text on '" + ObjectName + "'", Status.DONE);
        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }
    ```
----------------------

## **setEncrypted**

**Description**: This function is used to set an encrypted data to an element.

**Input Format** : @Expected encrypted text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`setEncrypted`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`setEncrypted`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`setEncrypted`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Enter the Decrypted value [<Data>] in the Field [<Object>]", input = InputType.YES)
    public void setEncrypted() {
        if (Data != null && Data.matches(".* Enc")) {
            if (elementEnabled()) {
                try {
                    Element.clear();
                    Data = Data.substring(0, Data.lastIndexOf(" Enc"));
                    byte[] valueDecoded = Encryption.getInstance().decrypt(Data).getBytes();
                    Element.sendKeys(new String(valueDecoded));
                    Report.updateTestLog(Action, "Entered Encrypted Text " + Data + " on " + ObjectName, Status.DONE);
                } catch (Exception ex) {
                    Report.updateTestLog("setEncrypted", ex.getMessage(), Status.FAIL);
                    Logger.getLogger(Basic.class.getName()).log(Level.SEVERE, null, ex);
                }
            } else {
                throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
            }
        } else {
            Report.updateTestLog(Action, "Data not encrypted '" + Data + "'", Status.DEBUG);
        }
    }
    ```

---------------------------------

## **moveTo**

**Description**: This function is used to move the browser view to the specified element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`moveTo`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP,
            desc = "Move the Browser View to the specified element [<Object>]")
    public void moveTo() {
        if (elementDisplayed()) {
            if (Data != null && Data.matches("(\\d)+,(\\d)+")) {
                int x = Integer.valueOf(Data.split(",")[0]);
                int y = Integer.valueOf(Data.split(",")[1]);
                new Actions(mDriver).moveToElement(Element, x, y).build().perform();
            } else {
                new Actions(mDriver).moveToElement(Element).build().perform();
            }
            Report.updateTestLog(Action, "Viewport moved to" + ObjectName, Status.DONE);
        } else {
            throw new ElementException(ExceptionType.Element_Not_Visible, ObjectName);
        }
    }
    ```
----------------------
## **changeWaitTime**

**Description**: This function is used to change the wait time by the expected input in seconds.

**Input Format** : @Expected time in seconds

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | MOBILE     |:green_circle: [`changeWaitTime`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE     |:green_circle: [`changeWaitTime`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE     |:green_circle: [`changeWaitTime`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "changing wait time by [<Data>] seconds", input = InputType.YES)
    public void changeWaitTime() {
        try {
            Duration t = Duration.ofSeconds(Integer.parseInt(Data));
            if (Integer.parseInt(Data) > 0) {
                SystemDefaults.waitTime = t;
                Report.updateTestLog("changeWaitTime", "Wait time changed to "
                        + Data + " second/s", Status.DONE);
            } else {
                Report.updateTestLog("changeWaitTime",
                        "Couldn't change Wait time (invalid input)",
                        Status.DEBUG);
            }

        } catch (NumberFormatException ex) {
            Report.updateTestLog("changeWaitTime",
                    "Couldn't change Wait time ", Status.DEBUG);
            Logger.getLogger(Basic.class.getName()).log(Level.SEVERE, null, ex);
        }
    }
    ```

---------------------------------
## **setElementTimeOut**

**Description**: This function is used to change default element finding wait time by input data in seconds

**Input Format** : @Expected data in seconds

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | MOBILE   |:green_circle: [`setElementTimeOut`](#)   | @value       || |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE  |:green_circle: [`setElementTimeOut`](#)   | Sheet:Column || |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE   |:green_circle: [`setElementTimeOut`](#)  | %dynamicVar% || |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE,
            desc = "Change Default Element finding wait time by [<Data>] seconds",
            input = InputType.YES)
    public void setElementTimeOut() {
        if (Data != null && Data.matches("[0-9]+")) {
            SystemDefaults.elementWaitTime = Duration.ofSeconds(Integer.valueOf(Data));
            Report.updateTestLog(Action, "Element Wait time changed to "
                    + Data + " second/s", Status.DONE);
        } else {
            Report.updateTestLog(Action,
                    "Couldn't change Element Wait time (invalid input) " + Data,
                    Status.DEBUG);
        }

    }
    ```

---------------------------------

