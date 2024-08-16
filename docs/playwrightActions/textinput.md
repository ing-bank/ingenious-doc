---
icon: material/text
---




# Text Input Actions
------------------------

## **Fill**

**Description**: This function is used to **enter data** in an `input` type object.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`Fill`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`Fill`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`Fill`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Enter the value [<Data>] in the Field [<Object>]", input = InputType.YES)
        public void Fill() {
        try {
                Locator.clear();
                Locator.fill(Data);
                Report.updateTestLog(Action, "Entered Text '" + Data + "' on '"
                        + "["+ObjectName+"]" + "'", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **FillIfDataExists**

**Description**:  This function is used to `enter` data in an input type object if data exists, else that step will be ignored.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object     |:green_circle: [`FillIfDataExists`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`FillIfDataExists`](#) | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`FillIfDataExists`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Enter the value [<Data>] in the [<Object>] if it Data exists", input = InputType.YES)
        public void FillIfDataExists() {
            Page.waitForLoadState();
            if (!Data.isEmpty()) {
                Fill();
            } else {
                Report.updateTestLog(Action, "Data not present", Status.DONE);
            }
        }
    ```
----------------------------------

## **FillIfVisible**

**Description**:  This function will check if an element is visible. If the element is visible, data will be entered for that element else that step will be ignored.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object     |:green_circle: [`FillIfVisible`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`FillIfVisible`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`FillIfVisible`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Enter the value [<Data>] in the [<Object>] if visible", input = InputType.YES)
        public void FillIfVisible() {
            Page.waitForLoadState();
            if (Locator.isVisible()) {
                Fill();
            } else {
                Report.updateTestLog(Action, "[" + ObjectName + "]" + " is not visible", Status.DONE);
            }
        }
    ```
----------------------------------

## **FillAndCheck**

**Description**: This function is used to **enter data** in object and check if the **element's value matches with the entered value.**

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`FillAndCheck`](#)| @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`FillAndCheck`](#)| Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`FillAndCheck`](#)| %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Enter the value [<Data>] in the Field [<Object>] and check [<Data>] matches with [<Object>] value", input = InputType.YES)
        public void FillAndCheck() {
            try {
                Locator.clear();
                Locator.fill(Data);
                if (Locator.getAttribute("value").equals(Data)) {
                    Report.updateTestLog("Set", "Entered Text '" + Data + "' on '"
                            + "["+ObjectName+"]" + "'", Status.DONE);
                } else {
                    Report.updateTestLog("Set", "Unable Enter Text '" + Data
                            + "' on '" + ObjectName + "'", Status.FAIL);
                }
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```    
---------------------------------------------

## **fillEncrypted**

**Description**: This function is used to **enter encrypted data** to an object

**Input Format** : @Encrypted text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`fillEncrypted`](#)| @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`fillEncrypted`](#)| Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>

    **Note**: If the data is passed from a data sheet, the data in the datasheet should be `encrypted`. To manually encrypt a data, select the data cell, **right click and select Encrypt**

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Enter the Decrypted value [<Data>] in the Field [<Object>]", input = InputType.YES)
        public void fillEncrypted() {
            if (Data != null && Data.matches(".* Enc")) {
                    try {
                        Locator.clear();
                        Data = Data.substring(0, Data.lastIndexOf(" Enc"));
                        byte[] valueDecoded = Encryption.getInstance().decrypt(Data).getBytes();
                        Locator.fill(new String(valueDecoded));
                        Report.updateTestLog(Action, "Entered Encrypted Text " + Data + " on " + "["+ObjectName+"]", Status.DONE);
                    } catch (Exception ex) {
                        Report.updateTestLog(Action, ex.getMessage(), Status.FAIL);
                        Logger.getLogger(TextInput.class.getName()).log(Level.SEVERE, null, ex);
                    }
                
            } else {
                Report.updateTestLog(Action, "Data not encrypted '" + Data + "'", Status.DEBUG);
            }
        }
    ```    
---------------------------------------------

## **PressSequentially**

**Description**: This function is used to **press keys sequentially** in an `input` type object which is adjacent to the provided `label` type element.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`PressSequentially`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object      |:green_circle: [`PressSequentially`](#) | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object       |:green_circle: [`PressSequentially`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Enter the value [<Data>] in the Field [<Object>]", input = InputType.YES)
        public void PressSequentially() {
            try {
                Locator.clear();
                Locator.pressSequentially(Data);
                Report.updateTestLog(Action, "Entered Text '" + Data + "' on '"
                        + "["+ObjectName+"]" + "'", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

-----------------------------------------------

## **Clear**

**Description**:  This function is used to **clear** an input field

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`Clear`](#)  |     |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Clear text [<Data>] from object [<Object>].")
        public void Clear() {
            try {
                Locator.clear();
                Report.updateTestLog("Clear", "Cleared Text on '" + "["+ObjectName+"]" + "'", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```
