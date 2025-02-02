# ByLabel Actions
------------------------

## **setInputByLabel**

**Description**: This function is used to set the expected text to an input element that is adjacent to the provided label element.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`setInputByLabel`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`setInputByLabel`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`setInputByLabel`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Set the data [<Data>] to an input element that is adjacent to the provided label element [<Object>]", input = InputType.YES)
	public void setInputByLabel() {
		cc.Element = findInputElementByLabelTextByXpath();
		new Basic(cc).Set();
	}
    ```

----------------------


## **TapInputByLabel**

**Description**: This function will tap on an element whose label is provided in the element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`TapInputByLabel`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap on an element whose label is provided in the [<Object>]")
	public void TapInputByLabel() {
		cc.Element = findInputElementByLabelTextByXpath();
		new Basic(cc).Tap();
	}
    ```

----------------------
## **TapInputByText**

**Description**: This function will tap on the element whose label is provided in the input.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`TapInputByText`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`TapInputByText`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`TapInputByText`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Tap on the element whose label is provided in the [<Input>]", input = InputType.YES)
	public void TapInputByText() {
		cc.Element = findInputElementByLabelTextByXpath(Data);// Another variant
		new Basic(cc).Tap();
	}
    ```
----------------------
## **submitInputByLabel**

**Description**: This function is used to submit the input element adjacent to the provided label element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`submitInputByLabel`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Submit input element adjacent to the provided label element [<Object>]")
	public void submitInputByLabel() {
		cc.Element = findInputElementByLabelTextByXpath();
		new Basic(cc).Submit();
	}
    ```
----------------------
## **assertElementTextByLabel**

**Description**: This function is used to assert if the element text adjacent to provided label element equals the expected data.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`assertElementTextByLabel`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`assertElementTextByLabel`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`assertElementTextByLabel`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text adjacent to provided label element Equals [<Data>]", input = InputType.YES)
	public void assertElementTextByLabel() {
		cc.Element = findInputElementByLabelTextByXpath();
		new Text(cc).assertElementTextEquals();
	}
    ```
----------------------

## **assertElementTextContainsByLabel**

**Description**: This function is used to assert if the element text adjacent to provided label element contains the expected data.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`assertElementTextContainsByLabel`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`assertElementTextContainsByLabel`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`assertElementTextContainsByLabel`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text adjacent to provided label element Contains [<Data>]", input = InputType.YES)
	public void assertElementTextContainsByLabel() {
		cc.Element = findInputElementByLabelTextByXpath();
		new Text(cc).assertElementTextContains();
	}
    ```