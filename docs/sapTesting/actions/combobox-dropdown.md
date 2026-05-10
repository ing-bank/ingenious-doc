# **ComboBox/Dropdown Actions**
------------------------

This section documents SAP ComboBox/Dropdown actions for SAP GUI automation in INGenious.

---

### **sapSelectDropDownByText**
**Description**: Select dropdown value by visible text.

**Input Format**: Visible text value

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectDropDownByText`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectDropDownByText`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectDropDownByText`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select dropdown value by visible text [<Data>]", input = InputType.YES)
    public void sapSelectDropDownByText() {
        try {
            Dispatch.put(SAPcomboBox, "Text", Data);
            Report.updateTestLog(Action, "Dropdown value set to [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to set dropdown value. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSelectDropDownByKey**
**Description**: Select dropdown value by key (internal value).

**Input Format**: Key value

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectDropDownByKey`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectDropDownByKey`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectDropDownByKey`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select Dropdown value by Key [<Data>]", input = InputType.YES)
    public void sapSelectDropDownByKey() {
        try {
            Dispatch.put(SAPcomboBox, "Key", Data);
            Report.updateTestLog(Action, "Dropdown key set to [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to set dropdown key. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSelectDropDownByIndex**
**Description**: Select dropdown value by index.

**Input Format**: Index (integer)

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectDropDownByIndex`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectDropDownByIndex`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectDropDownByIndex`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select dropdown value by index [<Data>]", input = InputType.YES)
    public void sapSelectDropDownByIndex() {
        try {
            Dispatch.call(SAPcomboBox, "Select", Integer.parseInt(Data));
            Report.updateTestLog(Action, "Dropdown index set to [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to set dropdown index. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapOpenComboBox**
**Description**: Open dropdown list.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapOpenComboBox`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Open dropdown [<Object>]", input = InputType.NO)
    public void sapOpenComboBox() {
        try {
            Dispatch.call(SAPcomboBox, "Open");
            Report.updateTestLog(Action, "Dropdown opened", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to open dropdown. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapCloseComboBox**
**Description**: Close dropdown list.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapCloseComboBox`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Close dropdown [<Object>]", input = InputType.NO)
    public void sapCloseComboBox() {
        try {
            Dispatch.call(SAPcomboBox, "Close");
            Report.updateTestLog(Action, "Dropdown closed", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to close dropdown. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
