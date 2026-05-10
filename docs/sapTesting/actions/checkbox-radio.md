# **Checkbox & Radio Button Actions**
------------------------

This section documents SAP checkbox and radio button actions for SAP GUI automation in INGenious.

---

### **sapSelectCheckBox**
**Description**: Select or deselect a checkbox.

**Input Format**: true/false

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectCheckBox`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectCheckBox`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectCheckBox`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Set checkbox [<Object>] to [<Data>] (true/false)", input = InputType.YES)
    public void sapSelectCheckBox() {
        try {
            Dispatch.put(SAPelement, "Selected", Boolean.parseBoolean(Data));
            Report.updateTestLog(Action, "Checkbox set to [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to set checkbox. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSelectRadioButtonInRow**
**Description**: Select radio button in table row.

**Input Format**: Row number

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectRadioButtonInRow`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectRadioButtonInRow`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectRadioButtonInRow`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select Radio Button in row [<Data>]", input = InputType.YES)
    public void sapSelectRadioButtonInRow() {
        try {
            Dispatch.put(SAPtable.getAbsoluteRow(Integer.parseInt(Data)), "Selected", true);
            Report.updateTestLog(Action, "Radio button selected in row [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to select radio button. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
