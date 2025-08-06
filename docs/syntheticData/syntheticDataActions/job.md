# **Faker Actions related to Job**

## **jobTitle**

**Description**: This function will generate a random job title

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`jobTitle`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random job title", input = InputType.YES, condition = InputType.NO)
        public void jobTitle() {
            try {
                String strObj = Input;
                String jobTitle = faker.get(key).job().title();
                Report.updateTestLog(Action, "Generated data: " + jobTitle, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, jobTitle);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating job title: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **jobField**

**Description**: This function will generate a random job field

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`jobField`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random field of job", input = InputType.YES, condition = InputType.NO)
        public void jobField() {
            try {
                String strObj = Input;
                String jobField = faker.get(key).job().field();
                Report.updateTestLog(Action, "Generated data: " + jobField, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, jobField);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating job field: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **jobKeySkills**

**Description**: This function will generate a random key skill for the job

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`jobKeySkills`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random key skill for the job", input = InputType.YES, condition = InputType.NO)
        public void jobKeySkills() {
            try {
                String strObj = Input;
                String keySkill = faker.get(key).job().keySkills();
                Report.updateTestLog(Action, "Generated data: " + keySkill, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, keySkill);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating job key skill: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **jobSeniority**

**Description**: This function will generate a random seniority level for the job

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`jobSeniority`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random seniority level for the job", input = InputType.YES, condition = InputType.NO)
        public void jobSeniority() {
            try {
                String strObj = Input;
                String seniority = faker.get(key).job().seniority();
                Report.updateTestLog(Action, "Generated data: " + seniority, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, seniority);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating job seniority: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **jobPosition**

**Description**: This function will generate a random job position

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`jobPosition`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random job position", input = InputType.YES, condition = InputType.NO)
        public void jobPosition() {
            try {
                String strObj = Input;
                String position = faker.get(key).job().position();
                Report.updateTestLog(Action, "Generated data: " + position, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, position);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating job position: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------