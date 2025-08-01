# **Faker Actions related to Number**

## **digit**

**Description**: This function will generate random digit

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`digit`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random digit", input = InputType.YES, condition = InputType.NO)
        public void digit() {
            try {
                String strObj = Input;
                String digit = faker.get(key).number().digit();
                Report.updateTestLog(Action, "Generated data: " + digit, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, digit);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating digit: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **digits**

**Description**: This function will generate random digits

**Input Format** : DatasheetName:ColumnName

**Condition Format**: digit count, for example: `5`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`digits`](#)   | DatasheetName:ColumnName      | ```digit count```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random digits", input = InputType.YES, condition = InputType.YES)
        public void digits() {
            try {
                String strObj = Input;
                String countStr = Condition;
                int count=Integer.parseInt(countStr);
                String digit = faker.get(key).number().digits(count);
                Report.updateTestLog(Action, "Generated data: " + digit, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, digit);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating digits: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomNumber**

**Description**: This function will generate a random number

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomNumber`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random number", input = InputType.YES, condition = InputType.NO)
        public void randomNumber() {
            try {
                String strObj = Input;
                long randomNumber = faker.get(key).number().randomNumber();
                Report.updateTestLog(Action, "Generated data: " + randomNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Long.toString(randomNumber));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random number: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomDigit**

**Description**: This function will generate a random number from 0-9 (both inclusive)

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomDigit`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random number from 0-9 (both inclusive)", input = InputType.YES, condition = InputType.NO)
        public void randomDigit() {
            try {
                String strObj = Input;
                int randomDigit = faker.get(key).number().randomDigit();
                Report.updateTestLog(Action, "Generated data: " + randomDigit, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Integer.toString(randomDigit));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random digit: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomDigitNot0**

**Description**: This function will generate a random number from 1-9 (both inclusive)

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomDigitNot0`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random number from 1-9 (both inclusive)", input = InputType.YES, condition = InputType.NO)
        public void randomDigitNot0() {
            try {
                String strObj = Input;
                int randomDigit = faker.get(key).number().randomDigitNotZero();
                Report.updateTestLog(Action, "Generated data: " + randomDigit, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Integer.toString(randomDigit));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random digit: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomIntegerNumberBetween**

**Description**: This function will generate a random number between 2 integers

**Input Format** : DatasheetName:ColumnName

**Condition Format**: minimum and maximum integer range, for example: `55:100`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomIntegerNumberBetween`](#)   | DatasheetName:ColumnName      | ```minimum and maximum integer range```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random number between 2 integers", input = InputType.YES, condition = InputType.YES)
        public void randomIntegerNumberBetween() {
            try {
                String strObj = Input;
                String inputMin = Condition.split(":", 2)[0];
                String inputMax = Condition.split(":", 2)[1];
                int min = Integer.parseInt(inputMin);
                int max = Integer.parseInt(inputMax);
                int randomNumber = faker.get(key).number().numberBetween(min, max);
                Report.updateTestLog(Action, "Generated data: " + randomNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Integer.toString(randomNumber));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random number: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomLongNumberBetween**

**Description**: This function will generate a random number between 2 long numbers

**Input Format** : DatasheetName:ColumnName

**Condition Format**: minimum and maximum long range, for example: `100:1000`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomLongNumberBetween`](#)   | DatasheetName:ColumnName      | ```minimum and maximum long range```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random number between 2 long numbers", input = InputType.YES, condition = InputType.YES)
        public void randomLongNumberBetween() {
            try {
                String strObj = Input;
                String inputMin = Condition.split(":", 2)[0];
                String inputMax = Condition.split(":", 2)[1];
                long min = Long.parseLong(inputMin);
                long max = Long.parseLong(inputMax);
                long randomNumber = faker.get(key).number().numberBetween(min, max);
                Report.updateTestLog(Action, "Generated data: " + randomNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Long.toString(randomNumber));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random number: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomDoubleBetweenIntegers**

**Description**: This function will generate a random double between 2 integers with maximum number of decimals

**Input Format** : DatasheetName:ColumnName

**Condition Format**: maximum number of decimals, minimum and maximum integer range, for example: `5:660:690`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomDoubleBetweenIntegers`](#)   | DatasheetName:ColumnName      | ```maximum number of decimals, minimum and maximum integer range```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random double between 2 integers with maximum number of decimals", input = InputType.YES, condition = InputType.YES)
        public void randomDoubleBetweenIntegers() {
            try {
                String strObj = Input;
                String inputMaxDecimals = Condition.split(":", 3)[0];
                String inputMin = Condition.split(":", 3)[1];
                String inputMax = Condition.split(":", 3)[2];
                int maxNumOfDecimals = Integer.parseInt(inputMaxDecimals);
                int min = Integer.parseInt(inputMin);
                int max = Integer.parseInt(inputMax);
                Double randomNumber = faker.get(key).number().randomDouble(maxNumOfDecimals, min, max);
                Report.updateTestLog(Action, "Generated data: " + randomNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Double.toString(randomNumber));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random number: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomDoubleBetweenLong**

**Description**: This function will generate a random double between 2 long numbers with maximum number of decimals

**Input Format** : DatasheetName:ColumnName

**Condition Format**: maximum number of decimals, minimum and maximum long range, for example: `5:660:690`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomDoubleBetweenLong`](#)   | DatasheetName:ColumnName      | ```maximum number of decimals, minimum and maximum long range```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random double between 2 Long numbers with maximum number of decimals", input = InputType.YES, condition = InputType.YES)
        public void randomDoubleBetweenLong() {
            try {
                String strObj = Input;
                String inputMaxDecimals = Condition.split(":", 3)[0];
                String inputMin = Condition.split(":", 3)[1];
                String inputMax = Condition.split(":", 3)[2];
                int maxNumOfDecimals = Integer.parseInt(inputMaxDecimals);
                long min = Long.parseLong(inputMin);
                long max = Long.parseLong(inputMax);
                Double randomNumber = faker.get(key).number().randomDouble(maxNumOfDecimals, min, max);
                Report.updateTestLog(Action, "Generated data: " + randomNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Double.toString(randomNumber));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random number between 1 and 100: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **randomNumberWithNoOfDigits**

**Description**: This function will generate a random number with specific number of digits

**Input Format** : DatasheetName:ColumnName

**Condition Format**: number of digits, for example: `15`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`randomNumberWithNoOfDigits`](#)   | DatasheetName:ColumnName      | ```number of digits```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random number with specific number of digits", input = InputType.YES, condition = InputType.YES)
        public void randomNumberWithNoOfDigits() {
            try {
                String strObj = Input;
                String digitStr = Condition;
                int numOfDigits=Integer.parseInt(digitStr);
                boolean strict = true;
                long randomNumber = faker.get(key).number().randomNumber(numOfDigits, strict);
                Report.updateTestLog(Action, "Generated data: " + randomNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Long.toString(randomNumber));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating random number: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------