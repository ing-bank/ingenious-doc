---
icon: material/alert
---

# Alert Actions
------------------------

## **answerAlert**

**Description**: This function is used to answer the alert present with the expected text.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`answerAlert`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`answerAlert`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`answerAlert`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Answer the alert present with [<Data>]", input = InputType.YES)
	public void answerAlert() {
		String setAlertText = Data;
		try {
			mDriver.switchTo().alert().sendKeys(setAlertText);
			Report.updateTestLog(Action, "Message '" + setAlertText + "' is set in the alert window", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
			Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
		}
	}
    ```
----------------------
## **acceptAlert**

**Description**: This function is used to accept the alert.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`acceptAlert`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Accept the alert present")
	public void acceptAlert() {
		try {
			mDriver.switchTo().alert().accept();
			Report.updateTestLog(Action, "Alert is accepted", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
			Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
		}
	}
    ```
----------------------
## **dismissAlert**

**Description**: This function is used to dismiss the alert.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`dismissAlert`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Dismiss the alert present")
	public void dismissAlert() {
		try {
			mDriver.switchTo().alert().dismiss();
			Report.updateTestLog(Action, "Alert is dismissed", Status.DONE);
		} catch (Exception e) {
			Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
			Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
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
    | Mobile     |:green_circle: [`storeAlertPresent`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeAlertPresent`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeAlertPresent`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
----------------------------------
## **waitForAlertPresent**

**Description**: This function will wait for alert to be present

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Mobile   |:green_circle: [`waitForAlertPresent`](#)| | |  |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Wait for alert to be present ", condition = InputType.OPTIONAL)
    public void waitForAlertPresent() {
        waitFor(WaitType.ALERT_PRESENT,
                "Alert popped up in stipulated time");
    }
    ```
----------------------
