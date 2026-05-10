# **Table Control Actions (GuiTableControl)**
------------------------

This section documents SAP table control actions for SAP GUI automation in INGenious.

---

### **sapSelectTableRow**
**Description**: Select table row.

**Input Format**: Row number

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectTableRow`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectTableRow`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectTableRow`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select table row [<Data>]", input = InputType.YES)
    public void sapSelectTableRow() {
        try {
            Dispatch.call(SAPtable, "SelectRow", Integer.parseInt(Data));
            Report.updateTestLog(Action, "Table row [" + Data + "] selected", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to select table row. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSetCurrentCell**
**Description**: Set current table cell.

**Input Format**: row,column

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSetCurrentCell`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSetCurrentCell`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSetCurrentCell`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Set current table cell [<Data>] (format: row,column)", input = InputType.YES)
    public void sapSetCurrentCell() {
        try {
            String[] parts = Data.split(",");
            int row = Integer.parseInt(parts[0]);
            int col = Integer.parseInt(parts[1]);
            Dispatch.call(SAPtable, "SetCurrentCell", row, col);
            Report.updateTestLog(Action, "Current cell set to row [" + row + "], column [" + col + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to set current cell. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
