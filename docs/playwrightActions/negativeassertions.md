---
icon: material/flask-empty-minus-outline
---

# Negative Assertions

## **assertElementNotContainsText**

**Description**:  This function will assert if the Element's `text` does not contain the expected text

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementNotContainsText`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementNotContainsText`](#) | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementNotContainsText`](#)   | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] contains the text [<Data>]", input = InputType.YES)
    public void assertElementNotContainsText() {
        String text = "";
        try {
            LocatorAssertions.ContainsTextOptions options = new LocatorAssertions.ContainsTextOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().containsText(Data, options);
            text = Locator.textContent();
            highlightElement();
            Report.updateTestLog(Action, "Element [" + ObjectName + "] dos not contain text '" + Data + "'. Actual text is '" + text + "'", Status.PASS);
            removeHighlightFromElement();
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] does not contain text '" + Data + "'");
        }
    }
    ```
----------------------------------

## **assertElementAttributeNotMatches**

**Description**:  This function will assert if the Element does not have the expected attribute.

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementAttributeNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementAttributeNotMatches`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementAttributeNotMatches`](#)    | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have attribute [<Data>]", input = InputType.YES)
    public void assertElementAttributeNotMatches() {
        String attributeName = Data.split("=")[0];
        String attributeValue = Data.split("=")[1];
        String actualAttributeValue = "";
        try {
            LocatorAssertions.HasAttributeOptions options = new LocatorAssertions.HasAttributeOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().hasAttribute(attributeName, attributeValue, options);
            actualAttributeValue = Locator.getAttribute(attributeName);
            highlightElement();
            Report.updateTestLog(Action, "Element [" + ObjectName + "] does not have attribute '" + attributeName + "' with value '" + attributeValue + "'. Actual value is '" + actualAttributeValue + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementClassNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementClassNotMatches`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementClassNotMatches`](#)   | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have class [<Data>]", input = InputType.YES)
    public void assertElementClassNotMatches() {
        String actualClassValue = "";
        try {
            LocatorAssertions.HasClassOptions options = new LocatorAssertions.HasClassOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().hasClass(Pattern.compile(Data), options);
            actualClassValue = Locator.getAttribute("class");
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] does not have 'class' matching '" + Data + "'. Actual value is '" + actualClassValue + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementCountNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementCountNotMatches`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementCountNotMatches`](#)  | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if count of [<Object>] does not equal [<Data>]", input = InputType.YES)
    public void assertElementCountNotMatches() {
        int elementCount = 0;
        try {
            LocatorAssertions.HasCountOptions options = new LocatorAssertions.HasCountOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().hasCount(Integer.parseInt(Data), options);
            elementCount = Locator.count();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementCSSNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementCSSNotMatches`](#)  | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementCSSNotMatches`](#)   | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have the CSS [<Data>]", input = InputType.YES)
    public void assertElementCSSNotMatches() {
        String attributeName = Data.split("=")[0];
        String attributeValue = Data.split("=")[1];
        String value = "";
        try {
            LocatorAssertions.HasCSSOptions options = new LocatorAssertions.HasCSSOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().hasCSS(attributeName, attributeValue, options);
            value = (String) Locator.evaluate("(element) => window.getComputetStyle(element).getPropertyValue(" + attributeName + ")");
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] does not have CSS attribute '" + attributeName + "' with value '" + attributeValue + "'. Actual value is '" + value + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIdNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIdNotMatches`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIdNotMatches`](#)   | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have ID [<Data>]", input = InputType.YES)
    public void assertElementIdNotMatches() {
        String actualIdValue = "";
        try {
            LocatorAssertions.HasIdOptions options = new LocatorAssertions.HasIdOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().hasId(Pattern.compile(Data), options);
            actualIdValue = Locator.getAttribute("id");
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] does not have 'ID' matching '" + Data + "'. Actual value is '" + actualIdValue + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementJSPropertyNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementJSPropertyNotMatches`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementJSPropertyNotMatches`](#)  | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have JS Property [<Data>]", input = InputType.YES)
    public void assertElementJSPropertyNotMatches() {
        String attributeName = Data.split("=")[0];
        String attributeValue = Data.split("=")[1];
        try {
            LocatorAssertions.HasJSPropertyOptions options = new LocatorAssertions.HasJSPropertyOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().hasJSProperty(attributeName, attributeValue, options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] does not have JS Property attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
            removeHighlightFromElement();
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] has JS Property attribute '" + attributeName + "' with value '" + attributeValue + "'");
        }
    }
    ```
----------------------------------

## **assertElementRoleNotMatches**

**Description**:  This function will assert if the Element's `Role` does not match the expected value

**Input Format** :   @Expected Role

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementRoleNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementRoleNotMatches`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementRoleNotMatches`](#)   | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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

## **assertElementTextNotMatches**

**Description**:  This function will assert if the Element's `text` does not match the expected text

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementTextNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementTextNotMatches`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementTextNotMatches`](#)   | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have text [<Data>]", input = InputType.YES)
    public void assertElementTextNotMatches() {
        String text = "";
        try {
            LocatorAssertions.HasTextOptions options = new LocatorAssertions.HasTextOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().hasText(Pattern.compile(Data), options);
            text = Locator.textContent();
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] does not have text '" + Data + "'. Actual text is '" + text + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementValueNotMatches`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementValueNotMatches`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementValueNotMatches`](#)   | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not value [<Data>]", input = InputType.YES)
    public void assertElementValueNotMatches() {

        String value = "";
        try {
            LocatorAssertions.HasValueOptions options = new LocatorAssertions.HasValueOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().hasValue(Pattern.compile(Data), options);
            value = Locator.getAttribute("value");
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] does not have value '" + Data + "'. Actual value is '" + value + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementValuesNotMatch`](#)   | @value       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementValuesNotMatch`](#)   | Sheet:Column | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementValuesNotMatch`](#)   | %dynamicVar% | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not have values [<Data>]", input = InputType.YES)
    public void assertElementValuesNotMatch() {
        try {
            LocatorAssertions.HasValuesOptions options = new LocatorAssertions.HasValuesOptions();
            options.setTimeout(getTimeoutValue());
            String values[] = Data.split("=");
            Pattern[] pattern = new Pattern[values.length];
            for (int i = 0; i < values.length; i++) {
                pattern[i] = Pattern.compile(values[i]);
            }
            assertThat(Locator).not().hasValues(pattern, options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] does not have values '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotAttached`](#)   |       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotAttached`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotAttached`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

   

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] does not point to an attached DOM node")
    public void assertElementIsNotAttached() {
        try {
            LocatorAssertions.IsAttachedOptions options = new LocatorAssertions.IsAttachedOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isAttached(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotChecked`](#)  |       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotChecked`](#) |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotChecked`](#)  |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not checked")
    public void assertElementIsNotChecked() {
        try {
            LocatorAssertions.IsCheckedOptions options = new LocatorAssertions.IsCheckedOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isChecked(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotDisabled`](#)   |        | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotDisabled`](#)    |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotDisabled`](#)    |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not disabled")
    public void assertElementIsNotDisabled() {
        try {
            LocatorAssertions.IsDisabledOptions options = new LocatorAssertions.IsDisabledOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isDisabled(options);
            Report.updateTestLog(Action, "[" + ObjectName + "] is not disabled", Status.PASS);
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] is disabled");
        }
    }

    ```
----------------------------------

## **assertElementIsNotEditable**

**Description**:  This function will assert if the Element is not editable.

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotEditable`](#)   |     | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotEditable`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotEditable`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not editable")
    public void assertElementIsNotEditable() {
        try {
            LocatorAssertions.IsEditableOptions options = new LocatorAssertions.IsEditableOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isEditable(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotEmpty`](#)  |      | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotEmpty`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotEmpty`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not empty")
    public void assertElementIsNotEmpty() {
        try {
            LocatorAssertions.IsEmptyOptions options = new LocatorAssertions.IsEmptyOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isEmpty(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotEnabled`](#)   |      | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotEnabled`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotEnabled`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

   
=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not enabled")
    public void assertElementIsNotEnabled() {
        try {
            LocatorAssertions.IsEnabledOptions options = new LocatorAssertions.IsEnabledOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isEnabled(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotFocused`](#)   |       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotFocused`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotFocused`](#)   | | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not focused")
     public void assertElementIsNotFocused() {
        try {
            LocatorAssertions.IsFocusedOptions options = new LocatorAssertions.IsFocusedOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isFocused(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotHidden`](#)   |       | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotHidden`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotHidden`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not hidden")
    public void assertElementIsNotHidden() {
        try {
            LocatorAssertions.IsHiddenOptions options = new LocatorAssertions.IsHiddenOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isHidden(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotInViewport`](#)   |        | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotInViewport`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotInViewport`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

   

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not in viewport")
    public void assertElementIsNotInViewport() {
        try {
            LocatorAssertions.IsInViewportOptions options = new LocatorAssertions.IsInViewportOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isInViewport(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsNotVisible`](#)   |        | `optional` timeout in milliseconds       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsNotVisible`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsNotVisible`](#)   |  | `optional` timeout in milliseconds       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is not visible")
    public void assertElementIsNotVisible() {
        try {
            LocatorAssertions.IsVisibleOptions options = new LocatorAssertions.IsVisibleOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).not().isVisible(options);
            Report.updateTestLog(Action, "[" + ObjectName + "] is not visible", Status.PASS);
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] is visible");
        }
    }
    ```
----------------------------------

