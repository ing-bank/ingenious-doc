# **Faker Actions related to Weather**

## **weatherDescription**

**Description**: This function will generate a random weather description

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`weatherDescription`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random weather description", input = InputType.YES, condition = InputType.NO)
        public void weatherDescription() {
            try {
                String strObj = Input;
                String description = faker.get(key).weather().description();
                Report.updateTestLog(Action, "Generated data: " + description, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, description);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating weather description: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **temperatureCelsius**

**Description**: This function will generate a random temperature in Celsius

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`temperatureCelsius`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random temperature in Celsius", input = InputType.YES, condition = InputType.NO)
        public void temperatureCelsius() {
            try {
                String strObj = Input;
                String temperature = faker.get(key).weather().temperatureCelsius();
                Report.updateTestLog(Action, "Generated data: " + temperature, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, temperature);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating temperature: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **temperatureFahrenheit**

**Description**: This function will generate a random temperature in Fahrenheit

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`temperatureFahrenheit`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random temperature in Fahrenheit", input = InputType.YES, condition = InputType.NO)
        public void temperatureFahrenheit() {
            try {
                String strObj = Input;
                String temperature = faker.get(key).weather().temperatureFahrenheit();
                Report.updateTestLog(Action, "Generated data: " + temperature, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, temperature);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating humidity: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **temperatureCelsiusWithinRange**

**Description**: This function will generate a random temperature in Celsius within a range

**Input Format** : DatasheetName:ColumnName

**Condition Format**: celcius range, for example: `35:50`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`temperatureCelsiusWithinRange`](#)   | DatasheetName:ColumnName      | ```celcius range```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random temperature in Celsius within a range", input = InputType.YES, condition = InputType.YES)
        public void temperatureCelsiusWithinRange() {
            try {
                String strObj = Input;
                String minTempStr = Condition.split(":", 2)[0];
                String maxTempStr = Condition.split(":", 3)[1];
                int minTemp=Integer.parseInt(minTempStr);
                int maxTemp=Integer.parseInt(maxTempStr);
                String temperature = faker.get(key).weather().temperatureCelsius(minTemp, maxTemp);
                Report.updateTestLog(Action, "Generated data: " + temperature, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, temperature);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating temperature: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **temperatureFahrenheitWithinRange**

**Description**: This function will generate a random temperature in Fahrenheit within a range

**Input Format** : DatasheetName:ColumnName

**Condition Format**: Farenheit range, for example: `95:109`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`temperatureFahrenheitWithinRange`](#)   | DatasheetName:ColumnName      | ```Farenheit range```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random temperature in Fahrenheit within a range", input = InputType.YES, condition = InputType.YES)
        public void temperatureFahrenheitWithinRange() {
            try {
                String strObj = Input;
                String minTempStr = Condition.split(":", 2)[0];
                String maxTempStr = Condition.split(":", 3)[1];
                int minTemp=Integer.parseInt(minTempStr);
                int maxTemp=Integer.parseInt(maxTempStr);
                String temperature = faker.get(key).weather().temperatureFahrenheit(minTemp, maxTemp);
                Report.updateTestLog(Action, "Generated data: " + temperature, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, temperature);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating humidity: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------