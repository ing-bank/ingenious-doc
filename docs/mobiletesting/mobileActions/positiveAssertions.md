---
icon: material/flask-empty-plus-outline
---

# Positive Assertions
------------------------

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

## **assertCookieByName**

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

## **assertElementAttrEquals**

**Description**: This function will assert if element attribute equals given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrEquals`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrEquals`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrEquals`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute Equals [<Data>]", input =InputType.YES)
    public void assertElementAttrEquals() {
        assertElementAttr(SpecText.Type.IS);
    }
    ```
----------------------

## **assertElementAttrContains**

**Description**: This function will assert if element attribute contains given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrContains`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrContains`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrContains`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute Contains [<Data>]", input =InputType.YES)
    public void assertElementAttrContains() {
        assertElementAttr(SpecText.Type.CONTAINS);
    }
    ```
----------------------

## **assertElementAttrStartsWith**

**Description**: This function will assert if element attribute starts with given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrStartsWith`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrStartsWith`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrStartsWith`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute StartsWith [<Data>]", input =InputType.YES)
    public void assertElementAttrStartsWith() {
        assertElementAttr(SpecText.Type.STARTS);
    }
    ```
----------------------

## **assertElementAttrEndsWith**

**Description**: This function will assert if element attribute ends with given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrEndsWith`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrEndsWith`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrEndsWith`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute EndsWith [<Data>]", input =InputType.YES)
    public void assertElementAttrEndsWith() {
        assertElementAttr(SpecText.Type.ENDS);
    }
    ```
----------------------

## **assertElementAttrMatches**

**Description**: This function will assert if element attribute matches given data in input column

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementAttrMatches`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementAttrMatches`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementAttrMatches`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc ="Assert if [<Object>]'s Attribute Matches [<Data>]", input =InputType.YES)
    public void assertElementAttrMatches() {
        assertElementAttr(SpecText.Type.MATCHES);
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

## **assertElementTextEquals**

**Description**: This function will assert if element text equals given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextEquals`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextEquals`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextEquals`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP,desc = "Assert if [<Object>]'s Text Equals [<Data>]",input = InputType.YES)
    public void assertElementTextEquals() {
        assertElementText(Type.IS);
    }
    ```
----------------------

## **assertElementTextContains**

**Description**: This function will assert if element text contains given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextContains`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextContains`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextContains`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text Contains [<Data>]", input = InputType.YES)
    public void assertElementTextContains() {
        assertElementText(Type.CONTAINS);
    }
    ```
----------------------

## **assertElementTextStartsWith**

**Description**: This function will assert if element text starts with given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextStartsWith`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextStartsWith`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextStartsWith`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text StartsWith [<Data>]", input = InputType.YES)
    public void assertElementTextStartsWith() {
        assertElementText(Type.STARTS);
    }
    ```
----------------------

## **assertElementTextEndsWith**

**Description**: This function will assert if element text ends with given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextEndsWith`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextEndsWith`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextEndsWith`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text EndsWith [<Data>]", input = InputType.YES)
    public void assertElementTextEndsWith() {
        assertElementText(Type.ENDS);
    }
    ```
----------------------

## **assertElementTextMatchesWith**

**Description**: This function will assert if element text matches with given text in input column

=== "Usage"

    
    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`assertElementTextMatchesWith`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`assertElementTextMatchesWith`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`assertElementTextMatchesWith`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>]'s Text Matches [<Data>]", input = InputType.YES)
    public void assertElementTextMatchesWith() {
        assertElementText(Type.MATCHES);
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