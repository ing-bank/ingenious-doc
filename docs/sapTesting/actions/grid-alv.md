# **Grid/ALV Actions (GuiGridView)**
------------------------

This section documents SAP Grid/ALV actions for SAP GUI automation in INGenious.

---

### **sapSelectGridRow**
**Description**: Select ALV grid row.

**Input Format**: Row number

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectGridRow`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectGridRow`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectGridRow`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select ALV grid row [<Data>]", input = InputType.YES)
    public void sapSelectGridRow() {
        try {
            Dispatch.call(SAPgrid, "SelectRow", Integer.parseInt(Data));
            Report.updateTestLog(Action, "Grid row [" + Data + "] selected", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to select grid row. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
