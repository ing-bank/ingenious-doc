# **Assert Actions**
------------------------

This section documents SAP assert actions for SAP GUI automation in INGenious.

---

### **sapAssertElementTextContains**
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
