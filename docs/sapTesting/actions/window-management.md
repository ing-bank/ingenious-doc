# **Window Management**
------------------------

This section documents SAP window management actions for SAP GUI automation in INGenious.

---

### **sapMaximizeWindow**
**Description**: Maximize SAP window.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapMaximizeWindow`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Maximize SAP window [<Object>]", input = InputType.NO)
    public void sapMaximizeWindow() {
        try {
            Dispatch.call(SAPwindow, "Maximize");
            Report.updateTestLog(Action, "Window maximized", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to maximize window. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapMinimizeWindow**
**Description**: Minimize SAP window.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapMinimizeWindow`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Minimize SAP window [<Object>]", input = InputType.NO)
    public void sapMinimizeWindow() {
        try {
            Dispatch.call(SAPwindow, "Minimize");
            Report.updateTestLog(Action, "Window minimized", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to minimize window. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapRestoreWindow**
**Description**: Restore SAP window to normal size.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapRestoreWindow`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Restore SAP window [<Object>] to normal size", input = InputType.NO)
    public void sapRestoreWindow() {
        try {
            Dispatch.call(SAPwindow, "Restore");
            Report.updateTestLog(Action, "Window restored", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to restore window. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
