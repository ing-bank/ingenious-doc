# General Actions

## **initDBConnection**

**Description**: This function will initialize the database connection

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Database   |:green_circle: [`initDBConnection`](#)| | |  |

=== "Corresponding Code"

    Performs connection of Database 

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Initiate the DB transaction")
        public void initDBConnection() {
            try {
                if (verifyDbConnection()) {
                    DatabaseMetaData metaData = dbconnection.getMetaData();
                    Report.updateTestLog(Action, " Connected with " + metaData.getDriverName() + "\n"
                        + "Driver version " + metaData.getDriverVersion() + " \n"
                        + "Database product name " + metaData.getDatabaseProductName() + "\n"
                        + "Database product version " + metaData.getDatabaseProductVersion(),
                        Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Could not able to make DB connection ", Status.FAILNS);
                }
                } catch (ClassNotFoundException | SQLException ex) {
                    Report.updateTestLog(Action, "Error connecting Database: " + ex.getMessage(),
                    Status.FAILNS);
            }
        }

    Internally uses the following Java logic :

        Class.forName(dbDriver);
        if (dbConnectionString != null && dbUser != null && dbPass != null) {
            dbconnection = DriverManager.getConnection(dbConnectionString, dbUser,dbPass);
        } else if (dbConnectionString != null) {
            dbconnection = DriverManager.getConnection(dbConnectionString);
        }
    ```
----------------------

## **closeDBConnection**

**Description**: This function will close the database connection

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|
    |------------|--------|--------------|-----------|---------|
    | Database   |:green_circle: [`closeDBConnection`](#)| | |  |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Close the DB Connection")
        public void closeDBConnection() {
            try {
                if (closeConnection()) {
                    Report.updateTestLog(Action, "DB Connection is closed", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Error in closing the DB Connection ", Status.FAILNS);
                }
            } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error: " + ex.getMessage(),
                    Status.FAILNS);
            }
        }

    Internally uses the following Java logic :

        dbconnection.close();
        statement.close();
        result.close();
    ```
----------------------

## **assertDBResult**

**Description**: This function will assert if the SQL result equals/exact match a particular data in a specific column after the execution of a SQL select statement.

**Input Format** : @ExpectedValue

**Condition** : Name of the column in which result is expected

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Database     |:green_circle: [`assertDBResult`](#)   | @Data       | nameOfDBColumn | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Database     |:green_circle: [`assertDBResult`](#)   | DatasheetName:ColumnName | nameOfDBColumn | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Database     |:green_circle: [`assertDBResult`](#)   | %variableName% | nameOfDBColumn | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Assert the value [<Input>] exist in the column [<Condition>] ", input = InputType.YES, condition = InputType.YES)
        public void assertDBResult() {
            if (assertDB(Condition, Data)) {
                Report.updateTestLog(Action, "Value " + Data + " exist in the Database", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Value " + Data + " doesn't exist in the Database", Status.FAILNS);
            }
        }

    public boolean assertDB(String columnName, String condition) {
        boolean isExist = false;
        try {
            result.beforeFirst();
            if (getColumnIndex(columnName) != -1) {
                while (result.next()) {
                    if (Objects.equal(result.getString(columnName), condition)) {
                        isExist = true;
                        break;
                    }
                }
            } else {
                Report.updateTestLog(Action, "Column " + columnName + " doesn't exist", Status.FAIL);
            }
        } catch (SQLException ex) {
            Report.updateTestLog(Action, "Error asserting the value in DB " + ex.getMessage(), Status.FAIL);
            return false;
        }
        return isExist;
        }

    ```

## **executeSelectQuery**

**Description**: This function will execute the given select query on the database

**Input Format** : @`SQL Query`

=== "Usage"

    | ObjectName | Action | Input                            | Condition |
    |------------|--------|-----------|-------|
    | Database   | :green_circle: [`executeSelectQuery`](#) | ``` @select designation from job where id=121;```      |           |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Execute the Query in [<Input>]", input = InputType.YES)
        public void executeSelectQuery() {
            try {
                executeSelect();
                Report.updateTestLog(Action, "Executed Select Query", Status.DONE);
            } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error executing the SQL Query: " + ex.getMessage(),
                    Status.FAILNS);
            }   
        }

        public void executeSelect() throws SQLException {
            initialize();
            result = statement.executeQuery(Data);
            resultData = result.getMetaData();
            populateColumnNames();
        }    

    ```

## **executeDMLQuery**

**Description**:  This query will execute an SQL DML statement on the database and will commit the results back to the database

**Input Format** : @`SQL Query`

=== "Usage"

    | ObjectName | Action | Input                                                     | Condition    |
    |------------|-----------------------------------------------------------|--------------|---|
    | Database   | :green_circle: [`executeDMLQuery`](#) |```@UPDATE job SET "designation"=Tester WHERE id = 121;``` |              |
    | Database	 | :green_circle: [`executeDMLQuery`](#) |Sheet:Column                                              |          	|  
    | Database   | :green_circle: [`executeDMLQuery`](#) |%dynamicVar%                                              |              |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Execute the Query in [<Input>]", input = InputType.YES)
        public void executeDMLQuery() {
            try {
                if (executeDML()) {
                    Report.updateTestLog(Action, " Table updated by using " + Data, Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, " Table not updated by using " + Data, Status.FAILNS);
                }
            } catch (SQLException ex) {
                Report.updateTestLog(Action, "Error executing the SQL Query: " + ex.getMessage(),
                    Status.FAILNS);
            }
        }   

    ```

----------------------

## **executeStoredProcedureQuery()**

**Description**:  This query will execute an PL/SQL stored procedure call provided in the Data field on  database and will commit the results back to the database

**Input Format** : @`Stored Procedure Call`

=== "Usage"

    | ObjectName | Action | Input                                                                       | Condition    |
    |------------|-----------------------------------------------------------|--------------------------|--------------|
    | Database   | :green_circle: [`executeStoredProcedureQuery`](#) |```@Begin  addemployee29; end; ``` |             |
    | Database	 | :green_circle: [`executeStoredProcedureQuery`](#) |Sheet:Column                       |             |  
    | Database   | :green_circle: [`executeStoredProcedureQuery`](#) |%dynamicVar%                       |             |

=== "Corresponding Code"

```java
   @Action(object = ObjectType.DATABASE, desc = "Execute the StoredProcedure Query in [<Input>]", input = InputType.YES)
      public void executeStoredProcedureQuery() {
        try {
            String trimmedData = (Data != null) ? Data.trim() : "";
            int beginCount = trimmedData.toLowerCase().split("begin", -1).length - 1;
            int endCount = trimmedData.toLowerCase().split("end", -1).length - 1;
            int semicolonCount = trimmedData.length() - trimmedData.replace(";", "").length();
            if (beginCount > 1 || endCount > 1 || semicolonCount > 1) {
                Report.updateTestLog(Action, "Invalid stored procedure input: Only a single stored procedure call is allowed.                    Input: " + Data, Status.FAILNS);
                return;
            }
            if (executeStoredProcedure()) {
                Report.updateTestLog(Action, "StoredProcedure operation successful using: " + Data, Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "StoredProcedure operation failed using: " + Data, Status.FAILNS);
            }
        } catch (SQLException ex) {
            Report.updateTestLog(Action, "Error executing the StoredProcedure Query: " + ex.getMessage(),
                    Status.FAILNS);
        }
    }

```
----------------------
## **assertDBResultContains**

**Description**: This function will assert if the SQL result contains/partial text match expected data after the execution of a SQL select statement.

**Input Format** : @ExpectedValue

**Condition** : Name of the DB column in which actual result is expected

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Database     |:green_circle: [`assertDBResultContains`](#)   | @Data       | nameOfDBColumn | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Database     |:green_circle: [`assertDBResultContains`](#)   | DatasheetName:ColumnName | nameOfDBColumn | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Database     |:green_circle: [`assertDBResultContains`](#)   | %variableName% | nameOfDBColumn | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
   @Action(object = ObjectType.DATABASE, desc = "Assert the value [<Input>] contains in the column [<Condition>] ", input = InputType.YES, condition = InputType.YES)
    public void assertDBResultContains() {
        if (Data == null || Data.trim().isEmpty()) {
            Report.updateTestLog(Action, "Expected value is null or empty, cannot perform contains check", Status.FAILNS);
            return;
        }
        if (assertDBContains(Condition, Data)) {
            Report.updateTestLog(Action, "Value " + Data + " exists in the Database (contains match)", Status.PASSNS);
        } else {
            Report.updateTestLog(Action, "Value " + Data + " does not exist in the Database (contains match)", Status.FAILNS);
        }
    }

    ```

     ----------------------
## **assertDBDataNotNull**

**Description**: This function will assert if the SQL result is not null or empty  after the execution of a SQL select statement.

**Input Format** : @ActualValue

**Condition** : Not used in this action

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Database     |:green_circle: [`assertDBDataNotNull`](#)   | @Data       | nameOfDBColumn | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Database     |:green_circle: [`assertDBDataNotNull`](#)   | DatasheetName:ColumnName | nameOfDBColumn | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Database     |:green_circle: [`assertDBDataNotNull`](#)   | %variableName% | nameOfDBColumn | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
  @Action(object = ObjectType.DATABASE, desc = "Assert DB Data Data Not Null ", input = InputType.YES)
    public void assertDBDataNotNull() {
        try {

            if (Data == null || Data.trim().isEmpty()) {
                Report.updateTestLog(Action, "DB column [" + Data + "]is null or empty ", Status.FAILNS);

            } else {
                Report.updateTestLog(Action, "DB column [" + Data + "] is not null or empty ", Status.PASSNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating DB Data is not null :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    ```
               ----------------------
## **assertDBDataStartsWith**

**Description**: This function will assert if the SQL result matches the startswith/prefix Data after the execution of a SQL select statement.

**Input Format** : @ExpectedValue - Prefix

**Condition** : Actual Value of the DB column  which is actual result 

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Database     |:green_circle: [`assertDBDataStartsWith`](#)   | @Data       | %ActualValueVariableName% or ActualValue | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Database     |:green_circle: [`assertDBDataStartsWith`](#)   | DatasheetName:ColumnName | %ActualValueVariableName% or ActualValue  | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Database     |:green_circle: [`assertDBDataStartsWith`](#)   | %variableName% | %ActualValueVariableName% or ActualValue  | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
   @Action(object = ObjectType.DATABASE, desc = "Assert DB Data Starts With ", input = InputType.YES, condition = InputType.YES)
    public void assertDBDataStartsWith() {
        try {

            String prefix = Data;
            String value;
            if (Condition != null && (Condition.startsWith("%") || Condition.endsWith("%"))) {
                value = getVar(Condition);
            } else {
                value = Condition;
            }
            if (value != null && value.startsWith(prefix)) {
                Report.updateTestLog(Action, "DB column [" + value + "] starts with [" + Data + "]", Status.PASSNS);

            } else {
                Report.updateTestLog(Action, "DB column [" + value + "]doesn't start with [" + Data + "]", Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating DB Data prefix :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    ```
                   ----------------------
## **assertDBDataPattern**

**Description**: This function will assert if the SQL result matches the pattern/regular expression after the execution of a SQL select statement.

**Input Format** : @ExpectedValue - Pattern/regular expression

**Condition** : Actual Value of the DB column  which is actual result 

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Database     |:green_circle: [`assertDBDataPattern`](#)   | @Data       | %ActualValueVariableName% or ActualValue | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | Database     |:green_circle: [`assertDBDataPattern`](#)   | DatasheetName:ColumnName | %ActualValueVariableName% or ActualValue | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | Database     |:green_circle: [`assertDBDataPattern`](#)   | %variableName% | %ActualValueVariableName% or ActualValue | |<span style="color:Brown"><<*Input from variable*</span>

=== "Corresponding Code"

    ```java
   @Action(object = ObjectType.DATABASE, desc = "Assert DB Data Pattern ", input = InputType.YES, condition = InputType.YES)
    public void assertDBDataPattern() {
        try {

            String pattern = Data;
            String value;
            if (Condition != null && (Condition.startsWith("%") || Condition.endsWith("%"))) {
                value = getVar(Condition);
            } else {
                value = Condition;
            }
            if (value != null && value.matches(pattern)) {
                Report.updateTestLog(Action, "DB column [" + value + "] matches the pattern [" + Data + "]", Status.PASSNS);

            } else {
                Report.updateTestLog(Action, "DB column [" + value + "]doesn't match the  pattern [" + Data + "]", Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating DB Data Pattern :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    ```
