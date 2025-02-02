# Assertions
------------------------

## **assertTextPresentInPage**

**Description**: This function will assert if the expected text is present on the page.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | MOBILE     |:green_circle: [`assertTextPresentInPage`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE     |:green_circle: [`assertTextPresentInPage`](#)  | Sheet:Column |      | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE     |:green_circle: [`assertTextPresentInPage`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
    | MOBILE     |:green_circle: [`assertCookiePresent`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE     |:green_circle: [`assertCookiePresent`](#)   | Sheet:Column |   | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE     |:green_circle: [`assertCookiePresent`](#)   | %dynamicVar% |   | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
    | MOBILE     |:green_circle: [`assertCookieByName`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | MOBILE     |:green_circle: [`assertCookieByName`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | MOBILE     |:green_circle: [`assertCookieByName`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

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
