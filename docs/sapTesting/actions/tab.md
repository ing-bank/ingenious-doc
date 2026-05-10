# **Tab Actions**
------------------------

This section documents SAP tab actions for SAP GUI automation in INGenious.

---

### **sapSelect**
**Description**: Select a tab.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelect`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select the [<Object>]")
    public void sapSelect() {
        try {
            Dispatch.call(SAPtab, "select");
            Report.updateTestLog(Action, "Tab selected", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to select tab. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
