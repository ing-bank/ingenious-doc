---
icon: material/flask-empty-plus-outline
---

# Positive Assertions

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

## **assertVariable**

**Description**:  This function will assert if the variable value matched with provided data.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertVariable`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertVariable`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertVariable`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER,desc = "Assert if Key:Value -> [<Data>] is valid",input = InputType.YES)
        public void assertVariable() throws RuntimeException {
            try {
                String strObj = Data;
                String[] strTemp = strObj.split("=", 2);
                String strAns = strTemp[0].matches("%.+%") ? getVar(strTemp[0]) : strTemp[0];
                if (strAns.equals(strTemp[1])) {
                    System.out.println("Condition '" + Input + "' is true ");
                    Report.updateTestLog("assertVariable",
                            "Variable matched with Provided data", Status.PASS);

                } else {
                    System.out.println("Condition '" + Input + "' is false ");
                    throw new Exception("Variable did not match with provided data");
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, null, ex);
                throw new ForcedException("assertVariable", ex.getMessage());
            }
        }
    ```
----------------------------------

## **assertVariableFromDataSheet**

**Description**:  This function will assert if the variable value matches with given value from datasheet.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`assertVariableFromDataSheet`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`assertVariableFromDataSheet`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`assertVariableFromDataSheet`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.BROWSER,desc = "Assert if  the  variable value matches with given value from datasheet(variable:datasheet->  [<Data>] )", input = InputType.YES, condition = InputType.YES)
        public void assertVariableFromDataSheet() throws RuntimeException {
            try {
                String strAns = getVar(Condition);
                if (strAns.equals(Data)) {
                    System.out.println("Variable " + Condition + " equals "
                            + Input);
                    Report.updateTestLog(Action,
                            "Variable is matched with the expected result", Status.DONE);

                } else {
                    System.out.println("Variable " + Condition + " is not equal "
                            + Input);
                    throw new ForcedException(Action,
                            "Variable did not match with provided data");
                }
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, null, e);
                throw new ForcedException("assertVariableFromDataSheet", e.getMessage());
            }
        }
    ```