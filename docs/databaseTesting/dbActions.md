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

**Description**: This function will assert if the SQL result contains a particular data in a specific column after the execution of a SQL select statement.

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
    | Database   | :green_circle: [`executeSelectQuery`](#) | ``` @select * from tableName ```      |           |

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
    | Database   | :green_circle: [`executeDMLQuery`](#) |```@UPDATE public."Employee" SET "Age"=27 WHERE id = 123456;``` |              |
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


## **verifyWithDataSheet**

**Description**: Verify Table values with the Test Data sheet

**Input Format** : @`SQL Query`

=== "Usage"

    | ObjectName | Action | Input                             | Condition |
    |------------|-----------------------------------|-----------|----|
    | Database   | :green_circle: [`verifyWithDataSheet`](#) | ```@select * from public."Employee" ```  | %variableName%     |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.DATABASE, desc = "Verify Table values with the Test Data sheet ", input = InputType.YES)
        public void verifyWithDataSheet() {
            String sheetName = Data;
            TestDataView dataView;
            if (!sheetName.isEmpty() && (dataView = userData.getTestData(sheetName)) != null) {
                List<String> columns = dataView.columns();
                boolean isFailed = false;
                StringBuilder desc = new StringBuilder();
                for (String column : columns.subList(4, columns.size())) {
                    if (assertDB(column, dataView.getField(column))) {
                        desc.append("Value ").append(userData.getData(sheetName, column)).append(" exist in the Database").append("\n");
                    } else {
                        isFailed = true;
                        desc.append("Value ").append(userData.getData(sheetName, column)).append(" doesn't exist in the Database").append("\n");
                    }
                }
                Report.updateTestLog(Action, desc.toString(), isFailed ? Status.FAILNS : Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Incorrect Sheet Name", Status.FAILNS);
            }
        }
    ```
