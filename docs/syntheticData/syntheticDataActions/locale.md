# **Faker Locale Setup**

## **setLocale**

**Description**: This function will setup the Faker locale based on locale entered by the user

**Input Format** : DatasheetName:ColumnName

**Condition Format**: faker locale, for example `en-US`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`setLocale`](#)   | DatasheetName:ColumnName      |  ```faker locale```     | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Set Faker locale for testing", input = InputType.YES, condition = InputType.YES)
        public void setLocale() {
            try {
                String strObj = Input;
                String locale = Condition.split(":", 1)[0];
                Faker faker1 = new Faker(new Locale(locale));
                faker.put(key,faker1);
                Report.updateTestLog(Action, "Faker locale set to " + locale, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, locale);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during locale setup", ex);
                Report.updateTestLog(Action, "Error setting locale: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------