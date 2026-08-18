---
icon: material/focus-field
---

# Focus Actions
------------------------


## **Focus**

**Description**:  This function is used to **focus** on an element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`Focus`](#)   |     |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Focus on the [<Object>] ")
        public void Focus() {
        try {
                Locator.focus();
                Report.updateTestLog(Action, "Focussing on " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Element not Found. Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-------------------------------------------------

## **Blur**

**Description**:  This function is used to **blur** an element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`Blur`](#)   |     |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Remove focus from [<Object>] ",input = InputType.YES)
        public void Blur() {
        try {
                Locator.blur();
                Report.updateTestLog(Action, "Removing focus from " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Element not Found. Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```
-------------------------------------------------

## **Highlight**

**Description**:  This function is used to **Highlight** an element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`Highlight`](#)   |     |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Highlight the element [<Object>]", input = InputType.OPTIONAL)
        public void Highlight() {        
            try {
                Locator.highlight();
                Report.updateTestLog(Action, "Element ["+ ObjectName +"] Highlighted",Status.PASS);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-------------------------------------------------

## **ScrollIntoViewIfNeeded**

**Description**:  This function is used to **scroll into view** an element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`ScrollIntoViewIfNeeded`](#)   |     |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc ="Scroll in to view the [<Object>]")
        public void ScrollIntoViewIfNeeded() {
            try{
                Locator.scrollIntoViewIfNeeded();
                Report.updateTestLog(Action, "Scrolled to view for " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-------------------------------------------------

## **TakePageScreenshot**

**Description**:  This function is used to **take screenshot** of the page

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`TakePageScreenshot`](#)   |     |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Take a Screen Shot ")
        public void TakePageScreenshot() {
            try {
                Report.updateTestLog(Action, "Screenshot is taken", Status.PASS);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.DEBUG);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }

    ```

-------------------------------------------------

## **TakeElementScreenshot**

**Description**:  This function is used to **take screenshot** of an element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`TakeElementScreenshot`](#)   |     |       | PageName |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Take a Screen Shot of [<Object>]")
        public void TakeElementScreenshot() {
            try {
                Locator.screenshot();
                Report.updateTestLog(Action, "Element Screenshot is taken", Status.PASS);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.DEBUG);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```