# **Relative Actions** 

## **Tap_Relative**

**Description**: This function will tap on element based on parent object

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`Tap_Relative`](#)   |        |  | PageName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Tap on element based on parent [<Object>]", condition = InputType.YES)
    public void Tap_Relative() {
        doRelative(RelativeAction.TAP);
    }
    ```
----------------------

## **set_Relative**

**Description**: This function will set given data from input column on element baseb on parent object

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`set_Relative`](#)   | @Data       |  | PageName |<span style="color:Green"><< *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`set_Relative`](#)   | DatasheetName:ColumnName |  | PageName |<span style="color:Blue"><< *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`set_Relative`](#)   | %variableName% |  | PageName |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Set [<Data>] on element based on parent [<Object>]", input = InputType.YES, condition = InputType.YES)
    public void set_Relative() {
        doRelative(RelativeAction.SET);
    }
    ```
----------------------
