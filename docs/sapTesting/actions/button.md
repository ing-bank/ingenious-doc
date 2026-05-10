# **Button Actions**
------------------------

This section documents SAP button actions for SAP GUI automation in INGenious.

---

### **sapClick**
**Description**: Click/Press button.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapClick`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Click the [<Object>]")
    public void sapClick() {
        try {
            Dispatch.call(SAPelement, "press");
            Report.updateTestLog(Action, "Button clicked", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to click button. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapPressButton**
**Description**: Press button by ID or function code.

**Input Format**: Button ID or function code (e.g., `SAVE`)

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapPressButton`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapPressButton`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapPressButton`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Press button with ID [<Data>]", input = InputType.YES)
    public void sapPressButton() {
        try {
            Dispatch.call(SAPtoolbar, "pressButton", Data);
            Report.updateTestLog(Action, "Pressed button with ID [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to press button. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
