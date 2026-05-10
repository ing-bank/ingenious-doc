# **Status Bar Actions (GuiStatusBar)**
------------------------

This section documents SAP status bar actions for SAP GUI automation in INGenious.

---

### **sapGetStatusBarText**
**Description**: Get status bar text.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapGetStatusBarText`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Get status bar text from [<Object>]", input = InputType.NO)
    public void sapGetStatusBarText() {
        try {
            String text = Dispatch.get(SAPstatusBar, "Text").toString();
            Report.updateTestLog(Action, "Status bar text: " + text, Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to get status bar text. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
