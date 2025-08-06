# **Faker Actions related to Stock**

## **nyseSymbol**

**Description**: This function will generate a random stock ticker symbol from the NYSE exchange

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`nyseSymbol`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random stock ticker symbol from the NYSE exchange", input = InputType.YES, condition = InputType.NO)
        public void nyseSymbol() {
            try {
                String strObj = Input;
                String nyse = faker.get(key).stock().nyseSymbol();
                Report.updateTestLog(Action, "Generated data: " + nyse, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, nyse);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating NYSE stock symbol: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **nsdqSymbol**

**Description**: This function will generate a random stock ticker symbol from the NSDQ exchange

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`nsdqSymbol`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random stock ticker symbol from the NSDQ exchange", input = InputType.YES, condition = InputType.NO)
        public void nsdqSymbol() {
            try {
                String strObj = Input;
                String nsdq = faker.get(key).stock().nsdqSymbol();
                Report.updateTestLog(Action, "Generated data: " + nsdq, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, nsdq);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating NYSE stock symbol: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------