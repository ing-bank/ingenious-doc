# ByLabel Actions
------------------------

## **storeText**

**Description**: This function is used store the element expected text into the runtime variable.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`storeText`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`storeText`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`storeText`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
    | APP     |:green_circle: [`storeTextinDataSheet`](#)   | Sheet:Column      |     | |<span style="color:Blue">:arrow_left: *Datasheet to where value is supposed br stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces. 

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
    | APP     |:green_circle: [`storeTextPresent`](#)  | @value       |  true or false    | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`storeTextPresent`](#)   | Sheet:Column  |true or false| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`storeTextPresent`](#)  | %dynamicVar%|true or false| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
## **storeElementSelected**

**Description**: This function is used store element selection state into runtime variable.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`storeElementSelected`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`storeElementSelected`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`storeElementSelected`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
## **storeElementAttribute**

**Description**: This function is used to store element's attribute into runtime variable.

**Input Format** : @Expected text

**Condition Format**: variable name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`storeElementAttribute`](#)  | @value       | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`storeElementAttribute`](#)   | Sheet:Column  || |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`storeElementAttribute`](#)  | %dynamicVar%|| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
## **storeElementValue**

**Description**: This function is used store element's value  into runtime variable.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`storeElementValue`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`storeElementValue`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`storeElementValue`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
## **storeAlertPresent**

**Description**: This function is used store exist or not exist based on the alert presence.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | MOBILE     |:green_circle: [`storeAlertPresent`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE     |:green_circle: [`storeAlertPresent`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE     |:green_circle: [`storeAlertPresent`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Store \"Exist\" or \"Not Exist\" based on the alert presence into -> [<Data>] Runtime variable", input = InputType.YES)
	public void storeAlertPresent() {
		String strObj = Input;
		if (strObj.startsWith("%") && strObj.endsWith("%")) {
			if (isAlertPresent(mDriver)) {
				addVar(strObj, "Exist");
			} else {
				addVar(strObj, "Not Exist");
			}
			Report.updateTestLog(Action, "Alert Text Status Stored", Status.DONE);
		} else {
			Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
		}
	}

    ```
----------------------

## **storeVariable**

**Description**: This function is used to store variable value.

**Input Format** : @Expected text

**Condition Format**: variable name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | MOBILE     |:green_circle: [`storeVariable`](#)  | @value       | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE     |:green_circle: [`storeVariable`](#)   | Sheet:Column  || |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE     |:green_circle: [`storeVariable`](#)  | %dynamicVar%|| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "store  value [<Data>] in Variable [<Condition>]", input = InputType.YES, condition = InputType.YES)
	public void storeVariable() {
		if (Condition.startsWith("%") && Condition.endsWith("%")) {
			addVar(Condition, Data);
			Report.updateTestLog(Action, "Value" + Data + "' is stored in Variable '" + Condition + "'", Status.DONE);
		} else {
			Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
		}
	}

    ```
----------------------
----------------------
## **storeVariableInDataSheet**

**Description**: This function is used to store variable value into the datasheet.

**Input Format** : @Expected text

**Condition Format**: variable name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | MOBILE     |:green_circle: [`storeVariableInDataSheet`](#)  | @value       | | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE     |:green_circle: [`storeVariableInDataSheet`](#)   | Sheet:Column  || |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE     |:green_circle: [`storeVariableInDataSheet`](#)  | %dynamicVar%|| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "store variable value [<Condition>] in data sheet[<Data>]", input = InputType.YES, condition = InputType.YES)
	public void storeVariableInDataSheet() {
		if (Input != null && Condition != null) {
			if (!getVar(Condition).isEmpty()) {
				System.out.println(Condition);
				String[] sheetDetail = Input.split(":");
				String sheetName = sheetDetail[0];
				String columnName = sheetDetail[1];
				userData.putData(sheetName, columnName, getVar(Condition));
				Report.updateTestLog(Action,
						"Value of variable " + Condition + " has been stored into " + "the data sheet", Status.DONE);
			} else {
				Report.updateTestLog(Action, "The variable " + Condition + " does not contain any value", Status.FAIL);
			}
		} else {
			Report.updateTestLog(Action, "Incorrect input format", Status.DEBUG);
			System.out.println("Incorrect input format " + Condition);
		}
	}

    ```
----------------------