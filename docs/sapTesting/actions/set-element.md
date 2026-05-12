---
icon: material/text
---

# **General Element Set Actions**

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

### **sapSetObjectProperty**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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
			if (Condition.isEmpty()) {
				String[] groups = Data.split(",");
				for (String group : groups) {
					String[] vals = group.split("=", 2);
					setProperty(vals[0], vals[1]);
				}
			} else {
				setProperty(Condition, Data);
			}
			String text = String.format("Setting Object Property for [%s] with [%s] for Object [%s - %s]", Condition, Data,
					Reference, ObjectName);
			Report.updateTestLog(Action, text, Status.DONE);
		} else {
			Report.updateTestLog(Action, "Input should not be empty", Status.FAILNS);
		}
	}
    ```
    
---

### **sapSetCurrentCell**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

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
