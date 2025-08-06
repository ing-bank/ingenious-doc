# **Faker Actions related to Team**

## **teamName**

**Description**: This function will generate a random team name

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`teamName`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random team name", input = InputType.YES, condition = InputType.NO)
        public void teamName() {
            try {
                String strObj = Input;
                String teamName = faker.get(key).team().name();
                Report.updateTestLog(Action, "Generated data: " + teamName, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, teamName);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating team name: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **teamSport**

**Description**: This function will generate a random team sport

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`teamSport`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random team sport", input = InputType.YES, condition = InputType.NO)
        public void teamSport() {
            try {
                String strObj = Input;
                String sport = faker.get(key).team().sport();
                Report.updateTestLog(Action, "Generated data: " + sport, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, sport);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating team sport: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **teamState**

**Description**: This function will generate a random team state

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`teamState`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random team state", input = InputType.YES, condition = InputType.NO)
        public void teamState() {
            try {
                String strObj = Input;
                String state = faker.get(key).team().state();
                Report.updateTestLog(Action, "Generated data: " + state, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, state);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating team mascot: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **teamCreature**

**Description**: This function will generate a random team creature

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`teamCreature`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random team creature", input = InputType.YES, condition = InputType.NO)
        public void teamCreature() {
            try {
                String strObj = Input;
                String creature = faker.get(key).team().creature();
                Report.updateTestLog(Action, "Generated data: " + creature, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, creature);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating team member: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------