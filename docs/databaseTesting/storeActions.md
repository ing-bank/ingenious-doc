# Store Actions

## **storeDBValueinDataSheet**

**Description**: This action will store the value of a specific cell(from specific row and column) from the result of an SQL select statement in the data sheet

**Input Format** : @SheetName:ColumnName , Condition : DatabaseColumnName, ResultSetRowNumber

=== "Usage"

    | ObjectName | Action | Input          | Condition        |
    |------------|----------------|------------------|---|
    | Database   | :green_circle: [`storeDBValueinDataSheet`](#) | DatasheetName:ColumnName  | DatabaseColumnName, ResultSetRowNumber   |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Save DB value in Test Data Sheet", input = InputType.YES, condition = InputType.YES)
        public void storeDBValueinDataSheet() {
            try {
                if (Condition != null && Input != null) {
                    int rowIndex = 1;
                    result.first();
                    String[] sheetDetail = Input.split(":");
                    String sheetName = sheetDetail[0];
                    String columnName = sheetDetail[1];
                    String value;
                    String[] split = Condition.split(",");
                    if (split.length > 1) {
                        rowIndex = Integer.parseInt(split[1]);
                    }
                    if (!result.absolute(rowIndex)) {
                        Report.updateTestLog(Action, "Row : " + rowIndex + " doesn't exist ", Status.FAILNS);
                    } else if (getColumnIndex(split[0]) != -1) {
                        value = result.getString(split[0]);
                        userData.putData(sheetName, columnName, value);
                        Report.updateTestLog(Action, "Value from DB " + value + "  stored into " + "the data sheet", Status.DONE);
                    } else {
                        Report.updateTestLog(Action, "Column : " + split[0] + " doesn't exist", Status.FAILNS);
                    }
                } else {
                    Report.updateTestLog(Action, "Incorrect Input or Condition format", Status.FAILNS);
                }
            } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error: " + ex.getMessage(), Status.FAILNS);
                System.out.println("Invalid Data " + Condition);
            }
        }

    ```

## **storeValueInVariable**

**Description**: This action will store the value of a specific cell(from specific row and column) from the result of an SQL select statement in a user defined variable

**Input Format** : %variableName% , Condition : DatabaseColumnName,ResultSetRowNumber

=== "Usage"

    | ObjectName | Action |Input        | Condition          |
    |------------|--------------|--------------------|---|
    | Database   | :green_circle: [`storeValueInVariable`](#) | %variableName%        | DatabaseColumnName,ResultSetRowNumber     |

=== "Corresponding Code"

    ```java

    @Action(object = ObjectType.DATABASE, desc = "Store it in the variable from the DB column [<Condition>] ", input = InputType.YES, condition = InputType.YES)
        public void storeValueInVariable() {
            storeValue(Input, Condition, false);
            if (getVar(Input) != null && !getVar(Input).equals("")) {
                Report.updateTestLog(Action, "Stored in the variable", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Value doesn't stored in Global variable", Status.FAILNS);
            }
        }

    ```

## **storeValueInGlobalVariable**

**Description**: This action will store the value of a specific cell(from specific row and column) from the result of an SQL select statement in global variable

**Input Format** : %variableName% , Condition : DatabaseColumnName,ResultSetRowNumber

=== "Usage"

    | ObjectName | Action | Input        | Condition       |
    |------------|--------------|-----------------|----|
    | Database   | :green_circle: [`storeValueInGlobalVariable`](#) | %variableName%        | DatabaseColumnName,ResultSetRowNumber  |

=== "Corresponding Code"

    ```java

    @Action(object = ObjectType.DATABASE, desc = "Store it in Global variable from the DB column [<Condition>] ", input = InputType.YES, condition = InputType.YES)
        public void storeValueInGlobalVariable() {
            storeValue(Input, Condition, true);
            if (getVar(Input) != null && !getVar(Input).equals("")) {
                Report.updateTestLog(Action, "Stored in Global variable", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Value doesn't stored in Global variable", Status.FAILNS);
            }
        }

    ```

## **storeResultInDataSheet**

**Description**:  This action will store the result of an SQL select statement in the test data sheet

**Input Format** : @`SQL Query` , Condition : DatasheetName

=== "Usage"

    | ObjectName | Action | Input                            | Condition |
    |------------|----------------------------------|-----------|----|
    | Database   | :green_circle: [`storeResultInDataSheet`](#) | ```@select designation from job where id=121;```  | DatasheetName |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Query and save the result in Datasheet ", input = InputType.YES, condition = InputType.YES)
        public void storeResultInDataSheet() {
            try {
                executeSelect();
                result.last();
                int totalRows = result.getRow();
                result.beforeFirst();
                int totalCols = resultData.getColumnCount();
                for (int colIndex = 0; colIndex < totalCols; colIndex++) {
                    result.beforeFirst();
                    for (int rowIndex = 1; rowIndex <= totalRows; rowIndex++) {
                        if (result.absolute(rowIndex)) {
                            userData.putData(Condition, colNames.get(colIndex), result.getString(colIndex + 1), userData.getIteration(), Integer.toString(rowIndex));
                        } else {
                            Report.updateTestLog(Action, "Row " + rowIndex + " doesn't exist",
                                Status.FAILNS);
                            return;
                        }
                    }
                }
                Report.updateTestLog(Action, " SQL Query Result has been saved in DataSheet: ",
                    Status.PASSNS);
                } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error executing the SQL Query: " + ex.getMessage(),
                    Status.FAILNS);
            }
        }

    ```

## **storeResultInVariable**

**Description**: This action will store the result of an SQL select statement in a user defined variable. The select query in this case should return a single column, the query may return multiple rows. In case the query returns a single value, the value will be stored in the variable name given (for eg:- var), In case if the select query returns multiple rows, multiple variables will be created by adding indexes to the variable name given and the value will be stored in these variables(for eg:- var1, var2, var3.....)

**Input Format** : @`SQL Query` , Condition : %VariableName% 

=== "Usage"

    | ObjectName | Action | Input                             | Condition |
    |------------|-----------------------------------|-----------|----|
    | Database   | :green_circle: [`storeResultInVariable`](#) | ```@@select designation from job where id=121;"```   | %variableName%     |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Query and save the result in variable(s) ", input = InputType.YES, condition = InputType.YES)
        public void storeResultInVariable() {
            String variableName = Condition;
            try {
                executeSelect();
                result.last();
                int totalRows = result.getRow();
                result.beforeFirst();
                for (int index = 1; index <= totalRows; index++) {
                    if (result.absolute(index)) {
                        if (index == 1) {
                            addVar(variableName, result.getString(1));
                        } else {
                            String temp = variableName.replaceAll("[%]$", index + "%");
                            addVar(temp, result.getString(1));
                        }
                    } else {
                        Report.updateTestLog(Action, "Row " + index + " doesn't exist",
                            Status.FAILNS);
                        return;
                    }
                }
                Report.updateTestLog(Action, " SQL Query Result has been saved in the run time variable(s) ",
                    Status.PASSNS);
            } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error executing the SQL Query: " + ex.getMessage(),
                    Status.FAILNS);
            }
        }
    ```
