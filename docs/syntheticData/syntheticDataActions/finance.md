# **Faker Actions related to Finance**

## **financeCreditCardNumber**

**Description**: This function will generate a random credit card number

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`financeCreditCardNumber`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random credit card number", input = InputType.YES, condition = InputType.NO)
        public void financeCreditCardNumber() {
            try {
                String strObj = Input;
                String creditCard = faker.get(key).finance().creditCard();
                Report.updateTestLog(Action, "Generated data: " + creditCard, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, creditCard);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **creditCardNumberBasedOnType**

**Description**: This function will generate a random credit card number based on type

**Input Format** : DatasheetName:ColumnName

**Condition Format**: type, for example: `VISA`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`creditCardNumberBasedOnType`](#)   | DatasheetName:ColumnName      | ```type```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random credit card number based on type", input = InputType.YES, condition = InputType.YES)
        public void creditCardNumberBasedOnType() {
            try {
                String strObj = Input;
                String type = Condition;
                CreditCardType creditCardType=CreditCardType.valueOf(type);
                String creditCard = faker.get(key).finance().creditCard(creditCardType);
                Report.updateTestLog(Action, "Generated data: " + creditCard, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, creditCard);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **bic**

**Description**: This function will generate a random BIC (Bank Identifier Code)

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`bic`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random BIC (Bank Identifier Code)", input = InputType.YES, condition = InputType.NO)
        public void bic() {
            try {
                String strObj = Input;
                String bic = faker.get(key).finance().bic();
                Report.updateTestLog(Action, "Generated data: " + bic, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, bic);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **iban**

**Description**: This function will generate a random IBAN (International Bank Account Number)

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`iban`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random IBAN (International Bank Account Number)", input = InputType.YES, condition = InputType.NO)
        public void iban() {
            try {
                String strObj = Input;
                String iban = faker.get(key).finance().iban();
                Report.updateTestLog(Action, "Generated data: " + iban, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, iban);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **ibanByCountry**

**Description**: This function will generate a random IBAN with a specific country code

**Input Format** : DatasheetName:ColumnName

**Condition Format**: country code, for example: `DE`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`ibanByCountry`](#)   | DatasheetName:ColumnName      | ```country code```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random IBAN with a specific country code", input = InputType.YES, condition = InputType.YES)
        public void ibanByCountry() {
            try {
                String strObj = Input;
                String countryCode = Condition;
                String iban = faker.get(key).finance().iban(countryCode);
                Report.updateTestLog(Action, "Generated data: " + iban, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, iban);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating data: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------