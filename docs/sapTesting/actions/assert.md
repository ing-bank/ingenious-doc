---
icon: material/flask-empty-plus-outline
---

# **Assert Actions**

### **sapAssertElementTextContains**
**Since:** <a href="https://github.com/ing-bank/INGenious/releases/tag/v3.0" target="_blank"><span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">3.0</span></span></a>

**Description**: Assert that an element contains the specified text.

**Input Format**: Text value to assert (e.g., `Success`)

=== "Usage"

    | ObjectName | Action   | Input        | Condition | Reference |  |
    |------------|----------|--------------|-----------|-----------|--|
    | SAP        |:green_circle: [`sapAssertElementTextContains`](#) | @value | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>
    | SAP        |:green_circle: [`sapAssertElementTextContains`](#) | Sheet:Column | | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | SAP        |:green_circle: [`sapAssertElementTextContains`](#) | %dynamicVar% | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.SAP, desc = "Assert that [<Object>] contains Text [<Data>]", input = InputType.YES)
    public void sapAssertElementTextContains() {
        try {
            String actual = Dispatch.get(SAPelement, "Text").toString();
            if (actual.contains(Data)) {
                Report.updateTestLog(Action, "Element contains text [" + Data + "]", Status.DONE);
            } else {
                Report.updateTestLog(Action, "Element does not contain text [" + Data + "]", Status.FAIL);
            }
        } catch (Exception e) {
            Report.updateTestLog(Action, "Failed to assert text. Error: " + e.getMessage(), Status.FAILNS);
        }
    }
    ```

---
