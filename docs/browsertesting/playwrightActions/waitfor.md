---
icon: material/timer
---

# WaitFor Actions
------------------------

## **waitForElementToBeVisible**

**Description**: This function will **wait for the element to be visible** on page

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`waitForElementToBeVisible`](#)   |       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Wait for [<Object>] to be visible ", condition = InputType.OPTIONAL)
        public void waitForElementToBeVisible() {
            waitForElement("VISIBLE", "Successfully waited for [" + ObjectName + "] to be visible");
        }
    ```
-----------------------------------------------------

## **waitForElementToBeHidden**

**Description**: This function will **wait for the element to be hidden** on page

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`waitForElementToBeHidden`](#)  |       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Wait for [<Object>] to be hidden ", condition = InputType.OPTIONAL)
        public void waitForElementToBeHidden() {
            waitForElement("HIDDEN", "Successfully waited for [" + ObjectName + "] to be hidden");
        }
    ```
-----------------------------------------------------

## **waitForElementToBeAttached**

**Description**: This function will **wait for the element to be attached** to the DOM

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`waitForElementToBeAttached`](#)   |       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Wait for [<Object>] to be attached to the DOM ", condition = InputType.OPTIONAL)
        public void waitForElementToBeAttached() {
            waitForElement("ATTACHED", "Successfully waited for [" + ObjectName + "] to be attached to the DOM");
        }
    ```
-----------------------------------------------------

## **waitForElementToBeDetached**

**Description**: This function will **wait for the element to be detached** from the DOM

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`waitForElementToBeDetached`](#)   |       | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Wait for [<Object>] to be detached from the DOM ", condition = InputType.OPTIONAL)
        public void waitForElementToBeDetached() {
            waitForElement("DETACHED", "Successfully waited for [" + ObjectName + "] to be detached from the DOM");
        }
    ```
-----------------------------------------------------

## **waitForLoadState**

**Description**: This function will **wait for required load state has been reached**

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`waitForLoadState`](#)   |       | | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Wait for required load state has been reached", condition = InputType.OPTIONAL)
        public void waitForLoadState() {
            try
            {
                Page.waitForLoadState();
                Report.updateTestLog(Action, "Successfully waited for required load state has been reached", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, null, ex);
                Report.updateTestLog(Action, "Wait Action Failed", Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------