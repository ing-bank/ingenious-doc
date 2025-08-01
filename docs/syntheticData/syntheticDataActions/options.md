# **Faker Actions related to Options**

## **optionFromBoolean**

**Description**: This function will generate a random boolean value (true or false)

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`optionFromBoolean`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Pick a random boolean value (true or false)", input = InputType.YES, condition = InputType.NO)
        public void optionFromBoolean() {
            try {
                String strObj = Input;
                boolean randomBoolean = faker.get(key).options().option(Boolean.TRUE, Boolean.FALSE);
                Report.updateTestLog(Action, "Generated data: " + randomBoolean, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Boolean.toString(randomBoolean));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating boolean: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **optionFromIntegers**

**Description**: This function will pick a random value from a predefined list of integers

**Input Format** : DatasheetName:ColumnName

**Condition Format**: list of integers, for example: `1:9:5:3:10:45:90`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`optionFromIntegers`](#)   | DatasheetName:ColumnName      | ```list of integers```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Pick a random value from a predefined list of integers", input = InputType.YES, condition = InputType.YES)
        public void optionFromIntegers() {
            try {
                String strObj = Input;
                char splitChar=':';
                int count = (int) Condition.chars().filter(ch -> ch == splitChar).count();
                Integer[] numbersList = new Integer[count+1];
                for(int i=0; i<=count; i++)
                {
                    numbersList[i]= Integer.valueOf(Condition.split(":", count+1)[i]);
                }
                Integer randomNumber = faker.get(key).options().option(numbersList);
                Report.updateTestLog(Action, "Generated data: " + randomNumber, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Long.toString(randomNumber));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating integer: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **optionFromDoubles**

**Description**: This function will pick a random value from a predefined list of doubles

**Input Format** : DatasheetName:ColumnName

**Condition Format**: list of doubles, for example: `1.1:1.2:33.3:58.9`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`optionFromDoubles`](#)   | DatasheetName:ColumnName      | ```list of doubles```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Pick a random value from a predefined list of doubles", input = InputType.YES, condition = InputType.YES)
        public void optionFromDoubles() {
            try {
                String strObj = Input;
                char splitChar=':';
                int count = (int) Condition.chars().filter(ch -> ch == splitChar).count();
                Double[] doubleList = new Double[count+1];
                for(int i=0; i<=count; i++)
                {
                    doubleList[i]= Double.valueOf(Condition.split(":", count+1)[i]);
                }
                Double randomDouble = faker.get(key).options().option(doubleList);
                Report.updateTestLog(Action, "Generated data: " + randomDouble, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Double.toString(randomDouble));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating double: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **optionFromLong**

**Description**: This function will pick a random value from a predefined list of long numbers

**Input Format** : DatasheetName:ColumnName

**Condition Format**: list of long numbers, for example: `12:33:44:55:99:98:104`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`optionFromLong`](#)   | DatasheetName:ColumnName      | ```list of long```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Pick a random value from a predefined list of Longs", input = InputType.YES, condition = InputType.YES)
        public void optionFromLong() {
            try {
                String strObj = Input;
                char splitChar=':';
                int count = (int) Condition.chars().filter(ch -> ch == splitChar).count();
                Long[] longList = new Long[count+1];
                for(int i=0; i<=count; i++)
                {
                    longList[i]= Long.valueOf(Condition.split(":", count+1)[i]);
                }
                Long randomDouble = faker.get(key).options().option(longList);
                Report.updateTestLog(Action, "Generated data: " + randomDouble, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Long.toString(randomDouble));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating double: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **optionFromStrings**

**Description**: This function will pick a random value from a predefined list of strings

**Input Format** : DatasheetName:ColumnName

**Condition Format**: list of strings, for example: `apple:bat:cat:deer:elephant:frog:goat:zebra`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`optionFromStrings`](#)   | DatasheetName:ColumnName      | ```list of strings```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Pick a random value from a predefined list of strings", input = InputType.YES, condition = InputType.YES)
        public void optionFromStrings() {
            try {
                String strObj = Input;
                char splitChar=':';
                int count = (int) Condition.chars().filter(ch -> ch == splitChar).count();
                String[] stringList = new String[count+1];
                for(int i=0; i<=count; i++)
                {
                    stringList[i]= String.valueOf(Condition.split(":", count+1)[i]);
                }
                String randomString = faker.get(key).options().option(stringList);
                Report.updateTestLog(Action, "Generated data: " + randomString, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, randomString);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating string: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **nextElementStringArray**

**Description**: This function will generate next element from an array of strings

**Input Format** : DatasheetName:ColumnName

**Condition Format**: list of strings, for example: `option1:option2:option3:option4:option5:option6:option7`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`nextElementStringArray`](#)   | DatasheetName:ColumnName      | ```list of strings```  | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate next element from an array of strings", input = InputType.YES, condition = InputType.YES)
        public void nextElementStringArray() {
            try {
                String strObj = Input;
                char splitChar=':';
                int count = (int) Condition.chars().filter(ch -> ch == splitChar).count();
                String[] stringList = new String[count+1];
                for(int i=0; i<=count; i++)
                {
                    stringList[i]= String.valueOf(Condition.split(":", count+1)[i]);
                }
                String element = faker.get(key).options().nextElement(stringList);
                Report.updateTestLog(Action, "Generated data: " + element, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, element);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating element from string array: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------