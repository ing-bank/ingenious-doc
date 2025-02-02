# ByLabel Actions
------------------------

## **back**

**Description**: This function will navigate to previous page.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`back`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Navigate to previous page")
	public void back() {
		try {
			mDriver.navigate().back();
			Report.updateTestLog("back", "Navigate page back is success", Status.DONE);
		} catch (WebDriverException e) {
			Report.updateTestLog("back", e.getMessage(), Status.FAIL);
			Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
		}
	}
    ```

----------------------
## **dragToAndDropElement**

**Description**: This function is used to perform drag and drop operation on an element.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | APP     |:green_circle: [`dragToAndDropElement`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | APP     |:green_circle: [`dragToAndDropElement`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | APP     |:green_circle: [`dragToAndDropElement`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "drag and drop operation of ", input = InputType.YES)
	public void dragToAndDropElement() {
		try {
			String Page = Data.split(":", 2)[0];
			String Object = Data.split(":", 2)[1];
			if (elementPresent()) {
				WebElement DropElement = mObject.findElement(Object, Page);
				if (DropElement != null) {
					new Actions(mDriver).dragAndDrop(Element, DropElement).build().perform();
					Report.updateTestLog(Action,
							"'" + ObjectName + "' has been dragged and dropped to '" + Object + "'", Status.PASS);
				} else {
					throw new ElementException(ElementException.ExceptionType.Element_Not_Found, Object);
				}
			} else {
				throw new ElementException(ElementException.ExceptionType.Element_Not_Found, ObjectName);
			}
		} catch (Exception e) {
			Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
			Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, e.getMessage(), e);
		}
	}
    ```
----------------------
## **mouseOverElement**

**Description**: This function is used to perform mouse hover operation on an element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`mouseOverElement`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Hover over the [<Object>] element")
	public void mouseOverElement() {
		if (elementPresent()) {
			new Actions(mDriver).moveToElement(Element).build().perform();
			Report.updateTestLog(Action, "Mouse Over to Element '" + ObjectName, Status.DONE);
		} else {
			throw new ElementException(ElementException.ExceptionType.Element_Not_Found, ObjectName);
		}
	}
    ```
----------------------
## **TapAndHoldElement**

**Description**: This function is used to perform tap and hold operation on an element.


=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`TapAndHoldElement`](#)|                             |           |         |

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

## **releaseElement**

**Description**: This function is used to perform release operation on an element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`releaseElement`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Release the dragged element over the [<Object>] element ")
	public void releaseElement() {
		if (elementEnabled()) {
			new Actions(mDriver).release(Element).build().perform();
			Report.updateTestLog(Action, "releaseElement action is done", Status.DONE);
		} else {
			throw new ElementException(ElementException.ExceptionType.Element_Not_Enabled, ObjectName);
		}
	}
    ```
----------------------

## **saveScreenshot**

**Description**: This function is used to take screenshot of the current page and store it in the input location.

**Input Format** : @Expected filepath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | MOBILE     |:green_circle: [`saveScreenshot`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE     |:green_circle: [`saveScreenshot`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE     |:green_circle: [`saveScreenshot`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Take screenshot of the current page and store it in the location [<Input>]", input = InputType.YES)
	public void saveScreenshot() {
		try {
			String strFullpath = Data;
			File scrFile = getDriverControl().createScreenShot();
			FileUtils.copyFile(scrFile, new File(strFullpath));
			Report.updateTestLog(Action, "Screenshot is taken and saved in this path -'" + strFullpath + "'",
					Status.PASS);
		} catch (IOException e) {
			Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
			Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
		}

	}
    ```
----------------------