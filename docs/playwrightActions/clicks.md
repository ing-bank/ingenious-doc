---
icon: material/cursor-default-click
---




# Click Actions
------------------------

## **Click**

**Description**: This function will **click** on a web element


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`Click`](#)   |     | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Click the [<Object>] ")
        public void Click() {
        try {
                Locator.click();
                Report.updateTestLog(Action, "Clicking on " + "["+ObjectName+"]", Status.DONE);
            } catch(PlaywrightException e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-----------------------------------------------------

## **ClickIfVisible**

**Description**: This function will **click** on a web element if it is visible on the page


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`ClickIfVisible`](#)   |     | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Click the [<Object>] if it is displayed")
        public void ClickIfVisible() {
            Page.waitForLoadState();
            if (Locator != null) {
                if (Locator.isVisible()) {
                    Click();
                } else {
                    Report.updateTestLog(Action, "Element [" + ObjectName + "] not Visible", Status.DONE);
                }
            } else {
                Report.updateTestLog(Action, "Element [" + ObjectName + "] not Exists", Status.DONE);
            }
        }

    ```

-----------------------------------------------------

## **ClickIfDataExists**

**Description**:  This function will `click` on a web element if data exists, else that step will be ignored.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object     |:green_circle: [`ClickIfDataExists`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`ClickIfDataExists`](#)    | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`ClickIfDataExists`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Click the [<Object>] if Data Exists", input = InputType.YES)
        public void ClickIfDataExists() {
            Page.waitForLoadState();
            if (!Data.isEmpty()) {
                Click();
            } else {
                Report.updateTestLog(Action, "Data not present", Status.DONE);
            }
        }
    ```

-----------------------------------------------------    
## **DoubleClick**

**Description**: This function will **double click** on a web element


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |*DoubleClick*   |     | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Double Click the [<Object>]")
        public void DoubleClick() {
            try {
                Locator.dblclick();
                Report.updateTestLog(Action, "Double Clicking on " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-----------------------------------------------------
## **RightClick**

**Description**: This function will **right click** on a web element


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |*RightClick*   |     | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Right Click the [<Object>]")
        public void RightClick() {
            try {
                Locator.click(new Locator.ClickOptions().setButton(MouseButton.RIGHT));
                Report.updateTestLog(Action, "Right Clicking on " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-----------------------------------------------------
## **ShiftClick**

**Description**: This function will **shift click** on a web element


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |*ShiftClick*   |     | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Shift Click the [<Object>]")
        public void ShiftClick() {
            try {
                Locator.click(new Locator.ClickOptions().setModifiers(Arrays.asList(KeyboardModifier.SHIFT)));
                Report.updateTestLog(Action, "Shift Clicking on " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-----------------------------------------------------

## **MouseHover**

**Description**: This function will **mouse hover** on a web element


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |*MouseHover*   |     | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Click the [<Object>] ")
        public void MouseHover() {
        try {
                Locator.hover();
                Report.updateTestLog(Action, "Hovering on " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-----------------------------------------------------

## **MouseUp**

**Description**: This function will **press mouse up** 


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |*MouseUp*   |     | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Press Mouse Up ")
        public void MouseUp() {
        try {
                Page.mouse().up();
                Report.updateTestLog(Action, "Pressed Mouse Up", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-----------------------------------------------------

## **MouseDown**

**Description**: This function will **press mouse down** 


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |*MouseDown*   |     | | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Press Mouse Down ")
        public void MouseDown() {
        try {
                Page.mouse().down();
                Report.updateTestLog(Action, "Pressed Mouse Down", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Element not Found. Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

-----------------------------------------------------
## **DragElementTo**

**Description**: This function will **drag a source element to target element** 

**Input Format** : @PageName,Target ObjectName - as defined in the Object Repository

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |*DragElementTo*   | @value       |       | PageName|<span style="color:Green"><< *Hardcoded Input*</span> 
    | Object     |*DragElementTo*   | Sheet:Column |       | PageName|<span style="color:Blue"><< *Input from Datasheet*</span>
    | Object     |*DragElementTo*   | %dynamicVar% |       | PageName|<span style="color:Brown"><<*Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Drag Source Object to Target", input = InputType.YES)
        public void DragElementTo() {
            try {
                com.microsoft.playwright.Locator source = Locator;
                String pageName = Data.split(",")[0];
                String targetObject = Data.split(",")[1];
                com.microsoft.playwright.Locator target = AObject.findElement(targetObject, pageName);
                source.dragTo(target);
                Report.updateTestLog(Action, "[" + ObjectName + "] dragged and dropped to object referred in Page [" + pageName + "] and ObjectName [" + targetObject + "]", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }

    ```