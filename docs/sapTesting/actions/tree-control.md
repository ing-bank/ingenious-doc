# **Tree Control Actions (GuiTree)**
------------------------

This section documents SAP tree control actions for SAP GUI automation in INGenious.

---

### **sapExpandTreeNode**
**Description**: Expand tree node.

**Input Format**: Node key

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapExpandTreeNode`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapExpandTreeNode`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapExpandTreeNode`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Expand tree node [<Data>]", input = InputType.YES)
    public void sapExpandTreeNode() {
        try {
            Dispatch.call(SAPtree, "ExpandNode", Data);
            Report.updateTestLog(Action, "Expanded tree node [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to expand tree node. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapCollapseTreeNode**
**Description**: Collapse tree node.

**Input Format**: Node key

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapCollapseTreeNode`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapCollapseTreeNode`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapCollapseTreeNode`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Collapse tree node [<Data>]", input = InputType.YES)
    public void sapCollapseTreeNode() {
        try {
            Dispatch.call(SAPtree, "CollapseNode", Data);
            Report.updateTestLog(Action, "Collapsed tree node [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to collapse tree node. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
