---
icon: material/gesture-tap
---

# Tap
------------------------

## **Tap**

**Description**: This function is used to tap the element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`Tap`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap the [<Object>] ")
    public void Tap() {
        if (elementEnabled()) {
            Element.click();
            Report.updateTestLog(Action, "Taping on " + ObjectName, Status.DONE);

        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }
    ```

----------------------


## **TapIfExists**

**Description**: This function will tap the element if it exists.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`TapIfExists`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap the [<Object>] if it exists")
    public void TapIfExists() {
        if (Element != null) {
            Tap();
        } else {
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not Exists", Status.DONE);
        }
    }
    ```

----------------------
## **TapIfVisible**

**Description**: This function will tap the element if it is displayed.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`TapIfVisible`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap the [<Object>] if it is displayed")
    public void TapIfVisible() {
        if (Element != null) {
            if (Element.isDisplayed()) {
                Tap();
            } else {
                Report.updateTestLog(Action, "Element [" + ObjectName + "] not Visible", Status.DONE);
            }
        } else {
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not Exists", Status.DONE);
        }
    }
    ```
----------------------

## **TapAndHoldElement**

**Description**: This function is used to perform tap and hold operation on an element.


=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`TapAndHoldElement`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap and hold the [<Object>] element ")
	public void TapAndHoldElement() {
		if (elementEnabled()) {
			new Actions(mDriver).clickAndHold(Element).build().perform();
			Report.updateTestLog(Action, "Tap and hold done", Status.DONE);
		} else {
			throw new ElementException(ElementException.ExceptionType.Element_Not_Enabled, ObjectName);
		}
	}
    ```
----------------------

## **TapInputByLabel**

**Description**: This function will tap on an element whose label is provided in the element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`TapInputByLabel`](#)|                             |           |         |

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
    | Mobile     |:green_circle: [`TapInputByText`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`TapInputByText`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`TapInputByText`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Tap on the element whose label is provided in the [<Input>]", input = InputType.YES)
	public void TapInputByText() {
		cc.Element = findInputElementByLabelTextByXpath(Data);// Another variant
		new Basic(cc).Tap();
	}
    ```
----------------------

## **Tap_Relative**

**Description**: This function will tap on element based on parent object

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`Tap_Relative`](#)   |        |  | PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap on element based on parent [<Object>]", condition = InputType.YES)
    public void Tap_Relative() {
        doRelative(RelativeAction.TAP);
    }
    ```
----------------------