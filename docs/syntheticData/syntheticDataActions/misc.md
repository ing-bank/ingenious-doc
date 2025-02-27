# **Faker Actions related to Miscellaneous actions**

## **expression**

**Description**: This function will generate a random expression based on input string

**Input Format** : DatasheetName:ColumnName

**Condition Format**: expression to be evaluated, for example: `expression to be evaluated`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`expression`](#)   | DatasheetName:ColumnName      | ```expression to be evaluated```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random expression based on input string", input = InputType.YES, condition = InputType.YES)
        public void expression() {
            try {
                String strObj = Input;
                String expression = Condition;
                String evaluated = faker.get(key).expression(expression);
                Report.updateTestLog(Action, "Generated data: " + evaluated, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, evaluated);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **bothify**

**Description**: This function will generate a random expression based on input pattern

**Input Format** : DatasheetName:ColumnName

**Condition Format**: pattern to be bothified, for example: `??##??##`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`bothify`](#)   | DatasheetName:ColumnName      | ```pattern to be bothified```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random expression based on input pattern", input = InputType.YES, condition = InputType.YES)
        public void bothify() {
            try {
                String strObj = Input;
                String pattern=Condition;
                String evaluated = faker.get(key).bothify(pattern);
                Report.updateTestLog(Action, "Generated data: " + evaluated, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, evaluated);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **bothifyWithUpper**

**Description**: This function will generate a random expression based on input pattern

**Input Format** : DatasheetName:ColumnName

**Condition Format**: pattern to be bothified, for example: `??##??##`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`bothifyWithUpper`](#)   | DatasheetName:ColumnName      | ```pattern to be bothified```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random expression based on input pattern", input = InputType.YES, condition = InputType.YES)
        public void bothifyWithUpper() {
            try {
                String strObj = Input;
                String pattern=Condition;
                boolean isUpper = true;
                String evaluated = faker.get(key).bothify(pattern, isUpper);
                Report.updateTestLog(Action, "Generated data: " + evaluated, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, evaluated);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **letterify**

**Description**: This function will generate a random expression based on input pattern

**Input Format** : DatasheetName:ColumnName

**Condition Format**: pattern to be letterified, for example: `????`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`letterify`](#)   | DatasheetName:ColumnName      | ```pattern to be letterified```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random expression based on input pattern", input = InputType.YES, condition = InputType.YES)
        public void letterify() {
            try {
                String strObj = Input;
                String pattern=Condition;
                String evaluated = faker.get(key).letterify(pattern);
                Report.updateTestLog(Action, "Generated data: " + evaluated, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, evaluated);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **letterifyWithUpper**

**Description**: This function will generate a random expression based on input pattern

**Input Format** : DatasheetName:ColumnName

**Condition Format**: pattern to be letterified, for example: `?????`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`letterifyWithUpper`](#)   | DatasheetName:ColumnName      | ```pattern to be letterified```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random expression based on input pattern", input = InputType.YES, condition = InputType.YES)
        public void letterifyWithUpper() {
            try {
                String strObj = Input;
                String pattern=Condition;
                boolean isUpper = true;
                String evaluated = faker.get(key).letterify(pattern, isUpper);
                Report.updateTestLog(Action, "Generated data: " + evaluated, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, evaluated);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **numerify**

**Description**: This function will generate a random expression based on input pattern

**Input Format** : DatasheetName:ColumnName

**Condition Format**: pattern to be numerified, for example: `#####`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`numerify`](#)   | DatasheetName:ColumnName      | ```pattern to be numerified```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random expression based on input pattern", input = InputType.YES, condition = InputType.YES)
        public void numerify() {
            try {
                String strObj = Input;
                String pattern=Condition;
                String evaluated = faker.get(key).numerify(pattern);
                Report.updateTestLog(Action, "Generated data: " + evaluated, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, evaluated);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **regexify**

**Description**: This function will generate a random expression based on input pattern

**Input Format** : DatasheetName:ColumnName

**Condition Format**: pattern to be regexified, for example: `[A-za-z0-9]{8}`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`regexify`](#)   | DatasheetName:ColumnName      | ```pattern to be regexified```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random expression based on input pattern", input = InputType.YES, condition = InputType.YES)
        public void regexify() {
            try {
                String strObj = Input;
                String pattern=Condition;
                String evaluated = faker.get(key).regexify(pattern);
                Report.updateTestLog(Action, "Generated data: " + evaluated, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, evaluated);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------