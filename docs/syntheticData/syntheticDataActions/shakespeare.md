# **Faker Actions related to Shakespeare**

## **quoteHamlet**

**Description**: This function will generate a random Hamlet quote

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`quoteHamlet`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Hamlet quote", input = InputType.YES, condition = InputType.NO)
        public void quoteHamlet() {
            try {
                String strObj = Input;
                String hamletQuote = faker.get(key).shakespeare().hamletQuote();
                Report.updateTestLog(Action, "Generated data: " + hamletQuote, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, hamletQuote);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Hamlet quote: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **quoteAsYouLikeIt**

**Description**: This function will generate a random As You Like It quote

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`quoteAsYouLikeIt`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random As You Like It quote", input = InputType.YES, condition = InputType.NO)
        public void quoteAsYouLikeIt() {
            try {
                String strObj = Input;
                String asYouLikeItQuote = faker.get(key).shakespeare().asYouLikeItQuote();
                Report.updateTestLog(Action, "Generated data: " + asYouLikeItQuote, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, asYouLikeItQuote);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating As You Like It quote: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **quoteKingRichard**

**Description**: This function will generate a random King Richard III quote

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`quoteKingRichard`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random King Richard III quote", input = InputType.YES, condition = InputType.NO)
        public void quoteKingRichard() {
            try {
                String strObj = Input;
                String kingRichardQuote = faker.get(key).shakespeare().kingRichardIIIQuote();
                Report.updateTestLog(Action, "Generated data: " + kingRichardQuote, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, kingRichardQuote);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating King Richard III quote: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **quoteRomeoAndJuliet**

**Description**: This function will generate a random Romeo and Juliet quote

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`quoteRomeoAndJuliet`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Romeo and Juliet quote", input = InputType.YES, condition = InputType.NO)
        public void quoteRomeoAndJuliet() {
            try {
                String strObj = Input;
                String romeoAndJulietQuote = faker.get(key).shakespeare().romeoAndJulietQuote();
                Report.updateTestLog(Action, "Generated data: " + romeoAndJulietQuote, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, romeoAndJulietQuote);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Romeo and Juliet quote: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------