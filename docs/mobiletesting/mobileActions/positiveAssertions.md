---
icon: material/flask-empty-plus-outline
---

# Positive Assertions
------------------------

## **assertAdbShellOutput**

**Description**: This function is used to execute adb shell <Input> command and assert output contains [Condition] text.

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`assertAdbShellOutput`](#)  | @value       | @value      | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`assertAdbShellOutput`](#)  | Sheet:Column | Sheet:Column | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`assertAdbShellOutput`](#)  | %dynamicVar% | %dynamicVar% | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Execute adb shell <Input> command and assert output contains [Condition] text",
            input = InputType.YES,
            condition = InputType.YES
        )
        public void assertAdbShellOutput() {
            if (!isAndroid()) return;
            try {
                String output = runShell(Data);
                if (output.contains(Condition)) {
                    Report.updateTestLog(
                        Action,
                        "Output contained '" + Condition + "': " + output,
                        Status.PASS
                    );
                } else {
                    Report.updateTestLog(
                        Action,
                        "Expected output to contain '" + Condition + "' but got: " + output,
                        Status.FAIL
                    );
                }
            } catch (Exception e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(Action, "adb shell failed: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------## **assertCookieByName**

**Description**: This function will assert if the cookie has the expected name.

**Input Format** : @Expected text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`assertCookieByName`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`assertCookieByName`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`assertCookieByName`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Assert if cookie: [<Object>] has name: [<Data>]", input = InputType.YES)
	public void assertCookieByName() {
		try {

			String strCookieName = Data.split(":", 2)[0];
			String strCookieValue = Data.split(":", 2)[1];
			if (mDriver.manage().getCookieNamed(strCookieName) != null) {
				if ((mDriver.manage().getCookieNamed(strCookieName).getValue().equals(strCookieValue))) {
					System.out.println("assertCookieByName Passed");
					Report.updateTestLog("assertCookieByName", "Cookie name matched with provided data", Status.PASS);

				} else {
					throw new Exception("Cookie value did not match with provided data");
				}
			} else {
				throw new Exception("Cookie  with the name '" + strCookieName + "' did not exist");
			}
		} catch (Exception ex) {
			System.out.println("assertCookieByName Failed");
			Logger.getLogger(Assertions.class.getName()).log(Level.SEVERE, null, ex);
			throw new ForcedException("assertCookieByName", ex.getMessage());
		}
	}
    ```
----------------------
## **assertCookiePresent**

**Description**: This function will assert if the cookie is present.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`assertCookiePresent`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`assertCookiePresent`](#)   | Sheet:Column |   | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`assertCookiePresent`](#)   | %dynamicVar% |   | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Assert if cookie name: [<Data>] is present", input = InputType.YES)
	public void assertCookiePresent() {
		try {
			String strCookieName = Data;
			if ((mDriver.manage().getCookieNamed(strCookieName) != null)) {
				System.out.println("assertCookiePresent Passed");
				Report.updateTestLog("assertCookiePresent", "Cookie name matched with the data provided", Status.PASS);
			} else {
				throw new Exception("Cookie name did not match with data provided");
			}
		} catch (Exception ex) {
			System.out.println("assertCookiePresent Failed");
			Logger.getLogger(Assertions.class.getName()).log(Level.SEVERE, null, ex);
			throw new ForcedException("assertCookiePresent", ex.getMessage());
		}
	}
    ```
-------------------------------

## **assertElementAttrContains**

**Description**: This function will assert if element attribute contains given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrContains`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrContains`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrContains`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute Contains [<Data>]", input =InputType.YES)
    public void assertElementAttrContains() {
        assertElementAttr(SpecText.Type.CONTAINS);
    }
    ```
----------------------

## **assertElementAttrEndsWith**

**Description**: This function will assert if element attribute ends with given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrEndsWith`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrEndsWith`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrEndsWith`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute EndsWith [<Data>]", input =InputType.YES)
    public void assertElementAttrEndsWith() {
        assertElementAttr(SpecText.Type.ENDS);
    }
    ```
----------------------

## **assertElementAttrEquals**

**Description**: This function will assert if element attribute equals given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrEquals`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrEquals`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrEquals`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute Equals [<Data>]", input =InputType.YES)
    public void assertElementAttrEquals() {
        assertElementAttr(SpecText.Type.IS);
    }
    ```
----------------------

## **assertElementAttrMatches**

**Description**: This function will assert if element attribute matches given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrMatches`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrMatches`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrMatches`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute Matches [<Data>]", input =InputType.YES)
    public void assertElementAttrMatches() {
        assertElementAttr(SpecText.Type.MATCHES);
    }
    ```
----------------------

## **assertElementAttrStartsWith**

**Description**: This function will assert if element attribute starts with given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrStartsWith`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrStartsWith`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrStartsWith`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute StartsWith [<Data>]", input =InputType.YES)
    public void assertElementAttrStartsWith() {
        assertElementAttr(SpecText.Type.STARTS);
    }
    ```
----------------------

## **assertElementContains**

**Description**: This function will assert if element contains

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementContains`](#)   |        |  | PageName |
    
=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>] contains <Object2> ", condition = InputType.YES)
    public void assertElementContains() {
        assertElementContains(false);
    }
    ```
----------------------

## **assertElementContainsPartly**

**Description**: This function will assert if element partly contains

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementContainsPartly`](#)   |        |  | PageName |
    
=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP,desc ="Assert if [<Object>] partly contains  <Object2> ", input =InputType.NO, 
    		condition = InputType.YES)
        public void assertElementContainsPartly() {
            assertElementContains(true);
    }
    ```
----------------------

## **assertElementDisplayed**

**Description**: This function will assert if the Element is displayed.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`assertElementDisplayed`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] element is displayed")
    public void assertElementDisplayed() {
        assertElement(elementDisplayed());
    }
    ```

----------------------
## **assertElementEnabled**

**Description**: This function will assert if the Element is enabled.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`assertElementEnabled`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is enabled on the current page")

    public void assertElementEnabled() {
        assertElement(elementEnabled());
    }
    ```
----------------------

## **assertElementPresent**

**Description**: This function will assert if the Element is present.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`assertElementPresent`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is present")
    public void assertElementPresent() {
        assertElement(elementPresent());
    ```

----------------------
## **assertElementSelected**

**Description**: This function will assert if the Element is selected.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`assertElementSelected`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] element is selected")
    public void assertElementSelected() {
        assertElement(elementSelected());
    }
    ```

----------------------

## **assertElementTextByLabel**

**Description**: This function is used to assert if the element text adjacent to provided label element equals the expected data.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextByLabel`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextByLabel`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextByLabel`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text adjacent to provided label element Equals [<Data>]", input = InputType.YES)
	public void assertElementTextByLabel() {
		cc.Element = findInputElementByLabelTextByXpath();
		new Text(cc).assertElementTextEquals();
	}
    ```
----------------------

## **assertElementTextContains**

**Description**: This function will assert if element text contains given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextContains`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextContains`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextContains`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text Contains [<Data>]", input = InputType.YES)
    public void assertElementTextContains() {
        assertElementText(Type.CONTAINS);
    }
    ```
----------------------

## **assertElementTextContainsByLabel**

**Description**: This function is used to assert if the element text adjacent to provided label element contains the expected data.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextContainsByLabel`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextContainsByLabel`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextContainsByLabel`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text adjacent to provided label element Contains [<Data>]", input = InputType.YES)
	public void assertElementTextContainsByLabel() {
		cc.Element = findInputElementByLabelTextByXpath();
		new Text(cc).assertElementTextContains();
	}
    ```
----------------------

## **assertElementTextEndsWith**

**Description**: This function will assert if element text ends with given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextEndsWith`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextEndsWith`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextEndsWith`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text EndsWith [<Data>]", input = InputType.YES)
    public void assertElementTextEndsWith() {
        assertElementText(Type.ENDS);
    }
    ```
----------------------

## **assertElementTextEquals**

**Description**: This function will assert if element text equals given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextEquals`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextEquals`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextEquals`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP,desc = "Assert if [<Object>]'s Text Equals [<Data>]",input = InputType.YES)
    public void assertElementTextEquals() {
        assertElementText(Type.IS);
    }
    ```
----------------------

## **assertElementTextMatchesWith**

**Description**: This function will assert if element text matches with given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextMatchesWith`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextMatchesWith`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextMatchesWith`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text Matches [<Data>]", input = InputType.YES)
    public void assertElementTextMatchesWith() {
        assertElementText(Type.MATCHES);
    }
    ```
----------------------

## **assertElementTextStartsWith**

**Description**: This function will assert if element text starts with given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextStartsWith`](#)   | @value       |  | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextStartsWith`](#)   | Sheet:Column |  | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextStartsWith`](#)   | %dynamicVar% |  | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text StartsWith [<Data>]", input = InputType.YES)
    public void assertElementTextStartsWith() {
        assertElementText(Type.STARTS);
    }
    ```
----------------------

## **assertTextPresentInPage**

**Description**: This function will assert if the expected text is present on the page.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`assertTextPresentInPage`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`assertTextPresentInPage`](#)  | Sheet:Column |      | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`assertTextPresentInPage`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Assert if text: [<Data>] is present on the page", input = InputType.YES)
	public void assertTextPresentInPage() throws RuntimeException {

		try {
			String strObj = Data;
			if (mDriver.findElement(By.tagName("html")).getText().contains(strObj)) {
				System.out.println("assertTextPresent passed");
				Report.updateTestLog("assertTextPresentInPage",
						"Expected text '" + strObj + "' is  present in the page", Status.PASS);

			} else {
				System.out.println("assertTextPresentInPage failed");
				throw new Exception("Expected text  '" + strObj + "' is not present in the page");
			}

		} catch (Exception e) {
			Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
			throw new ForcedException("assertTextPresentInPage", e.getMessage());
		}
	}
    ```
----------------------------------------

