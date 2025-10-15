---
icon: octicons/browser-16
---

# General Actions
------------------------

## **sapFill**

**Description**: This function is used to **enter data** in an `input` type object

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapFill`](#)  | @value       |       | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`sapFill`](#)  | Sheet:Column |       | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`sapFill`](#)  | %dynamicVar% |       | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Enter the value [<Data>] in the field [<Object>]", input = InputType.YES)
	public void sapFill() {
		try {
			Dispatch.put(SAPElement, "Text", Data);
			Report.updateTestLog(Action, "Entered Text '" + Data + "' on '" + ObjectName + "'", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed to Enter Text. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapEnter**

**Description**: This function is used to press **Enter** key element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapEnter`](#)| | | PageName |

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Press [<Enter>] key", input = InputType.NO)
	public void sapEnter() {
		try {
			Dispatch.call(SAPElement, "sendVKey", 0);
			Report.updateTestLog(Action, "Enter key pressed successfully.", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Error in Enter key press. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapClick**

**Description**: This function will **click** on an element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapClick`](#)| | | PageName |

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Click the [<Object>] ")
	public void sapClick() {
		try {
			Dispatch.call(SAPElement, "press");
			Report.updateTestLog(Action, "Clicking on [" + ObjectName +"]", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed to click. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapDoubleClickCell**

**Description**: This function will **double click** on the current cell

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapDoubleClickCell`](#)| | | PageName |

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Double click the current Cell ")
	public void sapDoubleClickCell() {
		try {
			Dispatch.call(SAPElement, "doubleClickCurrentCell");
			Report.updateTestLog(Action, "Double Clicking on Current cell [" + ObjectName+ "]", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed to double click. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapSimulateKeyPress**

**Description**: This function is used to **press a key or combination of keys**

**Input Format** : @Expected Keys or combination. See key combinations for reference.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapSimulateKeyPress`](#)   | @value       |       | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span> 
    | Object     |:green_circle: [`sapSimulateKeyPress`](#)   | Sheet:Column |       | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Object     |:green_circle: [`sapSimulateKeyPress`](#)   | %dynamicVar% |       | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Simulate key press with VCode [<Data>] ", input = InputType.YES)
	public void sapSimulateKeyPress() {
		try {
			Dispatch.call(SAPElement, "sendVKey", Integer.parseInt(Data));
			Report.updateTestLog(Action, "Simulate key press with VKey code [" + Data + "]", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action,
					"Fails to simulate key press with VKey code [" + Data + "]. Error : " + e.getMessage(),
					Status.FAILNS);
		}
	}
    ```

=== "Key Combinations"

    | Input | Key Combination |
    |-------|-----------------|
    | 00 | Enter |
    | 01 | F1 |
    | 02 | F2 |
    | 03 | F3 |
    | 04 | F4 |
    | 05 | F5 |
    | 06 | F6 |
    | 07 | F7 |
    | 08 | F8 |
    | 09 | F9 |
    | 10 | F10 |
    | 11 | Ctrl+S |
    | 12 | F12 |

    More key combinations [here](https://help.sap.com/docs/sap_gui_for_windows/b47d018c3b9b45e897faf66a6c0885a8/71d8c95e9c7947ffa197523a232d8143.html).
----------------------

## **sapAssertElementTextContains**

**Description**: This function is used to validate whether the element contains an expected text or not

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapAssertElementTextContains`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`sapAssertElementTextContains`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`sapAssertElementTextContains`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Assert that [<Object>] contains Text [<Data>]", input = InputType.YES)
	public void sapAssertElementTextContains() {
		try {
			String actualText = Dispatch.get(SAPElement, "Text").toString();
			if (actualText.contains(Data)) {
				Report.updateTestLog(Action, "["+ObjectName+
						"]actual text [" + actualText + "] contains expected text [" + Data + "].",
						Status.PASSNS);
			} else {
				Report.updateTestLog(Action,"["+ObjectName+
						"] actual text [" + actualText + "] not contains expected text [" + Data + "].", Status.FAILNS);
			}
		} catch (Exception e) {
			Report.updateTestLog(Action, "Fails to get Element text. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapSelectRadioButtonInRow**

**Description**: This function is used to select **Radio button** element

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapSelectRadioButtonInRow`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`sapSelectRadioButtonInRow`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`sapSelectRadioButtonInRow`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Select Radio Button ", input = InputType.YES)
	public void sapSelectRadioButtonInRow() {
		try {
			Dispatch row = Dispatch.call(SAPElement, "GetAbsoluteRow", Data).toDispatch();
			Dispatch.put(row, "Selected", true);
			Report.updateTestLog(Action, "Radio button selected successfully.", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Fails to select radio button. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapSelectCheckBox**

**Description**: This function is used to **check** a `check-box` type object

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapSelectCheckBox`](#)| | | PageName |

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Select checkbox ", input = InputType.NO)
	public void sapSelectCheckBox() {
		try {
			Dispatch.put(SAPElement, "Selected", true);
			Report.updateTestLog(Action, "Checkbox selected successfully.", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Fails to select Checkbox. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapSelect**

**Description**: This function is used to **select** an element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapSelect`](#)| | | PageName |

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Select the [<Object>] ")
	public void sapSelect() {
		try {
			Dispatch.call(SAPElement, "select");
			Report.updateTestLog(Action, "Select tab [" + ObjectName+"]", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed Select tab. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapSelectDropDownByText**

**Description**: This function is used to **select dropdown** from a given text

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapSelectDropDownByText`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`sapSelectDropDownByText`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`sapSelectDropDownByText`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Select dropdown value by visible text ", input = InputType.YES)
	public void sapSelectDropDownByText() {
		try {
			Dispatch.put(SAPElement, "Text", Data);
			Report.updateTestLog(Action, "Dropdown set with text [" + Data + "]", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed to set dropdown with text. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapSelectDropDownByKey**

**Description**: This function is used to **select dropdown** from a given key

**Input Format** : @Expected Key

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapSelectDropDownByKey`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`sapSelectDropDownByKey`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`sapSelectDropDownByKey`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Select Dropdown value by Key", input = InputType.YES)
	public void sapSelectDropDownByKey() {
		try {
			Dispatch.put(SAPElement, "Key", Data);
			Report.updateTestLog(Action, "Dropdown set with Key [" + Data + "]", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed to set dropdown with key. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapSelectDropDownByIndex**

**Description**: This function is used to **select dropdown** from a given index

**Input Format** : @Expected Index

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapSelectDropDownByIndex`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle: [`sapSelectDropDownByIndex`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle: [`sapSelectDropDownByIndex`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Select dropdown value by index", input = InputType.YES)
	public void sapSelectDropDownByIndex() {
		try {
			Dispatch.call(SAPElement, "Select", new Variant(Integer.parseInt(Data)));
			Report.updateTestLog(Action, "Dropdown set with index [" + Data + "]", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed to set dropdown with index . Error : " + e.getMessage(),
					Status.FAILNS);
		}
	}
    ```
----------------------

## **sapSetFocus**

**Description**: This function is used to **focus** on an element

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Object     |:green_circle: [`sapSetFocus`](#)| | | PageName |

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.SAP, desc = "Set focus on [<Object>]", input = InputType.NO)
	public void sapSetFocus() {
		try {
			Dispatch.call(SAPElement, "setFocus");
			Report.updateTestLog(Action, "Focus has been set on [" + ObjectName+"]", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed to set focus on [" + ObjectName+"]. Error : " + e.getMessage(), Status.FAILNS);
		}
	}
    ```
----------------------

## **sapCloseLogonScreen**

**Description**: This function is used to **close** logon landscape screen

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Browser    |:green_circle: [`sapCloseLogonScreen`](#)| | | PageName |

=== "Corresponding Code"

    ```java
	@Action(object = ObjectType.BROWSER, desc = "Close logon landscape screen", input = InputType.NO)
	public void sapCloseLogonScreen() {
		try {
			SAPProcess.destroy();
			Report.updateTestLog(Action, "Logon landscape screen closed successfully", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, "Failed to close Logon landscape screen. Error : " + e.getMessage(),
					Status.FAILNS);
		}
	}
    ```