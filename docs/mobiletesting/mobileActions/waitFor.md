# **WaitFor Actions** 

## **waitForAlertPresent**

**Description**: This function will wait for alert to be present

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Mobile   |:green_circle: [`waitForAlertPresent`](#)| | |  |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Wait for alert to be present ", condition = InputType.OPTIONAL)
    public void waitForAlertPresent() {
        waitFor(WaitType.ALERT_PRESENT,
                "Alert popped up in stipulated time");
    }
    ```
----------------------

## **waitForAppElementToBeVisible**

**Description**: This function will wait for element to be visible

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | mobileObject   |:green_circle: [`waitForAppElementToBeVisible`](#)| | |  PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for [<Object>] to be visible ", condition = InputType.OPTIONAL)
    public void waitForAppElementToBeVisible() {
        waitForElement(WaitType.VISIBLE, "'"
                + this.ObjectName
                + "' Element becomes visible in stipulated time");
    }
    ```
----------------------

## **waitForElementToBeInVisible**

**Description**: This function will wait for element to be invisible

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | mobileObject   |:green_circle: [`waitForElementToBeInVisible`](#)| | |  PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for [<Object>] to be invisible ", condition = InputType.OPTIONAL)
    public void waitForElementToBeInVisible() {
        waitForElement(WaitType.INVISIBLE, "'"
                + this.ObjectName
                + "' Element becomes invisible in stipulated time");
    }
    ```
----------------------

## **waitForElementToBeTapable**

**Description**: This function will wait for element to be tapable

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | mobileObject   |:green_circle: [`waitForElementToBeTapable`](#)| | |  PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for [<Object>] to be Tapable ", condition = InputType.OPTIONAL)
    public void waitForElementToBeTapable() {
        waitForElement(WaitType.CLICKABLE, "'"
                + this.ObjectName
                + "' Element becomes Tapable in stipulated time");
    }
    ```
----------------------

## **waitForElementToBeSelected**

**Description**: This function will wait for element to be selected

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | mobileObject   |:green_circle: [`waitForElementToBeSelected`](#)| | |  PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for [<Object>] to be selected ", condition = InputType.OPTIONAL)
    public void waitForElementToBeSelected() {
        waitForElement(WaitType.SELECTED, "'"
                + this.ObjectName
                + "' Element Selected in stipulated time");
    }
    ```
----------------------

## **waitForElementToContainText**

**Description**: This function will wait for element to contain text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | mobileObject   |:green_circle: [`waitForElementToContainText`](#)| | |  PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for element: [<Object>] to contain text [<Data>]", condition = InputType.OPTIONAL, input = InputType.YES)
    public void waitForElementToContainText() {
        waitForElement(WaitType.TEXT_CONTAINS, "'"
                + this.ObjectName + "' Element contained the text: "
                + Data + " in stipulated Time");
    }
    ```
----------------------

## **waitForElementToContainValue**

**Description**: This function will wait for element to contain value

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | mobileObject   |:green_circle: [`waitForElementToContainValue`](#)| | |  PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for [<Object>] element to contain value: [<Data>]", condition = InputType.OPTIONAL, input = InputType.YES)
    public void waitForElementToContainValue() {
        waitForElement(WaitType.VALUE_CONTAINS, "'"
                + this.ObjectName + "' Element contained the value: "
                + Data + " in stipulated Time");
    }
    ```
----------------------

## **waitForElementSelectionToBeTrue**

**Description**: This function will wait for element to be selected 

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | mobileObject   |:green_circle: [`waitForElementSelectionToBeTrue`](#)| | |  PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for [<Object>] element to be selected: [<Data>]", condition = InputType.OPTIONAL)
    public void waitForElementSelectionToBeTrue() {
        waitForElement(WaitType.EL_SELECT_TRUE, "'"
                + this.ObjectName
                + "' Element got Selected in the stipulated time");
    }
    ```
----------------------

## **waitForElementSelectionToBeFalse**

**Description**: This function will wait for element to be deselected 

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | mobileObject   |:green_circle: [`waitForElementSelectionToBeFalse`](#)| | |  PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for [<Object>] element to be deselected", condition = InputType.OPTIONAL)
    public void waitForElementSelectionToBeFalse() {
        waitForElement(WaitType.EL_SELECT_FALSE, "'"
                + this.ObjectName
                + "' Element got Deselected in the stipulated time");
    }
    ```
----------------------

## **waitForTitleToBe**

**Description**: This function will wait for page's title to match value given in Input column 

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`waitForTitleToBe`](#)   | @Data       |  | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`waitForTitleToBe`](#)   | DatasheetName:ColumnName |  | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`waitForTitleToBe`](#)   | %variableName% |  | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Wait for page's title to be [<Data>]", input = InputType.YES, condition = InputType.OPTIONAL)
    public void waitForTitleToBe() {
        waitFor(WaitType.TITLE_IS,
                "Title Equals '"
                + Data + "' in stipulated Time");
    }
    ```
----------------------

## **waitForTitleToContain**

**Description**: This function will wait for page's title to contain value given in Input column 

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`waitForTitleToContain`](#)   | @Data       |  | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`waitForTitleToContain`](#)   | DatasheetName:ColumnName |  | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`waitForTitleToContain`](#)   | %variableName% |  | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Wait for page's title to contain [<Data>]", condition = InputType.OPTIONAL, input = InputType.YES)
    public void waitForTitleToContain() {
        waitFor(WaitType.TITLE_CONTAINS,
                "Title Contains the value '"
                + Data + "' in stipulated Time");
    }
    ```
----------------------

## **waitForElementToBePresent**

**Description**: This function will wait for element to be present 

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`waitForElementToBePresent`](#)   |       |  | PageName |    

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait  for the element [<Object>] to be present", condition = InputType.OPTIONAL)
    public void waitForElementToBePresent() {
        MObject.setWaitTime(getWaitTime());
        try {
            Element = mObject.findElement(ObjectName, Reference);
            MObject.resetWaitTime();
            if (Element != null) {
                Report.updateTestLog(Action, "'" + this.ObjectName
                        + "' Element Present in the stipulated time", Status.PASS);
            } else {
                throw new ElementException(ElementException.ExceptionType.Element_Not_Found, ObjectName);
            }

        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            throw new ForcedException(Action,
                    ex.getMessage());
        }
    }

    ```
----------------------

## **waitForFrameAndSwitch**

**Description**: This function will wait for frame to be available and switch to it 

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`waitForFrameAndSwitch`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`waitForFrameAndSwitch`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`waitForFrameAndSwitch`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Wait for Frame To Be Available and Switch to it", input = InputType.OPTIONAL,
            condition = InputType.OPTIONAL)
    public void waitForFrameAndSwitch() {
        if (Element != null) {
            waitFor(WaitType.FRAME_EL, "Switched to Frame By Object '"
                    + ObjectName + "' in stipulated Time");
        } else if (Data != null) {
            if (Data.matches("[0-9]+")) {
                waitFor(WaitType.FRAME_IND, "Switched to Frame By Index '"
                        + Data + "' in stipulated Time");
            } else {
                waitFor(WaitType.FRAME_STR, "Switched to Frame By Value '"
                        + Data + "' in stipulated Time");
            }
        }
    }
    ```
----------------------
