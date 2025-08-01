# **Faker Actions related to Internet**

## **emailAddress**

**Description**: This function will generate a random email address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`emailAddress`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random email address", input = InputType.YES, condition = InputType.NO)
        public void emailAddress() {
            try {
                String strObj = Input;
                String email = faker.get(key).internet().emailAddress();
                Report.updateTestLog(Action, "Generated data: " + email, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, email);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating email: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **emailAddressWithLocalPart**

**Description**: This function will generate a random email address with local part

**Input Format** : DatasheetName:ColumnName

**Condition Format**: local part, for example: `faker`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`emailAddressWithLocalPart`](#)   | DatasheetName:ColumnName      | ```local part```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random email address with local part", input = InputType.YES, condition = InputType.YES)
        public void emailAddressWithLocalPart() {
            try {
                String strObj = Input;
                String localPart = Condition;
                String email = faker.get(key).internet().emailAddress(localPart);
                Report.updateTestLog(Action, "Generated data: " + email, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, email);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating email: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **safeEmailAddress**

**Description**: This function will generate a random safe email address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`safeEmailAddress`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random safe email address", input = InputType.YES, condition = InputType.NO)
        public void safeEmailAddress() {
            try {
                String strObj = Input;
                String safeEmail = faker.get(key).internet().safeEmailAddress();
                Report.updateTestLog(Action, "Generated data: " + safeEmail, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, safeEmail);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating safe email: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **safeEmailAddressWithLocalPart**

**Description**: This function will generate a random safe email address with local part

**Input Format** : DatasheetName:ColumnName

**Condition Format**: local part, for example: `faker`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`safeEmailAddressWithLocalPart`](#)   | DatasheetName:ColumnName      | ```local part```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random safe email address with local part", input = InputType.YES, condition = InputType.YES)
        public void safeEmailAddressWithLocalPart() {
            try {
                String strObj = Input;
                String localPart = Condition;
                String safeEmail = faker.get(key).internet().safeEmailAddress(localPart);
                Report.updateTestLog(Action, "Generated data: " + safeEmail, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, safeEmail);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating safe email: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **domainName**

**Description**: This function will generate a random domain name

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`domainName`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random domain name", input = InputType.YES, condition = InputType.NO)
        public void domainName() {
            try {
                String strObj = Input;
                String domainName = faker.get(key).internet().domainName();
                Report.updateTestLog(Action, "Generated data: " + domainName, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, domainName);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating domain name: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **domainSuffix**

**Description**: This function will generate a random domain suffix

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`domainSuffix`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random domain suffix", input = InputType.YES, condition = InputType.NO)
        public void domainSuffix() {
            try {
                String strObj = Input;
                String domainSuffix = faker.get(key).internet().domainSuffix();
                Report.updateTestLog(Action, "Generated data " + domainSuffix, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, domainSuffix);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating domain name: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **domainWord**

**Description**: This function will generate a random domain word

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`domainWord`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random domain Word", input = InputType.YES, condition = InputType.NO)
        public void domainWord() {
            try {
                String strObj = Input;
                String domainWord = faker.get(key).internet().domainWord();
                Report.updateTestLog(Action, "Generated data: " + domainWord, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, domainWord);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating domain name: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetUrl**

**Description**: This function will generate a random URL

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetUrl`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random URL", input = InputType.YES, condition = InputType.NO)
        public void internetUrl() {
            try {
                String strObj = Input;
                String url = faker.get(key).internet().url();
                Report.updateTestLog(Action, "Generated data: " + url, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, url);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating URL: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **ipV4Address**

**Description**: This function will generate a random IP (IPv4) address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`ipV4Address`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random IP (IPv4) address", input = InputType.YES, condition = InputType.NO)
        public void ipV4Address() {
            try {
                String strObj = Input;
                String ipV4 = faker.get(key).internet().ipV4Address();
                Report.updateTestLog(Action, "Generated data: " + ipV4, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, ipV4);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv4 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **ipV6Address**

**Description**: This function will generate a random IP (IPv6) address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`ipV6Address`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random IP (IPv6) address", input = InputType.YES, condition = InputType.NO)
        public void ipV6Address() {
            try {
                String strObj = Input;
                String ipV6 = faker.get(key).internet().ipV6Address();
                Report.updateTestLog(Action, "Generated data: " + ipV6, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, ipV6);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv6 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **ipV4Cidr**

**Description**: This function will generate a random IP (IPv4) CIDR address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`ipV4Cidr`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random IP (IPv4) CIDR address", input = InputType.YES, condition = InputType.NO)
        public void ipV4Cidr() {
            try {
                String strObj = Input;
                String ipV4 = faker.get(key).internet().ipV4Cidr();
                Report.updateTestLog(Action, "Generated data: " + ipV4, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, ipV4);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv4 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **ipV6Cidr**

**Description**: This function will generate a random IP (IPv6) CIDR address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`ipV6Cidr`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random IP (IPv6) CIDR address", input = InputType.YES, condition = InputType.NO)
        public void ipV6Cidr() {
            try {
                String strObj = Input;
                String ipV6 = faker.get(key).internet().ipV6Cidr();
                Report.updateTestLog(Action, "Generated data: " + ipV6, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, ipV6);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv6 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **macAddress**

**Description**: This function will generate a random MAC address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`macAddress`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random MAC address", input = InputType.YES, condition = InputType.NO)
        public void macAddress() {
            try {
                String strObj = Input;
                String macAddress = faker.get(key).internet().macAddress();
                Report.updateTestLog(Action, "Generated data: " + macAddress, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, macAddress);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating MAC Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **macAddressWithPrefix**

**Description**: This function will generate a random MAC address with Prefix

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`macAddressWithPrefix`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random MAC address with Prefix", input = InputType.YES, condition = InputType.NO)
        public void macAddressWithPrefix() {
            try {
                String strObj = Input;
                String prefix="A32";
                String macAddress = faker.get(key).internet().macAddress(prefix);
                Report.updateTestLog(Action, "Generated data: " + macAddress, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, macAddress);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating MAC Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **privateIpV4Address**

**Description**: This function will generate a random private IP (IPv4) address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`privateIpV4Address`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random private IP (IPv4) address", input = InputType.YES, condition = InputType.NO)
        public void privateIpV4Address() {
            try {
                String strObj = Input;
                String ipV4 = faker.get(key).internet().privateIpV4Address();
                Report.updateTestLog(Action, "Generated data: " + ipV4, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, ipV4);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv4 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **publicIpV6Address**

**Description**: This function will generate a random public IP (IPv6) address

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`publicIpV6Address`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random public IP (IPv6) address", input = InputType.YES, condition = InputType.NO)
        public void publicIpV6Address() {
            try {
                String strObj = Input;
                String ipV6 = faker.get(key).internet().publicIpV4Address();
                Report.updateTestLog(Action, "Generated data: " + ipV6, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, ipV6);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv6 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetAvatar**

**Description**: This function will generate a random internet avatar

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetAvatar`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random internet avatar", input = InputType.YES, condition = InputType.NO)
        public void internetAvatar() {
            try {
                String strObj = Input;
                String avatar = faker.get(key).internet().avatar();
                Report.updateTestLog(Action, "Generated data: " + avatar, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, avatar);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv6 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetImage**

**Description**: This function will generate a random internet image

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetImage`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random internet image", input = InputType.YES, condition = InputType.NO)
        public void internetImage() {
            try {
                String strObj = Input;
                String image = faker.get(key).internet().image();
                Report.updateTestLog(Action, "Generated data: " + image, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, image);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv6 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetImageWithSpecs**

**Description**: This function will generate a random internet image with specs

**Input Format** : DatasheetName:ColumnName

**Condition Format**: width, height, gray and text, for example: `12:12:4:hello`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetImageWithSpecs`](#)   | DatasheetName:ColumnName      | ```width, height, gray and text```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random internet image with specs", input = InputType.YES, condition = InputType.YES)
        public void internetImageWithSpecs() {
            try {
                String strObj = Input;
                String widthStr = Condition.split(":", 4)[0];
                String heightStr = Condition.split(":", 4)[1];
                String grayStr = Condition.split(":", 4)[2];
                String text = Condition.split(":", 4)[3];
                Integer width=Integer.parseInt(widthStr);
                Integer height=Integer.parseInt(heightStr);
                Boolean gray= Boolean.valueOf(grayStr);
                String image = faker.get(key).internet().image(width, height, gray, text);
                Report.updateTestLog(Action, "Generated data: " + image, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, image);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating IPv6 Address: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetPasswordWithLength**

**Description**: This function will generate a random password with custom length

**Input Format** : DatasheetName:ColumnName

**Condition Format**: min and max lengths, for example: `5:20`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetPasswordWithLength`](#)   | DatasheetName:ColumnName      | ```min and max lengths```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random password with custom length", input = InputType.YES, condition = InputType.YES)
        public void internetPasswordWithLength() {
            try {
                String strObj = Input;
                String minStr = Condition.split(":", 2)[0];
                String maxStr = Condition.split(":", 2)[1];
                int minLength=Integer.parseInt(minStr);
                int maxLength=Integer.parseInt(maxStr);
                String password = faker.get(key).internet().password(minLength, maxLength);
                Report.updateTestLog(Action, "Generated data: " + password, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, password);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating password: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetPassword**

**Description**: This function will generate a random password

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetPassword`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random password", input = InputType.YES, condition = InputType.NO)
        public void internetPassword() {
            try {
                String strObj = Input;
                String password = faker.get(key).internet().password();
                Report.updateTestLog(Action, "Generated data: " + password, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, password);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating password: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetPasswordWithDigits**

**Description**: This function will generate a random password including digits

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetPasswordWithDigits`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random password including digits", input = InputType.YES, condition = InputType.NO)
        public void internetPasswordWithDigits() {
            try {
                String strObj = Input;
                boolean includeDigit=true;
                String password = faker.get(key).internet().password(includeDigit);
                Report.updateTestLog(Action, "Generated data: " + password, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, password);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating password: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetPasswordWithLengthUppercase**

**Description**: This function will generate a random password with custom length and uppercase included

**Input Format** : DatasheetName:ColumnName

**Condition Format**: min and max lengths, for example: `5:19`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetPasswordWithLengthUppercase`](#)   | DatasheetName:ColumnName      | ```min and max lengths```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random password with custom length and uppercase included", input = InputType.YES, condition = InputType.YES)
        public void internetPasswordWithLengthUppercase() {
            try {
                String strObj = Input;
                String minStr = Condition.split(":", 2)[0];
                String maxStr = Condition.split(":", 2)[1];
                int minLength=Integer.parseInt(minStr);
                int maxLength=Integer.parseInt(maxStr);
                boolean includeUppercase=true;
                String password = faker.get(key).internet().password(minLength, maxLength, includeUppercase);
                Report.updateTestLog(Action, "Generated data: " + password, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, password);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating password: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetPasswordWithLengthUppercaseSpecial**

**Description**: This function will generate a random password with custom length, uppercase and special character

**Input Format** : DatasheetName:ColumnName

**Condition Format**: min and max lengths, for example: `5:9`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetPasswordWithLengthUppercaseSpecial`](#)   | DatasheetName:ColumnName      | ```min and max lengths```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random password with custom length, uppercase and special character", input = InputType.YES, condition = InputType.YES)
        public void internetPasswordWithLengthUppercaseSpecial() {
            try {
                String strObj = Input;
                String minStr = Condition.split(":", 2)[0];
                String maxStr = Condition.split(":", 2)[1];
                int minLength=Integer.parseInt(minStr);
                int maxLength=Integer.parseInt(maxStr);
                boolean includeUppercase=true;
                boolean includeSpecial=true;
                String password = faker.get(key).internet().password(minLength, maxLength, includeUppercase, includeSpecial);
                Report.updateTestLog(Action, "Generated data: " + password, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, password);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating password: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetPasswordwithUppercaseSpecialDigit**

**Description**: This function will generate a random password with custom length, uppercase, special character and digits

**Input Format** : DatasheetName:ColumnName

**Condition Format**: min and max lengths, for example: `4:9`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetPasswordwithUppercaseSpecialDigit`](#)   | DatasheetName:ColumnName      | ```min and max lengths```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random password with custom length, uppercase, special character and digits", input = InputType.YES, condition = InputType.YES)
        public void internetPasswordwithUppercaseSpecialDigit() {
            try {
                String strObj = Input;
                String minStr = Condition.split(":", 2)[0];
                String maxStr = Condition.split(":", 2)[1];
                int minLength=Integer.parseInt(minStr);
                int maxLength=Integer.parseInt(maxStr);
                boolean includeUppercase=true;
                boolean includeSpecial=true;
                boolean includeDigit=true;
                String password = faker.get(key).internet().password(minLength, maxLength, includeUppercase, includeSpecial, includeDigit);
                Report.updateTestLog(Action, "Generated data: " + password, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, password);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating password: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slug**

**Description**: This function will generate a random slug (like a URL slug)

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slug`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random slug (like a URL slug)", input = InputType.YES, condition = InputType.NO)
        public void slug() {
            try {
                String strObj = Input;
                String slug = faker.get(key).internet().slug();
                Report.updateTestLog(Action, "Generated data: " + slug, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, slug);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating slug: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slugWithSpecs**

**Description**: This function will generate a random slug (like a URL slug) with specs

**Input Format** : DatasheetName:ColumnName

**Condition Format**: list of strings and glue or null, for example: `faker:finance:iban:trial:last:`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slugWithSpecs`](#)   | DatasheetName:ColumnName      | ```list of strings and glue or null```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random slug (like a URL slug) with specs", input = InputType.YES, condition = InputType.YES)
        public void slugWithSpecs() {
            try {
                String strObj = Input;
                List<String> wordsOrNull= new ArrayList<>();
                char splitChar=':';
                int count = (int) Condition.chars().filter(ch -> ch == splitChar).count();
                for(int i=0; i<count; i++)
                {
                    wordsOrNull.add(Condition.split(":", count+1)[i]);
                }
                String glueOrNull=Condition.split(":", count+1)[count];
                String slug = faker.get(key).internet().slug(wordsOrNull, glueOrNull);
                Report.updateTestLog(Action, "Generated data: " + slug, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, slug);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating slug: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **userAgentWithAgentType**

**Description**: This function will generate a user agent with Agent type

**Input Format** : DatasheetName:ColumnName

**Condition Format**:  agent type, for example: `CHROME`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`userAgentWithAgentType`](#)   | DatasheetName:ColumnName      | ```agent type```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random user agent with Agent type", input = InputType.YES, condition = InputType.YES)
        public void userAgentWithAgentType()  {
            try {
                String strObj = Input;
                String option = Condition;
                Internet.UserAgent userAgent = Internet.UserAgent.valueOf(option);
                String userAgent1 = faker.get(key).internet().userAgent(userAgent);
                Report.updateTestLog(Action, "Generated data: " + userAgent1, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, userAgent1);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating slug: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **userAgentAny**

**Description**: This function will generate a random user agent

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`userAgentAny`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random user agent", input = InputType.YES, condition = InputType.NO)
        public void userAgentAny()   {
            try {
                String strObj = Input;
                String userAgentAny = faker.get(key).internet().userAgentAny();
                Report.updateTestLog(Action, "Generated data: " + userAgentAny, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, userAgentAny);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating slug: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **internetUUID**

**Description**: This function will generate a random uuid

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`internetUUID`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate any random uuid", input = InputType.YES, condition = InputType.NO)
        public void internetUUID()   {
            try {
                String strObj = Input;
                String uuid = faker.get(key).internet().uuid();
                Report.updateTestLog(Action, "Generated data: " + uuid, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, uuid);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating slug: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------