# Assert Element Actions
------------------------

## **assertElementNotPresent**

**Description**: This function will assert if the Element is not present.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`assertElementNotPresent`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is not present")
    public void assertElementNotPresent() {
        assertNotElement(!elementPresent());
    }
    ```

----------------------
## **assertElementNotSelected**

**Description**: This function will assert if the Element is not selected.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`assertElementNotSelected`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is not selected")
    public void assertElementNotSelected() {
        assertNotElement(!elementSelected());
    ```

----------------------
## **assertElementNotDisplayed**

**Description**: This function will assert if the Element is not displayed.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`assertElementNotDisplayed`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is not displayed")
    public void assertElementNotDisplayed() {
        assertNotElement(!elementDisplayed());
    }
    ```

----------------------
## **assertElementNotEnabled**

**Description**: This function will assert if the Element is not enabled.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`assertElementNotEnabled`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is not enabled")
    public void assertElementNotEnabled() {
        assertNotElement(!elementEnabled());
    ```

----------------------
## **assertElementPresent**

**Description**: This function will assert if the Element is present.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | APP |:green_circle: [`assertElementPresent`](#)|                             |           |         |

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
    | APP |:green_circle: [`assertElementSelected`](#)|                             |           |         |

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
    | APP |:green_circle: [`assertElementDisplayed`](#)|                             |           |         |

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
    | APP |:green_circle: [`assertElementEnabled`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is enabled on the current page")

    public void assertElementEnabled() {
        assertElement(elementEnabled());
    }
    ```
----------------------