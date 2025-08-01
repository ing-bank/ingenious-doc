# **Faker Actions related to Random Service**

## **randomHex**

**Description**: This function will generate a random hex

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomHex`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random hex", input = InputType.YES, condition = InputType.NO)
        public void randomHex() {
            try {
                String strObj = Input;
                String hex = faker.get(key).random().hex();
                Report.updateTestLog(Action, "Generated data: " + hex, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, hex);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random integer: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomHexWithLength**

**Description**: This function will generate a random hex with specified length

**Input Format** : DatasheetName:ColumnName

**Condition Format**: length, for example: `10`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomHexWithLength`](#)   | DatasheetName:ColumnName      | ```length```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random hex with specified length", input = InputType.YES, condition = InputType.YES)
        public void randomHexWithLength() {
            try {
                String strObj = Input;
                String lengthStr = Condition;
                int length=Integer.parseInt(lengthStr);
                String hex = faker.get(key).random().hex(length);
                Report.updateTestLog(Action, "Generated data: " + hex, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, hex);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random integer: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomNextIntWithLength**

**Description**: This function will generate a random integer with length

**Input Format** : DatasheetName:ColumnName

**Condition Format**: number, for example: `5`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomNextIntWithLength`](#)   | DatasheetName:ColumnName      | ```number```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random integer with length", input = InputType.YES, condition = InputType.YES)
        public void randomNextIntWithLength() {
            try {
                String strObj = Input;
                String numStr = Condition;
                int num = Integer.parseInt(numStr);
                int randomInt = faker.get(key).random().nextInt(num);
                Report.updateTestLog(Action, "Generated data: " + randomInt, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Integer.toString(randomInt));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random integer in range: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomNextIntInRange**

**Description**: This function will generate a random integer within a range

**Input Format** : DatasheetName:ColumnName

**Condition Format**: minimum and maximum range, for example: `880:990`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomNextIntInRange`](#)   | DatasheetName:ColumnName      | ```minimum and maximum range```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random integer within a range", input = InputType.YES, condition = InputType.YES)
        public void randomNextIntInRange() {
            try {
                String strObj = Input;
                String minStr = Condition.split(":", 2)[0];
                String maxStr = Condition.split(":", 2)[1];
                int min=Integer.parseInt(minStr);
                int max=Integer.parseInt(maxStr);
                int randomInt = faker.get(key).random().nextInt(min, max);
                Report.updateTestLog(Action, "Generated data: " + randomInt, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Integer.toString(randomInt));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random integer in range: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomNextLong**

**Description**: This function will generate a random long number

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomNextLong`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random long number", input = InputType.YES, condition = InputType.NO)
        public void randomNextLong() {
            try {
                String strObj = Input;
                long randomLong = faker.get(key).random().nextLong();
                Report.updateTestLog(Action, "Generated data: " + randomLong, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Long.toString(randomLong));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random long: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomNextLongWithLength**

**Description**: This function will generate a random long number with length

**Input Format** : DatasheetName:ColumnName

**Condition Format**: long number, for example: `15`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomNextLongWithLength`](#)   | DatasheetName:ColumnName      | ```long number```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random long number with length", input = InputType.YES, condition = InputType.YES)
        public void randomNextLongWithLength() {
            try {
                String strObj = Input;
                String numStr = Condition;
                long num=Long.parseLong(numStr);
                long randomLong = faker.get(key).random().nextLong(num);
                Report.updateTestLog(Action, "Generated data: " + randomLong, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Long.toString(randomLong));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random long: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomNextBoolean**

**Description**: This function will generate a random boolean value

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomNextBoolean`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random boolean value", input = InputType.YES, condition = InputType.NO)
        public void randomNextBoolean() {
            try {
                String strObj = Input;
                boolean randomBoolean = faker.get(key).random().nextBoolean();
                Report.updateTestLog(Action, "Generated data: " + randomBoolean, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Boolean.toString(randomBoolean));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random boolean: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomNextDouble**

**Description**: This function will generate a random double number

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomNextDouble`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Double number", input = InputType.YES, condition = InputType.NO)
        public void randomNextDouble() {
            try {
                String strObj = Input;
                Double randomDouble = faker.get(key).random().nextDouble();
                Report.updateTestLog(Action, "Generated data: " + randomDouble, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Double.toString(randomDouble));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random float: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------