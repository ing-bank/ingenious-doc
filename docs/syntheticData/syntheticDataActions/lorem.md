# **Faker Actions related to Lorem**

## **loremWord**

**Description**: This function will generate a random Lorem word

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremWord`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem word", input = InputType.YES, condition = InputType.NO)
        public void loremWord() {
            try {
                String strObj = Input;
                String word = faker.get(key).lorem().word();
                Report.updateTestLog(Action, "Generated data: " + word, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, word);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem word: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremWords**

**Description**: This function will generate random Lorem words

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremWords`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem words", input = InputType.YES, condition = InputType.NO)
        public void loremWords() {
            try {
                String strObj = Input;
                List<String> word = faker.get(key).lorem().words();
                Report.updateTestLog(Action, "Generated data: " + word, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, word.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem word: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremWordsWithCount**

**Description**: This function will generate a list of random Lorem words

**Input Format** : DatasheetName:ColumnName

**Condition Format**: word count, for example: `10`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremWordsWithCount`](#)   | DatasheetName:ColumnName      | ```word count```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a list of random Lorem words", input = InputType.YES, condition = InputType.YES)
        public void loremWordsWithCount() {
            try {
                String strObj = Input;
                String countStr = Condition;
                int count=Integer.parseInt(countStr);
                List<String> words = faker.get(key).lorem().words(count);
                Report.updateTestLog(Action, "Generated data: " + words, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, words.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem words: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **sentence**

**Description**: This function will generate a random Lorem sentence

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`sentence`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem sentence", input = InputType.YES, condition = InputType.NO)
        public void sentence() {
            try {
                String strObj = Input;
                String sentence = faker.get(key).lorem().sentence();
                Report.updateTestLog(Action, "Generated data: " + sentence, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, sentence);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem sentence: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **sentenceWithCount**

**Description**: This function will generate random Lorem sentence with a given word count

**Input Format** : DatasheetName:ColumnName

**Condition Format**: word count, for example: `5`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`sentenceWithCount`](#)   | DatasheetName:ColumnName      | ```word count```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem sentence with a given word count", input = InputType.YES, condition = InputType.YES)
        public void sentenceWithCount() {
            try {
                String strObj = Input;
                String wordCountStr = Condition;
                int wordCount=Integer.parseInt(wordCountStr);
                String sentence = faker.get(key).lorem().sentence(wordCount);
                Report.updateTestLog(Action, "Generated data: " + sentence + ": " + sentence, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, sentence);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem sentence: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **sentenceWithCountAndRandomWords**

**Description**: This function will generate random Lorem sentence with a given word count and words to add

**Input Format** : DatasheetName:ColumnName

**Condition Format**: word count and words to add, for example: `5:7`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`sentenceWithCountAndRandomWords`](#)   | DatasheetName:ColumnName      | ```word count and words to add```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem sentence with a given word count and words to add", input = InputType.YES, condition = InputType.YES)
        public void sentenceWithCountAndRandomWords() {
            try {
                String strObj = Input;
                String wordCountStr = Condition.split(":", 2)[0];
                String wordsToAddStr = Condition.split(":", 2)[1];
                int wordCount=Integer.parseInt(wordCountStr);
                int randomWordsToAdd=Integer.parseInt(wordsToAddStr);
                String sentence = faker.get(key).lorem().sentence(wordCount, randomWordsToAdd);
                Report.updateTestLog(Action, "Generated data: " + sentence + ": " + sentence, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, sentence);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem sentence: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **sentences**

**Description**: This function will generate random Lorem sentence with a given sentence count

**Input Format** : DatasheetName:ColumnName

**Condition Format**: sentence count, for example: `6`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`sentences`](#)   | DatasheetName:ColumnName      | ```sentence count```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem sentence with a given sentence count", input = InputType.YES, condition = InputType.YES)
        public void sentences() {
            try {
                String strObj = Input;
                String sentenceCountStr = Condition;
                int sentenceCount=Integer.parseInt(sentenceCountStr);
                String sentence = faker.get(key).lorem().sentence(sentenceCount);
                Report.updateTestLog(Action, "Generated data: " + sentence + ": " + sentence, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, sentence);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem sentence: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **paragraph**

**Description**: This function will generate random Lorem sentence with a given sentence count

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`paragraph`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem paragraph", input = InputType.YES, condition = InputType.NO)
        public void paragraph() {
            try {
                String strObj = Input;
                String paragraph = faker.get(key).lorem().paragraph();
                Report.updateTestLog(Action, "Generated data: " + paragraph, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, paragraph);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraph: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **paragraphWithSentenceCount**

**Description**: This function will generate random Lorem paragraph with a given sentence count

**Input Format** : DatasheetName:ColumnName

**Condition Format**: sentence count, for example: `6`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`paragraphWithSentenceCount`](#)   | DatasheetName:ColumnName      | ```sentence count```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem paragraph with a given sentence count", input = InputType.YES, condition = InputType.YES)
        public void paragraphWithSentenceCount() {
            try {
                String strObj = Input;
                String sentenceCountStr = Condition;
                int sentenceCount=Integer.parseInt(sentenceCountStr);
                String paragraph = faker.get(key).lorem().paragraph(sentenceCount);
                Report.updateTestLog(Action, "Generated data: " + sentenceCount + ": " + paragraph, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, paragraph);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraph: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **paragraphsWithParagraphCount**

**Description**: This function will generate random Lorem paragraphs

**Input Format** : DatasheetName:ColumnName

**Condition Format**: paragraph count, for example: `4`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`paragraphsWithParagraphCount`](#)   | DatasheetName:ColumnName      | ```paragraph count```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a list of random Lorem paragraphs", input = InputType.YES, condition = InputType.YES)
        public void paragraphsWithParagraphCount() {
            try {
                String strObj = Input;
                String paragraphCountStr = Condition;
                int paragraphCount=Integer.parseInt(paragraphCountStr);
                List<String> paragraphs = faker.get(key).lorem().paragraphs(paragraphCount);
                Report.updateTestLog(Action, "Generated data: " + paragraphs, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, paragraphs.toString());
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharacter**

**Description**: This function will generate random Lorem character

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharacter`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem character", input = InputType.YES, condition = InputType.NO)
        public void loremCharacter() {
            try {
                String strObj = Input;
                char character = faker.get(key).lorem().character();
                Report.updateTestLog(Action, "Generated data: " + character, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Character.toString(character));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharacters**

**Description**: This function will generate random Lorem characters

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharacters`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem characters", input = InputType.YES, condition = InputType.NO)
        public void loremCharacters() {
            try {
                String strObj = Input;
                String characters = faker.get(key).lorem().characters();
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharacterIncludeUpperCase**

**Description**: This function will generate random Lorem character including uppercase

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharacterIncludeUpperCase`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem character including uppercase", input = InputType.YES, condition = InputType.NO)
        public void loremCharacterIncludeUpperCase() {
            try {
                String strObj = Input;
                boolean includeUppercase=true;
                char character = faker.get(key).lorem().character(includeUppercase);
                Report.updateTestLog(Action, "Generated data: " + character, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, Character.toString(character));
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharactersIncludeUpperCase**

**Description**: This function will generate random Lorem characters including uppercase

**Input Format** : DatasheetName:ColumnName

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharactersIncludeUpperCase`](#)   | DatasheetName:ColumnName      |   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem characters including uppercase", input = InputType.YES, condition = InputType.NO)
        public void loremCharactersIncludeUpperCase() {
            try {
                String strObj = Input;
                boolean includeUppercase=true;
                String characters = faker.get(key).lorem().characters(includeUppercase);
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharactersWithNumberOfChars**

**Description**: This function will generate random Lorem characters with fixed number of characters

**Input Format** : DatasheetName:ColumnName

**Condition Format**: number of characters, for example: `10`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharactersWithNumberOfChars`](#)   | DatasheetName:ColumnName      | number of characters   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem characters with fixed number of characters", input = InputType.YES, condition = InputType.YES)
        public void loremCharactersWithNumberOfChars() {
            try {
                String strObj = Input;
                String charsStr = Condition;
                int fixedNumberOfCharacters=Integer.parseInt(charsStr);
                String characters = faker.get(key).lorem().characters(fixedNumberOfCharacters);
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharactersWithNumberOfCharsUpperCase**

**Description**: This function will generate random Lorem characters with fixed number of characters and uppercase

**Input Format** : DatasheetName:ColumnName

**Condition Format**: number of characters, for example: `5`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharactersWithNumberOfCharsUpperCase`](#)   | DatasheetName:ColumnName      | ```number of characters```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem characters with fixed number of characters and uppercase", input = InputType.YES, condition = InputType.YES)
        public void loremCharactersWithNumberOfCharsUpperCase() {
            try {
                String strObj = Input;
                String charsStr = Condition;
                int fixedNumberOfCharacters=Integer.parseInt(charsStr);
                boolean includeUppercase=true;
                String characters = faker.get(key).lorem().characters(fixedNumberOfCharacters, includeUppercase);
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharactersWithNumberOfCharsUpperCaseDigit**

**Description**: This function will generate random Lorem characters with fixed number of characters, uppercase and digit

**Input Format** : DatasheetName:ColumnName

**Condition Format**: number of characters, for example: `6`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharactersWithNumberOfCharsUpperCaseDigit`](#)   | DatasheetName:ColumnName      | ```number of characters```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem characters with fixed number of characters, uppercase and digit", input = InputType.YES, condition = InputType.YES)
        public void loremCharactersWithNumberOfCharsUpperCaseDigit() {
            try {
                String strObj = Input;
                String charsStr = Condition;
                int fixedNumberOfCharacters=Integer.parseInt(charsStr);
                boolean includeUppercase=true;
                boolean includeDigit=true;
                String characters = faker.get(key).lorem().characters(fixedNumberOfCharacters, includeUppercase, includeDigit);
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharactersWithinLength**

**Description**: This function will generate random Lorem characters with with min and max length

**Input Format** : DatasheetName:ColumnName

**Condition Format**: minimum and maximum characters, for example: `10:14`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharactersWithinLength`](#)   | DatasheetName:ColumnName      | ```minimum and maximum characters```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem characters with min and max length", input = InputType.YES, condition = InputType.YES)
        public void loremCharactersWithinLength() {
            try {
                String strObj = Input;
                String minStr = Condition.split(":", 2)[0];
                String maxStr = Condition.split(":", 2)[1];
                int minimumLength=Integer.parseInt(minStr);
                int maximumLength=Integer.parseInt(maxStr);
                String characters = faker.get(key).lorem().characters(minimumLength, maximumLength);
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharactersWithinLengthUpperCase**

**Description**: This function will generate random Lorem characters with with min and max length including uppercase

**Input Format** : DatasheetName:ColumnName

**Condition Format**: minimum and maximum characters, for example: `5:9`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharactersWithinLengthUpperCase`](#)   | DatasheetName:ColumnName      | ```minimum and maximum characters```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate random Lorem characters with min and max length including uppercase", input = InputType.YES, condition = InputType.YES)
        public void loremCharactersWithinLengthUpperCase() {
            try {
                String strObj = Input;
                String minStr = Condition.split(":", 2)[0];
                String maxStr = Condition.split(":", 2)[1];
                int minimumLength=Integer.parseInt(minStr);
                int maximumLength=Integer.parseInt(maxStr);
                boolean includeUppercase=true;
                String characters = faker.get(key).lorem().characters(minimumLength, maximumLength, includeUppercase);
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremCharactersWithinLengthUpperCaseDigit**

**Description**: This function will generate random Lorem characters with with min and max length including uppercase and digits

**Input Format** : DatasheetName:ColumnName

**Condition Format**: minimum and maximum characters, for example: `5:12`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremCharactersWithinLengthUpperCaseDigit`](#)   | DatasheetName:ColumnName      | ```minimum and maximum characters```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a list of random Lorem characters with min and max length including uppercase and digits", input = InputType.YES, condition = InputType.YES)
        public void loremCharactersWithinLengthUpperCaseDigit() {
            try {
                String strObj = Input;
                String minStr = Condition.split(":", 2)[0];
                String maxStr = Condition.split(":", 2)[1];
                int minimumLength=Integer.parseInt(minStr);
                int maximumLength=Integer.parseInt(maxStr);
                boolean includeUppercase=true;
                boolean includeDigit=true;
                String characters = faker.get(key).lorem().characters(minimumLength, maximumLength, includeUppercase, includeDigit);
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------

## **loremFixedString**

**Description**: This function will generate random Lorem fixed string

**Input Format** : DatasheetName:ColumnName

**Condition Format**: number of letters, for example: `10`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Synthetic Data     |:green_circle: [`loremFixedString`](#)   | DatasheetName:ColumnName      | ```number of letters```   | |<span style="color:#559BD1">:arrow_left:   *Store in Datasheet*</span> 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.FAKER, desc = "Generate a random Lorem fixed string", input = InputType.YES, condition = InputType.YES)
        public void loremFixedString() {
            try {
                String strObj = Input;
                String countStr = Condition;
                int numberOfLetters=Integer.parseInt(countStr);
                String characters = faker.get(key).lorem().characters(numberOfLetters);
                Report.updateTestLog(Action, "Generated data: " + characters, Status.DONE);
                String sheetName = strObj.split(":", 2)[0];
                String columnName = strObj.split(":", 2)[1];
                userData.putData(sheetName, columnName, characters);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during data generation", ex);
                Report.updateTestLog(Action, "Error generating Lorem paragraphs: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-----------------------------------------------------