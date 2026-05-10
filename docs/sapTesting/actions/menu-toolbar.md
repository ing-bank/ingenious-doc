# **Menu & Toolbar Actions**
------------------------

This section documents SAP menu and toolbar actions for SAP GUI automation in INGenious.

---

### **sapSelectMenuItem**
**Description**: Select menu item.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectMenuItem`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select menu item [<Object>]", input = InputType.NO)
    public void sapSelectMenuItem() {
        try {
            Dispatch.call(SAPmenu, "Select");
            Report.updateTestLog(Action, "Menu item selected", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to select menu item. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
