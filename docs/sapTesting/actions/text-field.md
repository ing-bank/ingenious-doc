# **Text Field Actions**
------------------------

This section documents SAP text field actions for SAP GUI automation in INGenious.

---

### **sapFill**
**Description**: Enter the value in the field.

**Input Format**: Value to enter (e.g., `Test123`)

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapFill`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapFill`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapFill`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Enter the value [<Data>] in the field [<Object>]", input = InputType.YES)
    public void sapFill() {
        try {
            Dispatch.put(SAPelement, "Text", Data);
            Report.updateTestLog(Action, "Entered value [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to enter value. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapEnter**
**Description**: Press Enter key in the field.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapEnter`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Press [<Enter>] key", input = InputType.NO)
    public void sapEnter() {
        try {
            Dispatch.call(SAPelement, "sendVKey", 0);
            Report.updateTestLog(Action, "Pressed Enter key", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to press Enter. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
