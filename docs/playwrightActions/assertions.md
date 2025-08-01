---
icon: material/check-all
---

# Assertions

----------------------------------

## **assertElementContainsText**

**Description**:  This function will assert if the Element's `text` contains the expected text

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementContainsText`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementContainsText`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementContainsText`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] contains the text [<Data>]", input = InputType.YES)
        public void assertElementContainsText() {
            String text = "";
            try {
                text = Locator.textContent();
                assertThat(Locator).containsText(Data);
                Report.updateTestLog(Action, "Element [" + ObjectName + "] contains text '" + Data + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not contain text '" + Data + "'. Actual text is '" + text + "'");
            }
        }
    ```
----------------------------------

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

## **assertElementAttributeMatches**

**Description**:  This function will assert if the Element has the expected attribute.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementAttributeMatches`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementAttributeMatches`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementAttributeMatches`](#) | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has the attribute [<Data>]", input = InputType.YES)
        public void assertElementAttributeMatches() {
            String attributeName = Data.split(",")[0];
            String attributeValue = Data.split(",")[1];
            String actualattributeValue = "";
            try {
                actualattributeValue = Locator.getAttribute(attributeName);
                assertThat(Locator).hasAttribute(attributeName, attributeValue);
                Report.updateTestLog(Action, "Element [" + ObjectName + "] has attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not have attribute '" + attributeName + " = " + attributeValue + "'. Actual value is '" + actualattributeValue + "'");
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

## **assertElementClassMatches**

**Description**:  This function will assert if the Element match the expected class

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementClassMatches`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementClassMatches`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementClassMatches`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has class [<Data>]", input = InputType.YES)
        public void assertElementClassMatches() {
            String actualClassValue = "";
            try {
                actualClassValue = Locator.getAttribute("class");
                assertThat(Locator).hasClass(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] has 'class' matching '" + Data + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not have 'class' matching '" + Data + "'. Actual value is '" + actualClassValue + "'");
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

## **assertElementCountMatches**

**Description**:  This function will assert if the count of Element matches the expected count

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementCountMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementCountMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementCountMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if count of [<Object>] matches [<Data>]", input = InputType.YES)
        public void assertElementCountMatches() {
            int elementCount = 0;
            try {
                elementCount = Locator.count();
                assertThat(Locator).hasCount(Integer.parseInt(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] count matches '" + Data + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] count does not match '" + Data + "'. Actual count is +'" + elementCount + "'");
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

## **assertElementCSSMatches**

**Description**:  This function will assert if the Element has the expected CSS attribute

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementCSSMatches`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementCSSMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementCSSMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has the CSS [<Data>]", input = InputType.YES)
        public void assertElementCSSMatches() {
            String attributeName = Data.split(",")[0];
            String attributeValue = Data.split(",")[1];
            try {
                assertThat(Locator).hasCSS(attributeName, attributeValue);
                Report.updateTestLog(Action, "[" + ObjectName + "] has CSS attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not have CSS attribute '" + attributeName + "' with value '" + attributeValue + "'");
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

## **assertElementIdMatches**

**Description**:  This function will assert if the Element has the expected ID

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIdMatches`](#) | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIdMatches`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIdMatches`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has ID [<Data>]", input = InputType.YES)
        public void assertElementIdMatches() {
            String actualIdValue = "";
            try {
                actualIdValue = Locator.getAttribute("id");
                assertThat(Locator).hasId(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] has 'ID' matching '" + Data + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not have 'ID' matching '" + Data + "'. Actual value is '" + actualIdValue + "'");
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

## **assertElementJSPropertyMatches**

**Description**:  This function will assert if the Element has the expected JS Property attribute

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementJSPropertyMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementJSPropertyMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementJSPropertyMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has JS Property [<Data>]", input = InputType.YES)
        public void assertElementJSPropertyMatches() {
            String attributeName = Data.split(",")[0];
            String attributeValue = Data.split(",")[1];
            try {
                assertThat(Locator).hasJSProperty(attributeName, attributeValue);
                Report.updateTestLog(Action, "[" + ObjectName + "] has JS Property attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not have JS Property attribute '" + attributeName + "' with value '" + attributeValue + "'");
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

## **assertElementTextMatches**

**Description**:  This function will assert if the Element's `text` matches the expected text

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementTextMatches`](#) | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementTextMatches`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementTextMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has text [<Data>]", input = InputType.YES)
        public void assertElementTextMatches() {
            String text = "";
            try {
                text = Locator.textContent();
                assertThat(Locator).hasText(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] has text '" + Data + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not have text '" + Data + "'. Actual text is '" + text + "'");
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

## **assertElementValueMatches**

**Description**:  This function will assert if the Element's `value` contains the expected value.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementValueMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementValueMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementValueMatches`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has value [<Data>]", input = InputType.YES)
        public void assertElementValueMatches() {

            String value = "";
            try {
                value = Locator.getAttribute("value");
                assertThat(Locator).hasValue(Pattern.compile(Data));
                Report.updateTestLog(Action, "[" + ObjectName + "] has value '" + Data + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not have value '" + Data + "'. Actual value is '" + value + "'");
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

## **assertElementValuesMatch**

**Description**:  This function will assert if the Element's `values` contains the expected values

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementValuesMatch`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementValuesMatch`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementValuesMatch`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has values [<Data>]", input = InputType.YES)
        public void assertElementValuesMatch() {
            try {
                String values[] = Data.split(",");
                Pattern[] pattern = new Pattern[values.length];
                for (int i = 0; i < values.length; i++) {
                    pattern[i] = Pattern.compile(values[i]);
                }
                assertThat(Locator).hasValues(pattern);
                Report.updateTestLog(Action, "[" + ObjectName + "] has values '" + Data + "'", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] does not have values '" + Data + "'");
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

## **assertElementIsAttached**

**Description**:  This function will assert if the Element is attached to the DOM

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsAttached`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsAttached`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsAttached`](#) | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] points to an attached DOM node")
        public void assertElementIsAttached() {
            try {
                assertThat(Locator).isAttached();
                Report.updateTestLog(Action, "[" + ObjectName + "] is attached to the DOM", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not attached to the DOM");
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

## **assertElementIsChecked**

**Description**:  This function will assert if the Element is checked.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsChecked`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsChecked`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsChecked`](#)  | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is checked")
        public void assertElementIsChecked() {
            try {
                assertThat(Locator).isChecked();
                Report.updateTestLog(Action, "[" + ObjectName + "] is checked", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not checked");
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

## **assertElementIsDisabled**

**Description**:  This function will assert if the Element is disabled.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsDisabled`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsDisabled`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsDisabled`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is disabled")
        public void assertElementIsDisabled() {
            try {
                assertThat(Locator).isDisabled();
                Report.updateTestLog(Action, "[" + ObjectName + "] is disabled", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not disabled");
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

## **assertElementIsEditable**

**Description**:  This function will assert if the Element is editable.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsEditable`](#)    | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsEditable`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsEditable`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is editable")
        public void assertElementIsEditable() {
            try {
                assertThat(Locator).isEditable();
                Report.updateTestLog(Action, "[" + ObjectName + "] is editable", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not editable");
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

## **assertElementIsEmpty**

**Description**:  This function will assert if the Element is empty.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsEmpty`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsEmpty`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsEmpty`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is empty")
        public void assertElementIsEmpty() {
            try {
                assertThat(Locator).isEmpty();
                Report.updateTestLog(Action, "[" + ObjectName + "] is empty", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not empty");
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

## **assertElementIsEnabled**

**Description**:  This function will assert if the Element is enabled.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsEnabled`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsEnabled`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsEnabled`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is enabled")
        public void assertElementIsEnabled() {
            try {
                assertThat(Locator).isEnabled();
                Report.updateTestLog(Action, "[" + ObjectName + "] is enabled", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not enabled");
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

## **assertElementIsFocused**

**Description**:  This function will assert if the Element is focused.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsFocused`](#)  | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsFocused`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsFocused`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is focused")
        public void assertElementIsFocused() {
            try {
                assertThat(Locator).isFocused();
                Report.updateTestLog(Action, "[" + ObjectName + "] is focused", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not focused");
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

## **assertElementIsHidden**

**Description**:  This function will assert if the Element is hidden.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsHidden`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsHidden`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsHidden`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is hidden")
        public void assertElementIsHidden() {
            try {
                assertThat(Locator).isHidden();
                Report.updateTestLog(Action, "[" + ObjectName + "] is hidden", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not hidden");
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

## **assertElementIsInViewport**

**Description**:  This function will assert if the Element is in viewport.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsInViewport`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsInViewport`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsInViewport`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is in viewport")
        public void assertElementIsInViewport() {
            try {
                assertThat(Locator).isInViewport();
                Report.updateTestLog(Action, "[" + ObjectName + "] is in viewport", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not in viewport");
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

## **assertElementIsVisible**

**Description**:  This function will assert if the Element is visible.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertElementIsVisible`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertElementIsVisible`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertElementIsVisible`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is visible")
        public void assertElementIsVisible() {
            try {
                assertThat(Locator).isVisible();
                Report.updateTestLog(Action, "[" + ObjectName + "] is visible", Status.PASS);
            } catch (PlaywrightException e) {
                PlaywrightExceptionLogging(e);
            } catch (AssertionFailedError err) {
                assertionLogging(err, "[" + ObjectName + "] is not visible");
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

## **assertPageTitleMatches**

**Description**:  This function will assert the Page Title.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertPageTitleMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertPageTitleMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertPageTitleMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Assert if Page has title [<Data>]", input = InputType.YES)
        public void assertPageTitleMatches() {

            try {
                assertThat(Page).hasTitle(Pattern.compile(Data));
                Report.updateTestLog(Action, "Page has title matching '" + Data + "'", Status.PASS);
            } catch (AssertionFailedError e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Assertion Failed", "Page does not have title matching '" + Data + "'", Status.FAIL);
            }
        }
    ```
----------------------------------

## **assertPageURLMatches**

**Description**:  This function will assert the Page URL.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertPageURLMatches`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertPageURLMatches`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertPageURLMatches`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Assert if Page has URL [<Data>]", input = InputType.YES)
        public void assertPageURLMatches() {

            try {
                assertThat(Page).hasURL(Pattern.compile(Data));
                Report.updateTestLog(Action, "Page has URL matching '" + Data + "'", Status.PASS);
            } catch (AssertionFailedError e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Assertion Failed", "Page does not have URL matching '" + Data + "'", Status.FAIL);
            }
        }
    ```
----------------------------------

