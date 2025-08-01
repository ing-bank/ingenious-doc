# **Faker Actions related to Date and Time**

## **futureUpto**

**Description**: This function will generate a random future date from now

**Input Format** : DatasheetName:ColumnName

**Condition Format**: max date and the time unit, for example: `10:SECONDS`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`futureUpto`](#)   | DatasheetName:ColumnName      |  ```max date and the time unit```     | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generates a future date from now", input = InputType.YES, condition = InputType.YES)
        public void futureUpto() {
            try {
                String strObj = Input;
                String max = Condition.split(":", 2)[0];
                int atMost=Integer.parseInt(max);
                String unitStr = Condition.split(":", 2)[1];
                TimeUnit unit=TimeUnit.valueOf(unitStr);
                Date futureDate = faker.get(key).date().future(atMost, unit);
                Report.updateTestLog(Action, "Generated data: " + futureDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, futureDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **futureWithinRange**

**Description**: This function will generate a random future date from now, with a minimum time

**Input Format** : DatasheetName:ColumnName

**Condition Format**: max, min dates and the time unit, for example: `10:5:HOURS`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`futureWithinRange`](#)   | DatasheetName:ColumnName      |  ```max, min dates and the time unit```     | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generates a future date from now, with a minimum time", input = InputType.YES, condition = InputType.YES)
        public void futureWithinRange() {
            try {
                String strObj = Input;
                String max = Condition.split(":", 3)[0];
                String min = Condition.split(":", 3)[1];
                int atMost=Integer.parseInt(max);
                int minimum=Integer.parseInt(min);
                String unitStr = Condition.split(":", 3)[2];
                TimeUnit unit=TimeUnit.valueOf(unitStr);
                Date futureDate = faker.get(key).date().future(atMost, minimum, unit);
                Report.updateTestLog(Action, "Generated data: " + futureDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, futureDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **futureUptoBasedOnRefDate**

**Description**: This function will generate a random future date relative to the reference date

**Input Format** : DatasheetName:ColumnName

**Condition Format**: max date, time unit and the reference date, for example: `15:SECONDS:01/10/2023`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`futureUptoBasedOnRefDate`](#)   | DatasheetName:ColumnName      |  ```max date, time unit and the reference date```     | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generates a future date relative to the reference date", input = InputType.YES, condition = InputType.YES)
        public void futureUptoBasedOnRefDate() {
            try {
                String strObj = Input;
                SimpleDateFormat formatter = new SimpleDateFormat("dd/MM/yyyy");
                String max = Condition.split(":", 3)[0];
                int atMost=Integer.parseInt(max);
                String unitStr = Condition.split(":", 3)[1];
                TimeUnit unit=TimeUnit.valueOf(unitStr);
                String dateStr = Condition.split(":", 3)[2];
                Date referenceDate = formatter.parse(dateStr);
                Date futureDate = faker.get(key).date().future(atMost, unit, referenceDate);
                Report.updateTestLog(Action, "Generated data: " + futureDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, futureDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **pastUpto**

**Description**: This function will generate a random past date from now

**Input Format** : DatasheetName:ColumnName

**Condition Format**: max date and the time unit, for example: `11:HOURS`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`pastUpto`](#)   | DatasheetName:ColumnName      |  ```max date and the time unit```    | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generates a past date from now", input = InputType.YES, condition = InputType.YES)
        public void pastUpto() {
            try {
                String strObj = Input;
                String max = Condition.split(":", 2)[0];
                int atMost=Integer.parseInt(max);
                String unitStr = Condition.split(":", 2)[1];
                TimeUnit unit=TimeUnit.valueOf(unitStr);
                Date pastDate = faker.get(key).date().past(atMost, unit);
                Report.updateTestLog(Action, "Generated data: " + pastDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, pastDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **pastWithinRange**

**Description**: This function will generate a random past date from now, with a minimum time

**Input Format** : DatasheetName:ColumnName

**Condition Format**: max, min dates and the time unit, for example: `10:5:MILLISECONDS`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`pastWithinRange`](#)   | DatasheetName:ColumnName      |  ```max, min dates and the time unit```    | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generates a past date from now, with a minimum time", input = InputType.YES, condition = InputType.YES)
        public void pastWithinRange() {
            try {
                String strObj = Input;
                String max = Condition.split(":", 3)[0];
                String min = Condition.split(":", 3)[1];
                int atMost=Integer.parseInt(max);
                int minimum=Integer.parseInt(min);
                String unitStr = Condition.split(":", 3)[2];
                TimeUnit unit=TimeUnit.valueOf(unitStr);
                Date pastDate = faker.get(key).date().past(atMost, minimum, unit);
                Report.updateTestLog(Action, "Generated data: " + pastDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, pastDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **pastUptoBasedOnRefDate**

**Description**: This function will generate a random past date relative to the reference date

**Input Format** : DatasheetName:ColumnName

**Condition Format**: max date, time unit and the reference date, for example: `15:DAYS:01/10/2023`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`pastUptoBasedOnRefDate`](#)   | DatasheetName:ColumnName      |  ```max date, time unit and the reference date```    | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generates a past date relative to the reference date", input = InputType.YES, condition = InputType.YES)
        public void pastUptoBasedOnRefDate() {
            try {
                String strObj = Input;
                SimpleDateFormat formatter = new SimpleDateFormat("dd/MM/yyyy");
                String max = Condition.split(":", 3)[0];
                int atMost=Integer.parseInt(max);
                String unitStr = Condition.split(":", 3)[1];
                TimeUnit unit=TimeUnit.valueOf(unitStr);
                String dateStr = Condition.split(":", 3)[2];
                Date referenceDate = formatter.parse(dateStr);
                Date pastDate = faker.get(key).date().past(atMost, unit, referenceDate);
                Report.updateTestLog(Action, "Generated data: " + pastDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, pastDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **dateBetween**

**Description**: This function will generate a random date between two dates

**Input Format** : DatasheetName:ColumnName

**Condition Format**: start and end dates, for example: `23/11/2023:11/12/2023`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`dateBetween`](#)   | DatasheetName:ColumnName      | ```start and end dates```    | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random date between two dates", input = InputType.YES, condition = InputType.YES)
        public void dateBetween() {
            try {
                String strObj = Input;
                SimpleDateFormat formatter = new SimpleDateFormat("dd/MM/yyyy");
                String from = Condition.split(":", 2)[0];
                String to = Condition.split(":", 2)[1];
                Date startDate= formatter.parse(from);
                Date endDate= formatter.parse(to);
                Date betweenDate = faker.get(key).date().between(startDate, endDate);
                Report.updateTestLog(Action, "Generated data: " + betweenDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, betweenDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **birthday**

**Description**: This function will generate a random birthday between 65 and 18 years ago

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`birthday`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generates a random birthday between 65 and 18 years ago", input = InputType.YES, condition = InputType.NO)
        public void birthday() {
            try {
                String strObj = Input;
                Date birthdayDate = faker.get(key).date().birthday();
                Report.updateTestLog(Action, "Generated data: " + birthdayDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, birthdayDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **birthdayWithinRange**

**Description**: This function will generate a random birthday between two ages

**Input Format** : DatasheetName:ColumnName

**Condition Format**: min and max ages, for example: `45:50`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`birthdayWithinRange`](#)   | DatasheetName:ColumnName      | ```min and max ages```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generates a random birthday between two ages", input = InputType.YES, condition = InputType.YES)
        public void birthdayWithinRange() {
            try {
                String strObj = Input;
                String from = Condition.split(":", 2)[0];
                String to = Condition.split(":", 2)[1];
                int minAge=Integer.parseInt(from);
                int maxAge=Integer.parseInt(to);
                Date birthdayDate = faker.get(key).date().birthday(minAge, maxAge);
                Report.updateTestLog(Action, "Generated data: " + birthdayDate, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, birthdayDate.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------