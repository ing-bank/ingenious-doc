---
icon: material/flask-empty-minus-outline
---

# Negative Assertions
------------------------

## **assertElementNotPresent**

**Description**: This function will assert if the Element is not present.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`assertElementNotPresent`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is not present")
    public void assertElementNotPresent() {
        assertNotElement(!elementPresent());
    }
    ```

----------------------

## **assertElementNotDisplayed**

**Description**: This function will assert if the Element is not displayed.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`assertElementNotDisplayed`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is not displayed")
    public void assertElementNotDisplayed() {
        assertNotElement(!elementDisplayed());
    }
    ```

----------------------

## **assertElementNotSelected**

**Description**: This function will assert if the Element is not selected.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`assertElementNotSelected`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is not selected")
    public void assertElementNotSelected() {
        assertNotElement(!elementSelected());
    ```

----------------------

## **assertElementNotEnabled**

**Description**: This function will assert if the Element is not enabled.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | mobileObject |:green_circle: [`assertElementNotEnabled`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Assert if [<Object>] is not enabled")
    public void assertElementNotEnabled() {
        assertNotElement(!elementEnabled());
    ```

----------------------