# **Faker Actions related to Rick and Morty**

## **characterRickAndMorty**

**Description**: This function will generate a random Rick and Morty character

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`characterRickAndMorty`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Rick and Morty character", input = InputType.YES, condition = InputType.NO)
        public void characterRickAndMorty() {
            try {
                String strObj = Input;
                String character = faker.get(key).rickAndMorty().character();
                Report.updateTestLog(Action, "Generated data: " + character, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, character);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Rick and Morty character: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **locationRickAndMorty**

**Description**: This function will generate a random Rick and Morty location

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`locationRickAndMorty`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Rick and Morty location", input = InputType.YES, condition = InputType.NO)
        public void locationRickAndMorty() {
            try {
                String strObj = Input;
                String location = faker.get(key).rickAndMorty().location();
                Report.updateTestLog(Action, "Generated data: " + location, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, location);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Rick and Morty location: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **quoteRickAndMorty**

**Description**: This function will generate a random Rick and Morty quote

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`quoteRickAndMorty`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Rick and Morty quote", input = InputType.YES, condition = InputType.NO)
        public void quoteRickAndMorty() {
            try {
                String strObj = Input;
                String quote = faker.get(key).rickAndMorty().quote();
                Report.updateTestLog(Action, "Generated data: " + quote, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, quote);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Rick and Morty quote: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------