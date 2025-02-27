# **Faker Actions related to Slack Emoji**

## **slackEmoji**

**Description**: This function will generate a random Slack emoji

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmoji`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji", input = InputType.YES, condition = InputType.NO)
        public void slackEmoji() {
            try {
                String strObj = Input;
                String emoji = faker.get(key).slackEmoji().emoji();
                Report.updateTestLog(Action, "Generated data: " + emoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, emoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack People Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slackEmojiPeople**

**Description**: This function will generate a random Slack emoji related to people

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmojiPeople`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji related to people", input = InputType.YES, condition = InputType.NO)
        public void slackEmojiPeople() {
            try {
                String strObj = Input;
                String peopleEmoji = faker.get(key).slackEmoji().people();
                Report.updateTestLog(Action, "Generated data: " + peopleEmoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, peopleEmoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack People Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slackEmojiNature**

**Description**: This function will generate a random Slack emoji related to nature

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmojiNature`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji related to nature", input = InputType.YES, condition = InputType.NO)
        public void slackEmojiNature() {
            try {
                String strObj = Input;
                String natureEmoji = faker.get(key).slackEmoji().nature();
                Report.updateTestLog(Action, "Generated data: " + natureEmoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, natureEmoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack Nature Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slackEmojiFoodAndDrink**

**Description**: This function will generate a random Slack emoji related to food and drink

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmojiFoodAndDrink`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji related to food and drink", input = InputType.YES, condition = InputType.NO)
        public void slackEmojiFoodAndDrink() {
            try {
                String strObj = Input;
                String foodAndDrinkEmoji = faker.get(key).slackEmoji().foodAndDrink();
                Report.updateTestLog(Action, "Generated data: " + foodAndDrinkEmoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, foodAndDrinkEmoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack Food and Drink Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slackEmojiCelebration**

**Description**: This function will generate a random Slack emoji related to celebration

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmojiCelebration`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji related to celebration", input = InputType.YES, condition = InputType.NO)
        public void slackEmojiCelebration() {
            try {
                String strObj = Input;
                String celebrationEmoji = faker.get(key).slackEmoji().celebration();
                Report.updateTestLog(Action, "Generated data: " + celebrationEmoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, celebrationEmoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack Celebration Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slackEmojiActivity**

**Description**: This function will generate a random Slack emoji related to activity

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmojiActivity`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji related to activity", input = InputType.YES, condition = InputType.NO)
        public void slackEmojiActivity() {
            try {
                String strObj = Input;
                String activityEmoji = faker.get(key).slackEmoji().activity();
                Report.updateTestLog(Action, "Generated data: " + activityEmoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, activityEmoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack Activity Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slackEmojiTravelAndPlaces**

**Description**: This function will generate a random Slack emoji related to travel and places

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmojiTravelAndPlaces`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji related to travel and places", input = InputType.YES, condition = InputType.NO)
        public void slackEmojiTravelAndPlaces() {
            try {
                String strObj = Input;
                String travelAndPlacesEmoji = faker.get(key).slackEmoji().travelAndPlaces();
                Report.updateTestLog(Action, "Generated data: " + travelAndPlacesEmoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, travelAndPlacesEmoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack Travel and Places Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slackEmojiObjectsAndSymbols**

**Description**: This function will generate a random Slack emoji related to objects and symbols

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmojiObjectsAndSymbols`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji related to objects and symbols", input = InputType.YES, condition = InputType.NO)
        public void slackEmojiObjectsAndSymbols() {
            try {
                String strObj = Input;
                String objectsAndSymbolsEmoji = faker.get(key).slackEmoji().objectsAndSymbols();
                Report.updateTestLog(Action, "Generated data: " + objectsAndSymbolsEmoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, objectsAndSymbolsEmoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack Objects and Symbols Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **slackEmojiCustom**

**Description**: This function will generate a random Slack emoji related to custom emojis

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`slackEmojiCustom`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Slack emoji related to custom emojis", input = InputType.YES, condition = InputType.NO)
        public void slackEmojiCustom() {
            try {
                String strObj = Input;
                String customEmoji = faker.get(key).slackEmoji().custom();
                Report.updateTestLog(Action, "Generated data: " + customEmoji, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, customEmoji);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Slack Custom Emoji: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------