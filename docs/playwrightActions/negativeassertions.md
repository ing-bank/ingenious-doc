---
icon: material/flask-empty-minus-outline
---

# Negative Assertions

## **assertElementNotContainsText**

**Description**:  This function will assert if the Element's `text` does not contain the expected text

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementNotContainsText`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementNotContainsText`](#) | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementNotContainsText`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not contain text [<Data>]", input = InputType.YES)
        public void assertElementNotContainsText() {
            String text = "";
            try {
                text = Locator.textContent();
                assertThat(Locator).not().containsText(Data);
                Report.updateTestLog(Action, "Element [" + ObjectName + "] does not contain text '" + Data + "'. Actual text is '" + text + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] contains text '" + Data + "'");
            }
        }
    ```
----------------------------------

## **assertElementAttributeNotMatches**

**Description**:  This function will assert if the Element does not have the expected attribute.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementAttributeNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementAttributeNotMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementAttributeNotMatches`](#)    | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have attribute [<Data>]", input = InputType.YES)
        public void assertElementAttributeNotMatches() {
            String attributeName = Data.split(",")[0];
            String attributeValue = Data.split(",")[1];
            String actualAttributeValue = "";
            try {
                actualAttributeValue = Locator.getAttribute(attributeName);
                assertThat(Locator).not().hasAttribute(attributeName, attributeValue);
                Report.updateTestLog(Action, "Element [" + ObjectName + "] does not have attribute '" + attributeName + "' with value '" + attributeValue + "'. Actual value is '" + actualAttributeValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has attribute '" + attributeName + " = " + actualAttributeValue + "'");
            }
        }
    ```
----------------------------------
## **assertElementClassNotMatches**

**Description**:  This function will assert if the Element does not match the expected class.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementClassNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementClassNotMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementClassNotMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have class [<Data>]", input = InputType.YES)
        public void assertElementClassNotMatches() {
            String actualClassValue = "";
            try {
                actualClassValue = Locator.getAttribute("class");
                assertThat(Locator).not().hasClass(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] does not have 'class' matching '" + Data + "'. Actual value is '" + actualClassValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has 'class' matching '" + Data + "'");
            }
        }
    ```
----------------------------------

## **assertElementCountNotMatches**

**Description**:  This function will assert if the count of Element does not match the expected count

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementCountNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementCountNotMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementCountNotMatches`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if count of [<Object>] does not match [<Data>]", input = InputType.YES)
        public void assertElementCountNotMatches() {
            int elementCount = 0;
            try {
                elementCount = Locator.count();
                assertThat(Locator).not().hasCount(Integer.parseInt(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] count does not match '" + Data + "'. Actual count is +'" + elementCount + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] count matches '" + Data + "'");
            }
        }
    ```
----------------------------------

## **assertElementCSSNotMatches**

**Description**:  This function will assert if the Element does not have the expected CSS attribute

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementCSSNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementCSSNotMatches`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementCSSNotMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have the CSS [<Data>]", input = InputType.YES)
        public void assertElementCSSNotMatches() {
            String attributeName = Data.split(",")[0];
            String attributeValue = Data.split(",")[1];
            try {
                assertThat(Locator).not().hasCSS(attributeName, attributeValue);
                Report.updateTestLog(Action, "[" + ObjectName + "] does not have CSS attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has CSS attribute '" + attributeName + "' with value '" + attributeValue + "'");
            }
        }
    ```
----------------------------------

## **assertElementIdNotMatches**

**Description**:  This function will assert if the Element does not have the expected ID

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIdNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIdNotMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIdNotMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have ID [<Data>]", input = InputType.YES)
        public void assertElementIdNotMatches() {
            String actualIdValue = "";
            try {
                actualIdValue = Locator.getAttribute("id");
                assertThat(Locator).not().hasId(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] does not have 'ID' matching '" + Data + "'. Actual value is '" + actualIdValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has 'ID' matching '" + Data + "'");
            }
        }
    ```
----------------------------------

## **assertElementJSPropertyNotMatches**

**Description**:  This function will assert if the Element does not have the expected JS Property attribute

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementJSPropertyNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementJSPropertyNotMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementJSPropertyNotMatches`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have JS Property [<Data>]", input = InputType.YES)
        public void assertElementJSPropertyNotMatches() {
            String attributeName = Data.split(",")[0];
            String attributeValue = Data.split(",")[1];
            try {
                assertThat(Locator).not().hasJSProperty(attributeName, attributeValue);
                Report.updateTestLog(Action, "[" + ObjectName + "] does not have JS Property attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has JS Property attribute '" + attributeName + "' with value '" + attributeValue + "'");
            }
        }
    ```
----------------------------------


## **assertElementTextNotMatches**

**Description**:  This function will assert if the Element's `text` does not match the expected text

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementTextNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementTextNotMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementTextNotMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have text [<Data>]", input = InputType.YES)
        public void assertElementTextNotMatches() {
            String text = "";
            try {
                text = Locator.textContent();
                assertThat(Locator).not().hasText(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] does not have text '" + Data + "'. Actual text is '" + text + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has text '" + Data + "'");
            }
        }
    ```
----------------------------------

## **assertElementValueNotMatches**

**Description**:  This function will assert if the Element's `value` does not match the expected value

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementValueNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementValueNotMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementValueNotMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not value [<Data>]", input = InputType.YES)
        public void assertElementValueNotMatches() {

            String value = "";
            try {
                value = Locator.getAttribute("value");
                assertThat(Locator).not().hasValue(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] does not have value '" + Data + "'. Actual value is '" + value + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has value '" + Data + "'");
            }
        }
    ```
----------------------------------

## **assertElementValuesNotMatch**

**Description**:  This function will assert if the Element's `values` does not match the expected values

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementValuesNotMatch`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementValuesNotMatch`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementValuesNotMatch`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have values [<Data>]", input = InputType.YES)
        public void assertElementValuesNotMatch() {
            try {
                String values[] = Data.split(",");
                Pattern[] pattern = new Pattern[values.length];
                for (int i = 0; i < values.length; i++) {
                    pattern[i] = Pattern.compile(values[i]);
                }
                assertThat(Locator).not().hasValues(pattern);
                Report.updateTestLog(Action, "[" + ObjectName + "] does not have values '" + Data + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has values '" + Data + "'");
            }
        }
    ```
----------------------------------

## **assertElementIsNotAttached**

**Description**:  This function will assert if the Element is not attached to the DOM

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotAttached`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotAttached`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotAttached`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not point to an attached DOM node")
        public void assertElementIsNotAttached() {
            try {
                assertThat(Locator).not().isAttached();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not attached to the DOM", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is attached to the DOM");
            }
        }
    ```
----------------------------------

## **assertElementIsNotChecked**

**Description**:  This function will assert if the Element is not checked.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotChecked`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotChecked`](#) | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotChecked`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not checked")
        public void assertElementIsNotChecked() {
            try {
                assertThat(Locator).not().isChecked();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not checked", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is checked");
            }
        }
    ```
----------------------------------
## **assertElementIsNotDisabled**

**Description**:  This function will assert if the Element is not disabled.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotDisabled`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotDisabled`](#)    | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotDisabled`](#)    | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not disabled")
        public void assertElementIsNotDisabled() {
            try {
                assertThat(Locator).not().isDisabled();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not disabled", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is disabled");
            }
        }
    ```
----------------------------------

## **assertElementIdNotMatches**

**Description**:  This function will assert if the Element does not have the expected ID

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIdNotMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIdNotMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIdNotMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have ID [<Data>]", input = InputType.YES)
        public void assertElementIdNotMatches() {
            String actualIdValue = "";
            try {
                actualIdValue = Locator.getAttribute("id");
                assertThat(Locator).not().hasId(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] does not have 'ID' matching '" + Data + "'. Actual value is '" + actualIdValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] has 'ID' matching '" + Data + "'");
            }
        }
    ```
----------------------------------

## **assertElementIsNotEditable**

**Description**:  This function will assert if the Element is not editable.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotEditable`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotEditable`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotEditable`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not editable")
        public void assertElementIsNotEditable() {
            try {
                assertThat(Locator).not().isEditable();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not editable", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is editable");
            }
        }
    ```
----------------------------------
## **assertElementIsNotEmpty**

**Description**:  This function will assert if the Element is not empty.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotEmpty`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotEmpty`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotEmpty`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not empty")
        public void assertElementIsNotEmpty() {
            try {
                assertThat(Locator).not().isEmpty();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not empty", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is empty");
            }
        }
    ```
----------------------------------
## **assertElementIsNotEnabled**

**Description**:  This function will assert if the Element is not enabled.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotEnabled`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotEnabled`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotEnabled`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not enabled")
        public void assertElementIsNotEnabled() {
            try {
                assertThat(Locator).not().isEnabled();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not enabled", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is enabled");
            }
        }
    ```
----------------------------------

## **assertElementIsNotFocused**

**Description**:  This function will assert if the Element is not focused.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotFocused`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotFocused`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotFocused`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not focused")
        public void assertElementIsNotFocused() {
            try {
                assertThat(Locator).not().isFocused();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not focused", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is focused");
            }
        }
    ```
----------------------------------

## **assertElementIsNotHidden**

**Description**:  This function will assert if the Element is not hidden.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotHidden`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotHidden`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotHidden`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not hidden")
        public void assertElementIsNotHidden() {
            try {
                assertThat(Locator).not().isHidden();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not hidden", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is hidden");
            }
        }
    ```
----------------------------------

## **assertElementIsNotInViewport**

**Description**:  This function will assert if the Element is not in viewport.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotInViewport`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotInViewport`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotInViewport`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not in viewport")
        public void assertElementIsNotInViewport() {
            try {
                assertThat(Locator).not().isInViewport();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not in viewport", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is in viewport");
            }
        }
    ```
----------------------------------


## **assertElementIsNotVisible**

**Description**:  This function will assert if the Element is not visible.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsNotVisible`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsNotVisible`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsNotVisible`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not visible")
        public void assertElementIsNotVisible() {
            try {
                assertThat(Locator).not().isVisible();
                Report.updateTestLog(Action, "[" + ObjectName + "] is not visible", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is visible");
            }
        }
    ```
----------------------------------

