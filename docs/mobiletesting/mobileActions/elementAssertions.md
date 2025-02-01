# **Element Assertions** 

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