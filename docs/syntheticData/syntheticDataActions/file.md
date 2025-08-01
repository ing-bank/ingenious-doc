# **Faker Actions related to File**

## **fileName**

**Description**: This function will generate a random file name

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`fileName`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random file name", input = InputType.YES, condition = InputType.NO)
        public void fileName() {
            try {
                String strObj = Input;
                String fileName = faker.get(key).file().fileName();
                Report.updateTestLog(Action, "Generated data: " + fileName, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, fileName);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **fileNameWithDetails**

**Description**: This function will generate a random file name with details

**Input Format** : DatasheetName:ColumnName

**Condition Format**: directory, name, extension and separator, for example: `c:javafaker:txt:.`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`fileNameWithDetails`](#)   | DatasheetName:ColumnName      | ```directory, name, extension and separator```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random file name with details", input = InputType.YES, condition = InputType.YES)
        public void fileNameWithDetails() {
            try {
                String strObj = Input;
                String dirOrNull = Condition.split(":", 4)[0];
                String nameOrNull = Condition.split(":", 4)[1];
                String extensionOrNull = Condition.split(":", 4)[2];
                String separatorOrNull = Condition.split(":", 4)[3];
                String fileName = faker.get(key).file().fileName(dirOrNull, nameOrNull, extensionOrNull, separatorOrNull);
                Report.updateTestLog(Action, "Generated data: " + fileName, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, fileName);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **mimeType**

**Description**: This function will generate a random mime type

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`mimeType`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random mime type", input = InputType.YES, condition = InputType.NO)
        public void mimeType() {
            try {
                String strObj = Input;
                String mimeType = faker.get(key).file().mimeType();
                Report.updateTestLog(Action, "Generated data: " + mimeType, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, mimeType);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **fileNameWithExtension**

**Description**: This function will generate a random file name with an optional file extension

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |*fileNameWithExtension*   | DatasheetName:ColumnName || |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random file name with an optional file extension", input = InputType.NO)
        public void fileNameWithExtension() {
            try {
                String strObj = Input;
                String fileNameWithExtension = faker.get(key).file().extension();
                Report.updateTestLog(Action, "Generated data: " + fileNameWithExtension, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, fileNameWithExtension);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------