# **General Element Actions**
------------------------

This section documents general SAP element actions for SAP GUI automation in INGenious.

---

### **sapSetFocus**
**Description**: Set focus on element.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSetFocus`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Set focus on [<Object>]", input = InputType.NO)
    public void sapSetFocus() {
        try {
            Dispatch.call(SAPelement, "setFocus");
            Report.updateTestLog(Action, "Focus set on element", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to set focus. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapDoubleClick**
**Description**: Double-click on element.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapDoubleClick`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Double click on [<Object>]")
    public void sapDoubleClick() {
        try {
            Dispatch.call(SAPelement, "doubleClick");
            Report.updateTestLog(Action, "Element double-clicked", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to double-click. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSetObjectProperty**
**Description**: Set object property at runtime.

**Input Format**: property value of SAP object

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSetObjectProperty`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSetObjectProperty`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSetObjectProperty`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Set object [<Object>] property as [<Data>] at runtime", input = InputType.YES, condition = InputType.YES)
    public void sapSetObjectProperty() {
        if (!Data.isEmpty()) {
            // ...property setting logic...
        }
    }
    ```

---
