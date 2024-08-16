---
icon: material/form-dropdown
---



# Dropdown & Checkbox Actions
------------------------

## **SelectSingleByText**

**Description**: This function is used to **select a single value** from a `select` type object.

**Input Format** : @Value

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`SelectSingleByText`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | Object     |:green_circle: [`SelectSingleByText`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`SelectSingleByText`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Select item in [<Object>] which has text: [<Data>]", input = InputType.YES)
        public void SelectSingleByText() {
            try
            {
            Locator.selectOption(Data);
            Report.updateTestLog(Action, "Item '" + Data
                            + "' is selected" + " from list [" + ObjectName +"]", Status.DONE);
            }
            catch (Exception e){
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **SelectMultipleByText**

**Description**: This function is used to **select multiple values** from a `select` type object.

**Input Format** : @Values seperated by Pipe. For example `Value1`|`Value2`|`Value3`|`Value4`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`SelectMultipleByText`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | Object     |:green_circle: [`SelectMultipleByText`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`SelectMultipleByText`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Select items [<Data>] of [<Object>] by visible Text", input = InputType.YES)
        public void SelectMultipleByText() {
            try
            {
            String options[] = Data.split("|");
            Locator.selectOption(options);
            Report.updateTestLog(Action, "Items '" + Data
                            + "' are selected" + " from list [" + ObjectName +"]", Status.DONE);
            }
            catch (Exception e){
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------------------

## **SelectSingleByTextIfDataExists**

**Description**:  This function is used to `select` a single value from a select type object if data exists, else that step will be ignored.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object     |:green_circle: [`SelectSingleByTextIfDataExists`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | Object     |:green_circle: [`SelectSingleByTextIfDataExists`](#)    | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`SelectSingleByTextIfDataExists`](#)    | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Select item in [<Object>] which has text: [<Data>] if it Data exists", input = InputType.YES)
        public void SelectSingleByTextIfDataExists() {
            Page.waitForLoadState();
            if (!Data.isEmpty()) {
                SelectSingleByText();
            } else {
                Report.updateTestLog(Action, "Data not present", Status.DONE);
            }
        }
    ```
----------------------------------

## **SelectSingleByTextIfVisible**

**Description**:  This function will check if an element is visible. If the element is visible, it will `select` a single value from a select type object, else that step will be ignored.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object     |:green_circle: [`SelectSingleByTextIfVisible`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | Object     |:green_circle: [`SelectSingleByTextIfVisible`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`SelectSingleByTextIfVisible`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Select item in [<Object>] if visible which has text: [<Data>]", input = InputType.YES)
        public void SelectSingleByTextIfVisible() {
            Page.waitForLoadState();
            if (Locator.isVisible()) {
                SelectSingleByText();
            } else {
                Report.updateTestLog(Action, "[" + ObjectName + "]" + " is not visible", Status.DONE);
            }
    }
    ```
----------------------------------

## **Check**

**Description**: This function is used to **check** a `check-box` type object.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`Check`](#)   |       |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Check the [<Object>] element")
        public void Check() {
            if (Locator != null) {
                if (Locator.isEnabled()) {
                    if (!Locator.isChecked()) {
                        Locator.check();
                    }
                    if (Locator.isChecked()) {
                        Report.updateTestLog("check", "Checkbox '" + Locator
                                + "'  has been selected/checked successfully",
                                Status.DONE);
                    } else {
                        Report.updateTestLog("check", "Checkbox '" + Locator
                                + "' couldn't be selected/checked", Status.FAIL);
                    }
                } else {
                    Report.updateTestLog("check", "Checkbox '" + Locator
                            + "' is not enabled", Status.FAIL);
                }
            } else {
                Report.updateTestLog(Action, "Object [" + ObjectName + "] not found", Status.FAIL);
            }
        }
    ```

----------------------

## **Uncheck**

**Description**: This function is used to **uncheck** a `check-box` type object.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`Uncheck`](#)   |       |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEB, desc = "Uncheck the [<Object>] element")
        public void Uncheck() {
            if (Locator != null) {
                if (Locator.isEnabled()) {
                    if (Locator.isChecked()) {
                        Locator.uncheck();
                    }
                    if (!Locator.isChecked()) {
                        Report.updateTestLog("uncheck", "Checkbox '" + Locator
                                + "'  has been un-checked successfully",
                                Status.DONE);
                    } else {
                        Report.updateTestLog("uncheck", "Checkbox '" + Locator
                                + "' couldn't be un-checked", Status.FAIL);
                    }
                } else {
                    Report.updateTestLog("uncheck", "Checkbox '" + Locator
                            + "' is not enabled", Status.FAIL);
                }
            } else {
                Report.updateTestLog(Action, "Object[" + ObjectName + "] not found", Status.FAIL);
            }
        }
    ```

----------------------

## **CheckIfVisible**

**Description**:  This function will check if an element is visible. If the element is visible, it will `check` a check-box type object, else that step will be ignored.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object     |:green_circle: [`CheckIfVisible`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | Object     |:green_circle: [`CheckIfVisible`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`CheckIfVisible`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Check [<Object>] if visible", input = InputType.YES)
        public void CheckIfVisible() {
            Page.waitForLoadState();
            if (Locator.isVisible()) {
                Check();
            } else {
                Report.updateTestLog(Action, "[" + ObjectName + "]" + " is not visible", Status.DONE);
            }
        }
    ```
----------------------------------

## **SetChecked**

**Description**:  This function will `check/uncheck` a checkbox type object.

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|
    |------------|----------------------------|---------------|-----------|---------|
    | Object     |:green_circle: [`SetChecked`](#)   |        |       | |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Check/Uncheck the [<Object>] element based on Data", input = InputType.YES)
        public void SetChecked() {
            try {
                Locator.setChecked(Boolean.parseBoolean(Data));
                Report.updateTestLog(Action, "Setting checked status of" + "[" + ObjectName + "] as [" + Data + "]", Status.DONE);
            } catch (PlaywrightException e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom [" + Action + "] action", "Error: " + e.getMessage(), Status.FAIL);
            }
        }
    ```

----------------------------------------------

## **SetCheckedifDataExists**

**Description**:  This function will `check/uncheck` a checkbox type object based on input data.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object     |:green_circle: [`SetCheckedifDataExists`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | Object     |:green_circle: [`SetCheckedifDataExists`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`SetCheckedifDataExists`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Check/Uncheck the [<Object>] element based on Data", input = InputType.YES)
        public void SetCheckedifDataExists() {
            if (!Data.isEmpty()) {
                SetChecked();
            } else {
                Report.updateTestLog(Action, "Data not present", Status.DONE);
            }
        }
    ```