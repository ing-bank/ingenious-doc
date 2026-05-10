# **Context Menu Actions**
------------------------

This section documents SAP context menu actions for SAP GUI automation in INGenious.

---

### **sapPressContextButton**
**Description**: Press context button with parameter.

**Input Format**: Button ID

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapPressContextButton`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapPressContextButton`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapPressContextButton`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Press context button with parameter [<Data>]", input = InputType.YES)
    public void sapPressContextButton() {
        try {
            Dispatch.call(SAPelement, "pressContextButton", Data);
            Report.updateTestLog(Action, "Pressed context button [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to press context button. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSelectContextMenuItem**
**Description**: Select context menu item.

**Input Format**: Menu ID

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectContextMenuItem`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectContextMenuItem`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectContextMenuItem`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select context menu item [<Data>]", input = InputType.YES)
    public void sapSelectContextMenuItem() {
        try {
            Dispatch.call(SAPelement, "selectContextMenuItem", Data);
            Report.updateTestLog(Action, "Selected context menu item [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to select context menu item. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
