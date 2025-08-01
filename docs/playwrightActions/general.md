---
icon: octicons/browser-16
---

# General Actions
------------------------

## **pause**

**Description**:  This function is used to **pause** the execution for a specific duration

**Input Format** : @duration in milliseconds. Example: @`5000` - this will pause the execution for 5 seconds.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | General     |:green_circle: [`pause`](#)  |@value   | | 


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.GENERAL, desc = "Wait for [<Data>] milli seconds", input = InputType.YES)
    public void pause() {
        try {
            Thread.sleep(Long.parseLong(Data));
            Report.updateTestLog(Action, "Thread sleep for '" + Long.parseLong(Data), Status.DONE);
        } catch (Exception e) {
            Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
            Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
        }

    }
    ```   

----------------------------------------------------

## **print**

**Description**:  This function is used to **print** the Data

**Input Format** : @Value

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | General     |:green_circle: [`print`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | General     |:green_circle: [`print`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | General     |:green_circle: [`print`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>



=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.GENERAL, desc = "print the data [<Data>]", input = InputType.YES)
    public void print() {
        System.out.println(Data);
        Report.updateTestLog("print", String.format("printed %s", Data), Status.DONE);
    }
    ```   
----------------------------------------------------

## **AddVar**

**Description**:  This function is used to add variable.

**Input Format** : @Value

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | General     |:green_circle: [`AddVar`](#)   | @value       |%variableName%       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | General     |:green_circle: [`AddVar`](#)   | Sheet:Column |%variableName%       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | General     |:green_circle: [`AddVar`](#)   | %dynamicVar% |%variableName%       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>



=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.GENERAL, desc = "Add a variable to access within testcase", input = InputType.YES, condition = InputType.YES)
    public void AddVar() {        
        addVar(Condition, Data);     

        if (getVar(Condition) != null) {
            Report.updateTestLog("addVar", "Variable " + Condition + " added with value " + Data, Status.DONE);
        } else {
            Report.updateTestLog("addVar", "Variable " + Condition + " not added ", Status.DEBUG);
        }
    }
    ```   
----------------------------------------------------

## **AddGlobalVar**

**Description**:  This function is used to add global variable.

**Input Format** : @Value

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | General     |:green_circle: [`AddGlobalVar`](#)   | @value       |%globalVariableName%       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | General     |:green_circle: [`AddGlobalVar`](#)   | Sheet:Column |%globalVariableName%       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | General     |:green_circle: [`AddGlobalVar`](#)   | %dynamicVar% |%globalVariableName%       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>



=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.GENERAL, desc = "Add a Global variable to access across test set", input = InputType.YES, condition = InputType.YES)
    public void AddGlobalVar() {
        addGlobalVar(Condition, Data);
        if (getVar(Condition) != null) {
            Report.updateTestLog(Action, "Variable " + Condition
                    + " added with value " + Data, Status.DONE);
        } else {
            Report.updateTestLog(Action, "Variable " + Condition
                    + " not added ", Status.DEBUG);
        }
    }
    ```   
----------------------------------------------------

## **storeVariableInDataSheet**

**Description**: This function will **store a variable** in a data sheet

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | General     |:green_circle: [`storeVariableInDataSheet`](#)  | DatasheetName:ColumnName       |%variableName% | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.GENERAL, desc = "store variable value [<Condition>] in data sheet[<Data>]", input = InputType.YES, condition = InputType.YES)
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
-----------------------------------------------------

## **assertVariable**

**Description**:  This function will assert if the variable value matched with provided data.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | General     |:green_circle: [`assertVariable`](#)   | @%variableName%=value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>     

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.GENERAL,
            desc = "Assert if Key:Value -> [<Data>] is valid",
            input = InputType.YES)
    public void assertVariable() throws RuntimeException {
        try {
            String strObj = Data;
            String[] strTemp = strObj.split("=", 2);
            String strAns = strTemp[0].matches("%.+%") ? getVar(strTemp[0]) : strTemp[0];
            if (strAns.equals(strTemp[1])) {
                System.out.println("Condition '" + Input + "' is true ");
                Report.updateTestLog("assertVariable",
                        "Variable value matches with provided data " + strTemp[1], Status.PASSNS);

            } else {
                System.out.println("Condition '" + Input + "' is false ");
                Report.updateTestLog("assertVariable",
                        "Variable value is " + strAns + " but expected value is " + strTemp[1], Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, null, ex);
            throw new ForcedException("assertVariable", ex.getMessage());
        }
    }
    ```
----------------------------------

## **assertVariableFromDataSheet**

**Description**:  This function will assert if the variable value matches with given value from datasheet.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|    
    | General     |:green_circle: [`assertVariableFromDataSheet`](#)   | Sheet:Column | %variableName%      | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>

=== "Corresponding Code"

    ```java
        @Action(object = ObjectType.GENERAL,
            desc = "Assert if  the  variable value matches with given value from datasheet(variable:datasheet->  [<Data>] )",
            input = InputType.YES,
            condition = InputType.YES)
    public void assertVariableFromDataSheet() throws RuntimeException {
        try {
            String strAns = getVar(Condition);
            if (strAns.equals(Data)) {
                System.out.println("Variable " + Condition + " equals "
                        + Input);
                Report.updateTestLog(Action,
                        "Variable is matched with the expected result", Status.DONE);

            } else {
                System.out.println("Variable " + Condition + " is not equal "
                        + Input);
                throw new ForcedException(Action,
                        "Variable did not match with provided data");
            }
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, null, e);
            throw new ForcedException("assertVariableFromDataSheet", e.getMessage());
        }
    }
    ```
----------------------------------------
