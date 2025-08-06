# **Faker Actions related to Phone Number**

## **phoneNumber**

**Description**: This function will generate a random phone number

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`phoneNumber`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random phone number", input = InputType.YES, condition = InputType.NO)
        public void phoneNumber() {
            try {
                String strObj = Input;
                String phoneNumber = faker.get(key).phoneNumber().phoneNumber();
                Report.updateTestLog(Action, "Generated data: " + phoneNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, phoneNumber);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating phone number: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **cellPhone**

**Description**: This function will generate a random cell phone number

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`cellPhone`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random cell phone number", input = InputType.YES, condition = InputType.NO)
        public void cellPhone() {
            try {
                String strObj = Input;
                String phoneNumber = faker.get(key).phoneNumber().cellPhone();
                Report.updateTestLog(Action, "Generated data: " + phoneNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, phoneNumber);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating phone number: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------