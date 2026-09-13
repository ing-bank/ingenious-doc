---
icon: simple/databricks
---

# Store Actions
------------------------

## **storeAppInstalledState**

**Description**: This function is used to store whether app [<Data>] is installed into runtime variable [<Condition>].

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeAppInstalledState`](#)  | @value       | @value | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeAppInstalledState`](#)  | Sheet:Column | Sheet:Column | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeAppInstalledState`](#)  | %dynamicVar% | %dynamicVar% | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store whether app [<Data>] is installed into runtime variable [<Condition>]",
            input = InputType.YES,
            condition = InputType.YES
        )
        public void storeAppInstalledState() {
            try {
                if (
                    Data == null ||
                    Data.trim().isEmpty() ||
                    Condition == null ||
                    Condition.trim().isEmpty()
                ) {
                    Report.updateTestLog(Action, "Input/Condition cannot be empty", Status.FAIL);
                    return;
                }
                Object installed = invokeDriverMethod(
                    "isAppInstalled",
                    new Class[] { String.class },
                    new Object[] { Data.trim() }
                );
                addVar(Condition, String.valueOf(installed));
                Report.updateTestLog(
                    Action,
                    "Stored app installed state for " + Data + " in variable " + Condition,
                    Status.DONE
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to read app installed state: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------

## **storeAvailableContexts**

**Description**: This function is used to store all available contexts into runtime variable [<Data>] (comma-separated).

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeAvailableContexts`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeAvailableContexts`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeAvailableContexts`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store all available contexts into runtime variable [<Data>] (comma-separated)",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void storeAvailableContexts() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Variable name input is empty", Status.FAIL);
                    return;
                }
                Set<String> contextNames = ((SupportsContextSwitching) mDriver).getContextHandles();
                String value = String.join(",", contextNames);
                addVar(Data, value);
                Report.updateTestLog(Action, "Stored contexts in variable " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to store contexts: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------

## **storeClipboardText**

**Description**: This function is used to store clipboard text into runtime variable [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeClipboardText`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeClipboardText`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeClipboardText`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store clipboard text into runtime variable [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void storeClipboardText() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Variable name input is empty", Status.FAIL);
                    return;
                }
                Object value = invokeDriverMethod("getClipboardText", new Class[] {}, new Object[] {});
                addVar(Data, value == null ? "" : value.toString());
                Report.updateTestLog(Action, "Clipboard text stored in variable " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to read clipboard text: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------

## **storeCurrentContext**

**Description**: This function is used to store current context name into runtime variable [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeCurrentContext`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeCurrentContext`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeCurrentContext`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store current context name into runtime variable [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void storeCurrentContext() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Variable name input is empty", Status.FAIL);
                    return;
                }
                String current = ((SupportsContextSwitching) mDriver).getContext();
                addVar(Data, current);
                Report.updateTestLog(Action, "Stored current context in variable " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to store current context: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------

## **storeDeviceLocation**

**Description**: This function is used to store device location into runtime variable [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeDeviceLocation`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeDeviceLocation`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeDeviceLocation`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store device location into runtime variable [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void storeDeviceLocation() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Variable name input is empty", Status.FAIL);
                    return;
                }
                Object location = invokeDriverMethod("getLocation", new Class[] {}, new Object[] {});
                addVar(Data, location == null ? "" : location.toString());
                Report.updateTestLog(Action, "Device location stored in variable " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to get device location: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **storeElementAttribute**

**Description**: This function is used to store element's attribute into runtime variable.

**Input Format** : @Expected text

**Condition Format**: variable name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`storeElementAttribute`](#)  | @value       | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`storeElementAttribute`](#)   | Sheet:Column  || |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`storeElementAttribute`](#)  | %dynamicVar%|| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Store [<Object>] element's  attribute into Runtime variable ->  [<Data>]", input = InputType.YES, condition = InputType.YES)
	public void storeElementAttribute() {
		if (elementPresent()) {
			addVar(Condition, Element.getAttribute(Data));
			Report.updateTestLog(Action, "Element's attribute value is stored in variable", Status.PASS);
		} else {
			throw new ElementException(ExceptionType.Element_Not_Found, ObjectName);
		}
	}

    ```
----------------------
## **storeElementSelected**

**Description**: This function is used store element selection state into runtime variable.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`storeElementSelected`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`storeElementSelected`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`storeElementSelected`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Store [<Object>] element  selection state into Runtime variable: -> [<Data>]", input = InputType.YES)
	public void storeElementSelected() {
		if (elementPresent()) {
			String strObj = Input;
			if (strObj.startsWith("%") && strObj.endsWith("%")) {

				if (Element.isSelected()) {
					addVar(strObj, "true");
				} else {
					addVar(strObj, "false");
				}
				Report.updateTestLog(Action, "Element selected flag has been stored into variable '" + strObj + "'",
						Status.DONE);
			} else {
				Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
			}
		} else {
			throw new ElementException(ExceptionType.Element_Not_Found, ObjectName);
		}
	}
    ```
----------------------
## **storeElementValue**

**Description**: This function is used store element's value  into runtime variable.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`storeElementValue`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`storeElementValue`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`storeElementValue`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Store [<Object>] element's  value  into Runtime variable: -> [<Data>]", input = InputType.YES)
	public void storeElementValue() {
		if (elementPresent()) {
			String strObj = Input;
			if (strObj.startsWith("%") && strObj.endsWith("%")) {
				addVar(strObj, Element.getAttribute("value"));
				Report.updateTestLog(Action,
						"Element's value " + Element.getAttribute("value") + " is stored in variable '" + strObj + "'",
						Status.DONE);
			} else {
				Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
			}
		} else {
			throw new ElementException(ExceptionType.Element_Not_Found, ObjectName);
		}
	}
    ```
----------------------

## **storeText**

**Description**: This function is used store the element expected text into the runtime variable.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`storeText`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`storeText`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`storeText`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Store the [<Object>] element's text into the Runtime variable: [<Data>]", input = InputType.YES)
	public void storeText() {
		if (elementPresent()) {
			String strObj = Input;
			if (strObj.startsWith("%") && strObj.endsWith("%")) {
				addVar(strObj, getElementText());
				Report.updateTestLog(Action, "Element text " + getElementText() + " is stored in variable " + strObj,
						Status.PASS);
			} else {
				Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
			}
		} else {
			throw new ElementException(ExceptionType.Element_Not_Found, ObjectName);
		}
	}
    ```
----------------------
## **storeTextinDataSheet**

**Description**: This function is used to store the element's text into datasheet.

**Input Format** : @Expected datasheet name:column name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`storeTextinDataSheet`](#)   | Sheet:Column      |     | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>

    Note: Ensure that your datasheet doesn't contain column names with spaces. 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Store the [<Object>] element's text into datasheet:columname [<Data>]", input = InputType.YES)
	public void storeTextinDataSheet() {
		if (elementPresent()) {
			String strObj = Input;
			if (strObj.matches(".*:.*")) {
				try {
					System.out.println("Updating value in SubIteration " + userData.getSubIteration());
					String sheetName = strObj.split(":", 2)[0];
					String columnName = strObj.split(":", 2)[1];
					String elText = getElementText();
					userData.putData(sheetName, columnName, elText.trim());
					Report.updateTestLog(Action, "Element text [" + elText + "] is stored in " + strObj, Status.DONE);
				} catch (Exception ex) {
					Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
					Report.updateTestLog(Action, "Error Storing text in datasheet " + ex.getMessage(), Status.DEBUG);
				}

			} else {
				Report.updateTestLog(Action,
						"Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
						Status.DEBUG);
			}
		} else {
			throw new ElementException(ExceptionType.Element_Not_Found, ObjectName);
		}
	}
    ```
----------------------

## **storeTextPresent**

**Description**: This function is to store in variable true or false based on presence of text.

**Input Format** : @Expected element text

**Condition Format**: true or false

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`storeTextPresent`](#)  | @value       |  true or false    | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`storeTextPresent`](#)   | Sheet:Column  |true or false| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`storeTextPresent`](#)  | %dynamicVar%|true or false| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Store in variable true or false based on presence of text in [<Object>] element -> [<Data>]", input = InputType.YES, condition = InputType.YES)
	public void storeTextPresent() {
		try {
			if (elementPresent()) {
				if (getElementText().contains(Data)) {
					addVar(Condition, "true");
				} else {
					addVar(Condition, "false");
				}
				Report.updateTestLog(Action, "Element presence flag has been stored into variable", Status.DONE);
			} else {
				throw new ElementException(ExceptionType.Element_Not_Found, ObjectName);
			}
		} catch (Exception ex) {
			Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
			Report.updateTestLog(Action, ex.getMessage(), Status.FAIL);
		}
	}
    ```
----------------------
