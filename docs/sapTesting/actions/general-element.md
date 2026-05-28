---
icon: octicons/browser-16
---

# **General Element Actions**

### **sapFill**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

**Description**: Enter the value in the field.

**Input Format**: Value to enter (e.g., `Test123`)

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapFill`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapFill`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapFill`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Enter the value [<Data>] in the field [<Object>]", input = InputType.YES)
    public void sapFill() {
        try {
            Dispatch.put(SAPelement, "Text", Data);
            Report.updateTestLog(Action, "Entered value [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to enter value. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapEnter**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

**Description**: Press Enter key in the field.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapEnter`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Press [<Enter>] key", input = InputType.NO)
    public void sapEnter() {
        try {
            Dispatch.call(SAPelement, "sendVKey", 0);
            Report.updateTestLog(Action, "Pressed Enter key", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to press Enter. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapClick**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

**Description**: Click/Press button.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapClick`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Click the [<Object>]")
    public void sapClick() {
        try {
            Dispatch.call(SAPelement, "press");
            Report.updateTestLog(Action, "Button clicked", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to click button. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapDoubleClick**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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

### **sapPressButton**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

**Description**: Press button by ID or function code.

**Input Format**: Button ID or function code (e.g., `SAVE`)

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapPressButton`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapPressButton`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapPressButton`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Press button with ID [<Data>]", input = InputType.YES)
    public void sapPressButton() {
        try {
            Dispatch.call(SAPtoolbar, "pressButton", Data);
            Report.updateTestLog(Action, "Pressed button with ID [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to press button. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---


### **sapSetFocus**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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

### **sapMaximizeWindow**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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

### **sapExpandTreeNode**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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

### **sapGetStatusBarText**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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

------

### **sapPressContextButton**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>


**Description**: Press context button with parameter.

**Input Format**: Button ID

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapPressContextButton`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapPressContextButton`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapPressContextButton`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Press context button with parameter [<Data>]", input = InputType.YES)
    public void sapPressContextButton() {
        try {
            Dispatch.call(SAPelement, "pressContextButton", Data);
            Report.updateTestLog(Action, "Pressed context button [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to press context button. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapOpenComboBox**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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
