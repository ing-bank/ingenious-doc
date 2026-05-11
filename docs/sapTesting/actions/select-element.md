# **ComboBox/Dropdown Select Actions**
------------------------

This section documents SAP general element select actions for SAP GUI automation in INGenious.

---

### **sapSelectDropDownByText**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

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
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

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
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

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
            Dispatch.call(SAPcomboBox, "Item", Integer.parseInt(Data));
            Report.updateTestLog(Action, "Dropdown index set to [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to set dropdown index. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSelectCheckBox**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

**Description**: Select or deselect a checkbox.

**Input Format**: true/false

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectCheckBox`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectCheckBox`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectCheckBox`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Set checkbox [<Object>] to [<Data>] (true/false)", input = InputType.YES)
    public void sapSelectCheckBox() {
        try {
            Dispatch.put(SAPelement, "Selected", Boolean.parseBoolean(Data));
            Report.updateTestLog(Action, "Checkbox set to [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to set checkbox. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSelectRadioButtonInRow**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

**Description**: Select radio button in table row.

**Input Format**: Row number

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectRadioButtonInRow`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectRadioButtonInRow`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectRadioButtonInRow`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select Radio Button in row [<Data>]", input = InputType.YES)
    public void sapSelectRadioButtonInRow() {
        try {
            Dispatch.put(SAPtable.getAbsoluteRow(Integer.parseInt(Data)), "Selected", true);
            Report.updateTestLog(Action, "Radio button selected in row [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to select radio button. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapSelectTableRow**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

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

------

### **sapSelect**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

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

### **sapSelectMenuItem**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

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

### **sapSelectGridRow**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

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

### **sapSelectContextMenuItem**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v2.4" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">2.4</span></span></a>

**Description**: Select context menu item.

**Input Format**: Menu ID

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapSelectContextMenuItem`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapSelectContextMenuItem`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapSelectContextMenuItem`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Select context menu item [<Data>]", input = InputType.YES)
    public void sapSelectContextMenuItem() {
        try {
            Dispatch.call(SAPelement, "selectContextMenuItem", Data);
            Report.updateTestLog(Action, "Selected context menu item [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to select context menu item. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
