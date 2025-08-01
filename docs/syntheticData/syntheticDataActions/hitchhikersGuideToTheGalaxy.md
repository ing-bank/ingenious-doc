# **Faker Actions related to Hitchhikers Guide to the Galaxy**

## **characterHitchhiker**

**Description**: This function will generate a random character name from the Hitchhiker's Guide to the Galaxy series

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`characterHitchhiker`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random character name from the Hitchhiker's Guide to the Galaxy series", input = InputType.YES, condition = InputType.NO)
        public void characterHitchhiker() {
            try {
                String strObj = Input;
                String character = faker.get(key).hitchhikersGuideToTheGalaxy().character();
                Report.updateTestLog(Action, "Generated data: " + character, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, character);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **locationHitchhiker**

**Description**: This function will generate a random location name from the Hitchhiker's Guide to the Galaxy series

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`locationHitchhiker`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random location name from the Hitchhiker's Guide to the Galaxy series", input = InputType.YES, condition = InputType.NO)
        public void locationHitchhiker() {
            try {
                String strObj = Input;
                String location = faker.get(key).hitchhikersGuideToTheGalaxy().location();
                Report.updateTestLog(Action, "Generated data: " + location, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, location);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **marvinQuoteHitchhiker**

**Description**: This function will generate a random marvin quote from the Hitchhiker's Guide to the Galaxy series

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`marvinQuoteHitchhiker`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random marvin quote from the Hitchhiker's Guide to the Galaxy series", input = InputType.YES, condition = InputType.NO)
        public void marvinQuoteHitchhiker() {
            try {
                String strObj = Input;
                String quote = faker.get(key).hitchhikersGuideToTheGalaxy().marvinQuote();
                Report.updateTestLog(Action, "Generated data: " + quote, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, quote);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **quoteHitchhiker**

**Description**: This function will generate a random quote from the Hitchhiker's Guide to the Galaxy series

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`quoteHitchhiker`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random quote from the Hitchhiker's Guide to the Galaxy series", input = InputType.YES, condition = InputType.NO)
        public void quoteHitchhiker() {
            try {
                String strObj = Input;
                String quote = faker.get(key).hitchhikersGuideToTheGalaxy().quote();
                Report.updateTestLog(Action, "Generated data: " + quote, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, quote);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **planetHitchhiker**

**Description**: This function will generate a random planet name from the Hitchhiker's Guide to the Galaxy series

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`planetHitchhiker`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random planet name from the Hitchhiker's Guide to the Galaxy series", input = InputType.YES, condition = InputType.NO)
        public void planetHitchhiker() {
            try {
                String strObj = Input;
                String planet = faker.get(key).hitchhikersGuideToTheGalaxy().planet();
                Report.updateTestLog(Action, "Generated data: " + planet, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, planet);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **specieHitchhiker**

**Description**: This function will generate a random species name from the Hitchhiker's Guide to the Galaxy series

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`specieHitchhiker`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random species name from the Hitchhiker's Guide to the Galaxy series", input = InputType.YES, condition = InputType.NO)
        public void specieHitchhiker() {
            try {
                String strObj = Input;
                String species = faker.get(key).hitchhikersGuideToTheGalaxy().specie();
                Report.updateTestLog(Action, "Generated data: " + species, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, species);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **starshipHitchhiker**

**Description**: This function will generate a random starship from the Hitchhiker's Guide to the Galaxy series

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`starshipHitchhiker`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random starship from the Hitchhiker's Guide to the Galaxy series", input = InputType.YES, condition = InputType.NO)
        public void starshipHitchhiker() {
            try {
                String strObj = Input;
                String starShip = faker.get(key).hitchhikersGuideToTheGalaxy().starship();
                Report.updateTestLog(Action, "Generated data: " + starShip, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, starShip);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------