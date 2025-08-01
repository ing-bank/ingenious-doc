# **Faker Actions related to Chunk Norris Fact**

## **chuckNorrisFact**

**Description**: This function will generate a random chuck Norris Fact

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`chuckNorrisFact`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Chuck Norris fact", input = InputType.YES, condition = InputType.NO)
        public void chuckNorrisFact() {
            try {
                String strObj = Input;
                String chuckNorrisFact = faker.get(key).chuckNorris().fact();
                Report.updateTestLog(Action, "Generated data: " + chuckNorrisFact, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, chuckNorrisFact);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------