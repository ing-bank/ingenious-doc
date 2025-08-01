---
icon: octicons/browser-16
---

# General Actions
------------------------

## **back**

**Description**: This function will navigate to previous page.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`back`](#)|                             |           |         |

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

## **clear**

**Description**: This function is used to clear text from the element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`clear`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Clear text [<Data>] from object [<Object>].")
    public void clear() {
        if (elementEnabled()) {
            Element.clear();
            Report.updateTestLog("Clear", "Cleared Text on '" + ObjectName + "'", Status.DONE);
        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }
    ```
----------------------

## **isEnabled**

**Description**: This function is used to verify web element is enabled.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`isEnabled`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Object [<Object> is enabled]")
    public void isEnabled() {
        if (elementEnabled()) {
            Report.updateTestLog(Action, "Web Element is enabled", Status.PASS);
        } else {
            throw new ElementException(ElementException.ExceptionType.Element_Not_Enabled, Condition);
        }
    }
    ```
----------------------

## **mouseOverElement**

**Description**: This function is used to perform mouse hover operation on an element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`mouseOverElement`](#)|                             |           |         |

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

## **moveTo**

**Description**: This function is used to move the browser view to the specified element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`moveTo`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Move the Browser View to the specified element [<Object>]")
    public void moveTo() {
        if (elementDisplayed()) {
            if (Data != null && Data.matches("(\\d)+,(\\d)+")) {
                int x = Integer.valueOf(Data.split(",")[0]);
                int y = Integer.valueOf(Data.split(",")[1]);
                new Actions(mDriver).moveToElement(Element, x, y).build().perform();
            } else {
                new Actions(mDriver).moveToElement(Element).build().perform();
            }
            Report.updateTestLog(Action, "Viewport moved to" + ObjectName, Status.DONE);
        } else {
            throw new ElementException(ExceptionType.Element_Not_Visible, ObjectName);
        }
    }
    ```
----------------------

## **releaseElement**

**Description**: This function is used to perform release operation on an element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`releaseElement`](#)|                             |           |         |

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
    | Mobile     |:green_circle: [`saveScreenshot`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`saveScreenshot`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`saveScreenshot`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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

## **sendKeysToElement**

**Description**: This function is used to perform send key action on object.
**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`sendKeysToElement`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`sendKeysToElement`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`sendKeysToElement`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java

    @Action(object = ObjectType.APP, desc = "Send Keys [<Data>]  to object [<Object>].", input = InputType.YES)
    public void sendKeysToElement() {
        if (elementPresent()) {
            String[] Values = Data.toLowerCase().split("\\+");
            if (Values.length == 4) {
                Element.sendKeys(Keys
                        .chord(getKeyCode(Values[0]),
                                getKeyCode(Values[1]),
                                getKeyCode(Values[2]),
                                getKeyCode(Values[3]) != null ? getKeyCode(Values[3])
                                : Values[3]));
                Report.updateTestLog(Action, "Keys Submitted", Status.DONE);
            } else if (Values.length == 3) {
                Element.sendKeys(Keys
                        .chord(getKeyCode(Values[0]),
                                getKeyCode(Values[1]),
                                getKeyCode(Values[2]) != null ? getKeyCode(Values[2])
                                : Values[2]));
                Report.updateTestLog(Action, "Keys Submitted", Status.DONE);
            } else if (Values.length == 2) {
                Element.sendKeys(Keys
                        .chord(getKeyCode(Values[0]),
                                getKeyCode(Values[1]) != null ? getKeyCode(Values[1])
                                : Values[1]));
                Report.updateTestLog(Action, "Keys Submitted", Status.DONE);
            } else if (Values.length == 1) {
                Element.sendKeys(Keys.chord(getKeyCode(Values[0])));
                Report.updateTestLog(Action, "Keys Submitted", Status.DONE);
            }
        } else {
            throw new ElementException(ExceptionType.Element_Not_Found, ObjectName);
        }
    }
    ```
----------------------

## **sendKeysToWindow**

**Description**: This function is used to perform send key action on window.
**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`sendKeysToWindow`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`sendKeysToWindow`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`sendKeysToWindow`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java

    @Action(object = ObjectType.MOBILE, desc = "Send Keys [<Data>]  to Window.", input = InputType.YES)
    public void sendKeysToWindow() {
        Actions builder = new Actions(mDriver);
        String[] Values = Data.toLowerCase().split("\\+");
        switch (Values.length) {
            case 4:
                builder.sendKeys(
                        Keys.chord(
                                getKeyCode(Values[0]),
                                getKeyCode(Values[1]),
                                getKeyCode(Values[2]),
                                getKeyCode(Values[3]) != null ? getKeyCode(Values[3])
                                : Values[3])).perform();
                Report.updateTestLog(Action, "Keys Submitted", Status.DONE);
                break;
            case 3:
                builder.sendKeys(
                        Keys.chord(
                                getKeyCode(Values[0]),
                                getKeyCode(Values[1]),
                                getKeyCode(Values[2]) != null ? getKeyCode(Values[2])
                                : Values[2])).perform();
                Report.updateTestLog(Action, "Keys Submitted", Status.DONE);
                break;
            case 2:
                builder.sendKeys(
                        Keys.chord(
                                getKeyCode(Values[0]),
                                getKeyCode(Values[1]) != null ? getKeyCode(Values[1])
                                : Values[1])).build().perform();
                Report.updateTestLog(Action, "Keys Submitted", Status.DONE);
                break;
            case 1:
                builder.sendKeys(Keys.chord(getKeyCode(Values[0]))).build()
                        .perform();
                Report.updateTestLog(Action, "Keys Submitted", Status.DONE);
                break;
            default:
                Report.updateTestLog(Action, "Input format is not correct",
                        Status.DEBUG);
                break;
        }
    }

    Keys getKeyCode(String data) {
        switch (data) {
            case "tab":
                return Keys.TAB;
            case "enter":
                return Keys.ENTER;
            case "shift":
                return Keys.SHIFT;
            case "ctrl":
                return Keys.CONTROL;
            case "alt":
                return Keys.ALT;
            case "esc":
                return Keys.ESCAPE;
            case "delete":
                return Keys.DELETE;
            case "backspace":
                return Keys.BACK_SPACE;
            case "home":
                return Keys.HOME;
            default:
                try {
                    return Keys.valueOf(data.toUpperCase());
                } catch (Exception ex) {
                    return null;
                }
        }
    }
    ```
----------------------

## **Submit**

**Description**: This function is used to submit action on the browser.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`Submit`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Submit action on the browser")
    public void Submit() {
        if (elementEnabled()) {
            Element.submit();
            Report.updateTestLog(Action, "[" + ObjectName + "] Submitted successfully ", Status.DONE);

        } else {
            throw new ElementException(ExceptionType.Element_Not_Enabled, ObjectName);
        }
    }
    ```
----------------------
## **SubmitIfExists**

**Description**: This function is used to submit the element if it exists.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`SubmitIfExists`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Submit the [<Object>] if it exists")
    public void SubmitIfExists() {
        if (Element != null) {
            Submit();
        } else {
            Report.updateTestLog(Action, "Element [" + ObjectName + "] not Exists", Status.DONE);
        }
    }
    ```
----------------------

## **submitInputByLabel**

**Description**: This function is used to submit the input element adjacent to the provided label element.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`submitInputByLabel`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Submit input element adjacent to the provided label element [<Object>]")
	public void submitInputByLabel() {
		cc.Element = findInputElementByLabelTextByXpath();
		new Basic(cc).Submit();
	}
    ```
----------------------

## **switchContextWhenNameContains**

**Description**: This function is used to switch context when name contains.

**Input Format** : @Expected text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`switchContextWhenNameContains`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`switchContextWhenNameContains`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`switchContextWhenNameContains`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Switch Context When Name Contains", input = InputType.YES, condition = InputType.NO)
    public void switchContextWhenNameContains() {
        try {
            Set<String> contextNames = ((SupportsContextSwitching) mDriver).getContextHandles();
            for (String contextName : contextNames) {
                if (contextName.contains(Data)) {
                    ((SupportsContextSwitching) mDriver).context(contextName);
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    ```
---------------------------------

## **switchContextWhenNameEquals**

**Description**: This function is used to switch context when name equals.

**Input Format** : @Expected text


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`switchContextWhenNameEquals`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`switchContextWhenNameEquals`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`switchContextWhenNameEquals`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Switch Context When Name Equals", input = InputType.YES, condition = InputType.NO)
    public void switchContextWhenNameEquals() {
        try {
            Set<String> contextNames = ((SupportsContextSwitching) mDriver).getContextHandles();
            for (String contextName : contextNames) {
                if (contextName.equals(Data)) {
                    ((SupportsContextSwitching) mDriver).context(contextName);
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    ```
---------------------------------





