---
icon: material/flask-empty-plus-outline
---

# Positive Assertions

## **assertElementContainsText**

**Description**:  This function will assert if the Element's `text` contains the expected text

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementContainsText`](#)  | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementContainsText`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementContainsText`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] contains the text [<Data>]", input = InputType.YES)
    public void assertElementContainsText() {
        String text = "";
        try {
            LocatorAssertions.ContainsTextOptions options = new LocatorAssertions.ContainsTextOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).containsText(Data,options);
            text = Locator.textContent();
            highlightElement();
            Report.updateTestLog(Action, "Element [" + ObjectName + "] contains text '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] does not contain text '" + Data + "'. Actual text is '" + text + "'");
        }
    }
    ```
----------------------------------

## **assertElementContainsTextIgnoreCase**

**Description**:  This function will assert if the Element's `text` contains the expected text (case insensitive)

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementContainsTextIgnoreCase`](#)  | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementContainsTextIgnoreCase`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementContainsTextIgnoreCase`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] contains the text [<Data>]", input = InputType.YES)
    public void assertElementContainsTextIgnoreCase() {
        String text = "";
        try {
            LocatorAssertions.ContainsTextOptions options = new LocatorAssertions.ContainsTextOptions();
            options.setTimeout(getTimeoutValue());
            options.setIgnoreCase(true);
            assertThat(Locator).containsText(Data,options);
            text = Locator.textContent();
            highlightElement();
            Report.updateTestLog(Action, "Element [" + ObjectName + "] contains text '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] does not contain text '" + Data + "'. Actual text is '" + text + "'");
        }
    }
    ```
----------------------------------

## **assertElementHasAccessibleDescription**

**Description**:  This function will assert if the Element has an Accessible Description

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementHasAccessibleDescription`](#)  | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementHasAccessibleDescription`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementHasAccessibleDescription`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has Accessible Description [<Data>]", input = InputType.YES)
    public void assertElementHasAccessibleDescription() {

        try {
            LocatorAssertions.HasAccessibleDescriptionOptions options = new LocatorAssertions.HasAccessibleDescriptionOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).hasAccessibleDescription(Data,options);
            highlightElement();
            Report.updateTestLog(Action, "Element [" + ObjectName + "] has Accessible Description '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] does not contain expected Accessible Description");
        }
    }
    ```
----------------------------------

## **assertElementHasAccessibleName**

**Description**:  This function will assert if the Element has an Accessible Name

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementHasAccessibleName`](#)  | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementHasAccessibleName`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementHasAccessibleName`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has Accessible Name [<Data>]", input = InputType.YES)
    public void assertElementHasAccessibleName() {

        try {
            LocatorAssertions.HasAccessibleNameOptions options = new LocatorAssertions.HasAccessibleNameOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).hasAccessibleName(Data,options);
            highlightElement();
            Report.updateTestLog(Action, "Element [" + ObjectName + "] has Accessible Name '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] does not contain expected Accessible Name");
        }
    }
    ```
----------------------------------

## **assertElementAttributeMatches**

**Description**:  This function will assert if the Element has the expected attribute.

**Input Format** :   `AttributeName=AttributeValue`

**Condition Format** : (Optional)  Timeout Value (in ms)


=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementAttributeMatches`](#)  | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementAttributeMatches`](#)  | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementAttributeMatches`](#) | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has the attribute [<Data>]", input = InputType.YES)
    public void assertElementAttributeMatches() {
        String attributeName = Data.split("=")[0];
        String attributeValue = Data.split("=")[1];
        String actualattributeValue = "";
        try {
            LocatorAssertions.HasAttributeOptions options = new LocatorAssertions.HasAttributeOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).hasAttribute(attributeName, attributeValue,options);
            actualattributeValue = Locator.getAttribute(attributeName);
            highlightElement();
            Report.updateTestLog(Action, "Element [" + ObjectName + "] has attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementClassMatches`](#)  | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementClassMatches`](#)  | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementClassMatches`](#)  | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has class [<Data>]", input = InputType.YES)
    public void assertElementClassMatches() {
        String actualClassValue = "";
        try {
            LocatorAssertions.HasClassOptions options = new LocatorAssertions.HasClassOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).hasClass(Pattern.compile(Data),options);
            actualClassValue = Locator.getAttribute("class");
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] has 'class' matching '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementCountMatches`](#)   | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementCountMatches`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementCountMatches`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"


    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if count of [<Object>] equals [<Data>]", input = InputType.YES)
    public void assertElementCountMatches() {
        int elementCount = 0;
        try {
            LocatorAssertions.HasCountOptions options = new LocatorAssertions.HasCountOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).hasCount(Integer.parseInt(Data),options);
            elementCount = Locator.count();
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

**Input Format** :   `CSS Name=CSS Value`

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementCSSMatches`](#)  | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementCSSMatches`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementCSSMatches`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has the CSS [<Data>]", input = InputType.YES)
    public void assertElementCSSMatches() {
        String attributeName = Data.split("=",2)[0];
        String attributeValue = Data.split("=",2)[1];
        String value = "";
        try {
            LocatorAssertions.HasCSSOptions options = new LocatorAssertions.HasCSSOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).hasCSS(attributeName, attributeValue, options);
            value = (String) Locator.evaluate("(element) => window.getComputetStyle(element).getPropertyValue("+attributeName+")");
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] has CSS attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
            removeHighlightFromElement();
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] does not have CSS attribute '" + attributeName + "' with value '" + attributeValue + "'. Actual value is '"+value+"'");
        }
    }

    ```
----------------------------------

## **assertElementIdMatches**

**Description**:  This function will assert if the Element has the expected ID

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIdMatches`](#) | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIdMatches`](#)  | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIdMatches`](#)  | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has ID [<Data>]", input = InputType.YES)
    public void assertElementIdMatches() {
        String actualIdValue = "";
        try {
            LocatorAssertions.HasIdOptions options = new LocatorAssertions.HasIdOptions();
            options.setTimeout(getTimeoutValue());         
            assertThat(Locator).hasId(Pattern.compile(Data),options);
            actualIdValue = Locator.getAttribute("id");
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] has 'ID' matching '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementJSPropertyMatches`](#)   | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementJSPropertyMatches`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementJSPropertyMatches`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has JS Property [<Data>]", input = InputType.YES)
            public void assertElementJSPropertyMatches() {
                String attributeName = Data.split("=")[0];
                String attributeValue = Data.split("=")[1];
                try {
                    LocatorAssertions.HasJSPropertyOptions options = new LocatorAssertions.HasJSPropertyOptions();
                    options.setTimeout(getTimeoutValue());        
                    assertThat(Locator).hasJSProperty(attributeName, attributeValue, options);
                    highlightElement();
                    Report.updateTestLog(Action, "[" + ObjectName + "] has JS Property attribute '" + attributeName + "' with value '" + attributeValue + "'", Status.PASS);
                    removeHighlightFromElement();
                } catch (PlaywrightException e) {
                    PlaywrightExceptionLogging(e);
                } catch (AssertionFailedError err) {
                    assertionLogging(err, "[" + ObjectName + "] does not have JS Property attribute '" + attributeName + "' with value '" + attributeValue + "'");
                }
            }
    ```
----------------------------------

## **assertElementRoleMatches**

**Description**:  This function will assert if the Element's `Role` matches the expected value

**Input Format** :   @Expected Role Value

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementRoleMatches`](#) | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementRoleMatches`](#)  | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementRoleMatches`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has Role [<Data>]", input = InputType.YES)
    public void assertElementRoleMatches() {
        String actualIdValue = "";
        try {
            LocatorAssertions.HasRoleOptions options = new LocatorAssertions.HasRoleOptions();
            options.setTimeout(getTimeoutValue());         
            assertThat(Locator).hasRole(AriaRole.valueOf(Data.toUpperCase()),options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] has 'Role' matching '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
        } catch (PlaywrightException e) {
            PlaywrightExceptionLogging(e);
        } catch (AssertionFailedError err) {
            assertionLogging(err, "[" + ObjectName + "] does not have 'Role' matching '" + Data + "'. Actual value is '" + actualIdValue + "'");
        }
    }
    ```
----------------------------------
## **assertElementTextMatches**

**Description**:  This function will assert if the Element's `text` matches the expected text

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementTextMatches`](#) | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementTextMatches`](#)  | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementTextMatches`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has text [<Data>]", input = InputType.YES)
    public void assertElementTextMatches() {
        String text = "";
        try {
            LocatorAssertions.HasTextOptions options = new LocatorAssertions.HasTextOptions();
            options.setTimeout(getTimeoutValue());      
            assertThat(Locator).hasText(Pattern.compile(Data),options);
            text = Locator.textContent();
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] has text '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementValueMatches`](#)   | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementValueMatches`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementValueMatches`](#)  | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has value [<Data>]", input = InputType.YES)
    public void assertElementValueMatches() {

        String value = "";
        try {
            LocatorAssertions.HasValueOptions options = new LocatorAssertions.HasValueOptions();
            options.setTimeout(getTimeoutValue());      
            assertThat(Locator).hasValue(Pattern.compile(Data),options);
            value = Locator.getAttribute("value");
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] has value '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementValuesMatch`](#)   | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementValuesMatch`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementValuesMatch`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] has values [<Data>]", input = InputType.YES)
    public void assertElementValuesMatch() {
        try {
            LocatorAssertions.HasValuesOptions options = new LocatorAssertions.HasValuesOptions();
            options.setTimeout(getTimeoutValue()); 
            String values[] = Data.split("=");
            Pattern[] pattern = new Pattern[values.length];
            for (int i = 0; i < values.length; i++) {
                pattern[i] = Pattern.compile(values[i]);
            }
            assertThat(Locator).hasValues(pattern,options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] has values '" + Data + "'", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsAttached`](#)   |       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsAttached`](#)   |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsAttached`](#) |  |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] points to an attached DOM node")
    public void assertElementIsAttached() {
        try {
            LocatorAssertions.IsAttachedOptions options = new LocatorAssertions.IsAttachedOptions();
            options.setTimeout(getTimeoutValue()); 
            assertThat(Locator).isAttached(options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] is attached to the DOM", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsChecked`](#)   |        | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsChecked`](#)   |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsChecked`](#)  |  |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is checked")
    public void assertElementIsChecked() {
        try {
            LocatorAssertions.IsCheckedOptions options = new LocatorAssertions.IsCheckedOptions();
            options.setTimeout(getTimeoutValue()); 
            assertThat(Locator).isChecked(options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] is checked", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsDisabled`](#)   |        | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsDisabled`](#)  |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsDisabled`](#)   | |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is disabled")
    public void assertElementIsDisabled() {
        try {
            LocatorAssertions.IsDisabledOptions options = new LocatorAssertions.IsDisabledOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).isDisabled(options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] is disabled", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsEditable`](#)    |        | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsEditable`](#)   |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsEditable`](#)   |  |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>



=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is editable")
    public void assertElementIsEditable() {
        try {
            LocatorAssertions.IsEditableOptions options = new LocatorAssertions.IsEditableOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).isEditable(options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] is editable", Status.PASS);
            removeHighlightFromElement();
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


**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsEmpty`](#)   |      | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsEmpty`](#)   |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsEmpty`](#)   | |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is empty")
    public void assertElementIsEmpty() {
        try {
            LocatorAssertions.IsEmptyOptions options = new LocatorAssertions.IsEmptyOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).isEmpty(options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] is empty", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsEnabled`](#)   |        | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsEnabled`](#)  |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsEnabled`](#)   |  |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is enabled")
    public void assertElementIsEnabled() {
        try {
            LocatorAssertions.IsEnabledOptions options = new LocatorAssertions.IsEnabledOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).isEnabled(options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] is enabled", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsFocused`](#)  |       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsFocused`](#)   |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsFocused`](#)   |  |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is focused")
    public void assertElementIsFocused() {
        try {
            LocatorAssertions.IsFocusedOptions options = new LocatorAssertions.IsFocusedOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).isFocused(options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] is focused", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsHidden`](#)   |       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsHidden`](#)   |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsHidden`](#)   |  |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is hidden")
    public void assertElementIsHidden() {
        try {
            LocatorAssertions.IsHiddenOptions options = new LocatorAssertions.IsHiddenOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Locator).isHidden(options);
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsInViewport`](#)   |       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsInViewport`](#)   |  | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsInViewport`](#)   | |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is in viewport")
    public void assertElementIsInViewport() {
        try {
            LocatorAssertions.IsInViewportOptions options = new LocatorAssertions.IsInViewportOptions();
            options.setTimeout(getTimeoutValue()); 
            assertThat(Locator).isInViewport(options);
            highlightElement();
            Report.updateTestLog(Action, "[" + ObjectName + "] is in viewport", Status.PASS);
            removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object    |:green_circle: [`assertElementIsVisible`](#)   |      | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object    |:green_circle: [`assertElementIsVisible`](#)   | | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object    |:green_circle: [`assertElementIsVisible`](#)   | |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java

    @Action(object = ObjectType.PLAYWRIGHT, desc = "Assert if [<Object>] is visible")
        public void assertElementIsVisible() {
            try {
                LocatorAssertions.IsVisibleOptions options = new LocatorAssertions.IsVisibleOptions();
                options.setTimeout(getTimeoutValue());              
                assertThat(Locator).isVisible(options);
                highlightElement();
                Report.updateTestLog(Action, "[" + ObjectName + "] is visible", Status.PASS);
                removeHighlightFromElement();
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

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser    |:green_circle: [`assertPageTitleMatches`](#)   | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser    |:green_circle: [`assertPageTitleMatches`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser    |:green_circle: [`assertPageTitleMatches`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Assert if Page has title [<Data>]", input = InputType.YES)
    public void assertPageTitleMatches() {

        try {
            PageAssertions.HasTitleOptions options = new PageAssertions.HasTitleOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Page).hasTitle(Pattern.compile(Data), options);
            Report.updateTestLog(Action, "Page has title matching '" + Data + "'", Status.PASS);
        } catch (AssertionFailedError e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog("Assertion Failed", "Page does not have title matching '" + Data + "'", Status.FAIL);
        } catch (PlaywrightException e) {
            throw new ActionException(e);
        }
    }
    ```
----------------------------------

## **assertPageURLMatches**

**Description**:  This function will assert the Page URL.

**Input Format** :   @Expected Text

**Condition Format** : (Optional)  Timeout Value (in ms)

=== "Usage"

    | ObjectName | Action                     | Input         | Condition <br> (Optional) |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser    |:green_circle: [`assertPageURLMatches`](#)   | @value       | `optional` timeout (in ms)       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser    |:green_circle: [`assertPageURLMatches`](#)   | Sheet:Column | `optional` timeout (in ms)       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser    |:green_circle: [`assertPageURLMatches`](#)   | %dynamicVar% |`optional` timeout (in ms)       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Assert if Page has URL [<Data>]", input = InputType.YES)
    public void assertPageURLMatches() {

        try {
            PageAssertions.HasURLOptions options = new PageAssertions.HasURLOptions();
            options.setTimeout(getTimeoutValue());
            assertThat(Page).hasURL(Pattern.compile(Data), options);
            Report.updateTestLog(Action, "Page has URL matching '" + Data + "'", Status.PASS);
        } catch (AssertionFailedError e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog("Assertion Failed", "Page does not have URL matching '" + Data + "'", Status.FAIL);
        } catch (PlaywrightException e) {
            throw new ActionException(e);
        }
    }
    ```
----------------------------------    