# **Faker Actions related to How I met your mother**

## **characterHowIMetYourMother**

**Description**: This function will generate a random character name from How I Met Your Mother

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`characterHowIMetYourMother`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random character name from How I Met Your Mother", input = InputType.YES, condition = InputType.NO)
        public void characterHowIMetYourMother() {
            try {
                String strObj = Input;
                String character = faker.get(key).howIMetYourMother().character();
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

## **quoteHowIMetYourMother**

**Description**: This function will generate a random quote from How I Met Your Mother

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`quoteHowIMetYourMother`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random quote from How I Met Your Mother", input = InputType.YES, condition = InputType.NO)
        public void quoteHowIMetYourMother() {
            try {
                String strObj = Input;
                String quote = faker.get(key).howIMetYourMother().quote();
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

## **catchPhraseHowIMetYourMother**

**Description**: This function will generate a random catchphrase from How I Met Your Mother

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`catchPhraseHowIMetYourMother`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random catchphrase from How I Met Your Mother", input = InputType.YES, condition = InputType.NO)
        public void catchPhraseHowIMetYourMother() {
            try {
                String strObj = Input;
                String catchphrase = faker.get(key).howIMetYourMother().catchPhrase();
                Report.updateTestLog(Action, "Generated data: " + catchphrase, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, catchphrase);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **highFiveHowIMetYourMother**

**Description**: This function will generate a random high five from How I Met Your Mother

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`highFiveHowIMetYourMother`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random high five from How I Met Your Mother", input = InputType.YES, condition = InputType.NO)
        public void highFiveHowIMetYourMother() {
            try {
                String strObj = Input;
                String highFive = faker.get(key).howIMetYourMother().highFive();
                Report.updateTestLog(Action, "Generated data: " + highFive, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, highFive);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------