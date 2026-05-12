---
icon: octicons/browser-16
---

# **Session & Transaction Management**

### **sapExecuteTransaction**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

**Description**: Execute an SAP transaction code (e.g., `VA01`, `ME23N`).

**Input Format**: Transaction code (e.g., `VA01`)

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | Browser    |:green_circle: [`sapExecuteTransaction`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | Browser    |:green_circle: [`sapExecuteTransaction`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser    |:green_circle: [`sapExecuteTransaction`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Execute SAP transaction [<Data>]", input = InputType.YES)
    public void sapExecuteTransaction() {
        try {
            Dispatch.call(SAPsession, "startTransaction", Data);
            Report.updateTestLog(Action, "Executed transaction [" + Data + "]", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to execute transaction. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapEndTransaction**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

**Description**: End the current SAP transaction.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | Browser    |:green_circle: [`sapEndTransaction`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "End current SAP transaction", input = InputType.NO)
    public void sapEndTransaction() {
        try {
            Dispatch.call(SAPsession, "endTransaction");
            Report.updateTestLog(Action, "Ended current transaction successfully", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to end transaction. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---

### **sapRefreshSession**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

**Description**: Refresh the SAP session.

**Input Format**: None

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | Browser    |:green_circle: [`sapRefreshSession`](#) |  | | |<span style="color:#349651">:arrow_left:   *No Input*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Refresh SAP session", input = InputType.NO)
    public void sapRefreshSession() {
        try {
            Dispatch.call(SAPsession, "Refresh");
            Report.updateTestLog(Action, "SAP session refreshed", Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to refresh session. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
