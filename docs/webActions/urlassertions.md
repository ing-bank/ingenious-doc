# Browser URL Assertions

------------------------------

## **assertUrlEquals**

**Description**:  This function will validate if the URL of the current page is equal to user-provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlEquals*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlEquals*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlEquals*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER,
            desc = "Assert if Browser's Url Equals [<Data>]",
            input = InputType.YES)
    public void assertUrlEquals() {
        assertUrl(SpecText.Type.IS);
    }
```

----------------------


## **assertUrlContains**

**Description**:  This function will validate if the URL of the current page has the user-provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlContains*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlContains*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlContains*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
@Action(object = ObjectType.BROWSER,
            desc = "Assert if Browser's Url Contains [<Data>]",
            input = InputType.YES)
    public void assertUrlContains() {
        assertUrl(SpecText.Type.CONTAINS);
    }
```

----------------------


## **assertUrlStartsWith**

**Description**:   This function will validate if the URL of the current page begins with the user-provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlStartsWith*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlStartsWith*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlStartsWith*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.


```java
@Action(object = ObjectType.BROWSER,
            desc = "Assert if Browser's Url StartsWith [<Data>]",
            input = InputType.YES)
    public void assertUrlStartsWith() {
        assertUrl(SpecText.Type.STARTS);
    }
```

----------------------


## **assertUrlEndsWith**

**Description**:   This function will validate if the URL of the current page ends with the user-provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlEndsWith*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlEndsWith*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlEndsWith*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

```java
 @Action(object = ObjectType.BROWSER, desc ="Assert if Browser's Title EndsWith [<Data>]", input =InputType.YES)
    public void assertTitleEndsWith() {
        assertTitle(SpecText.Type.ENDS);
    }

```

----------------------


## **assertUrlMatches**

**Description**:   This function will validate if the URL of current page matches the user-provided data. 

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlMatches*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlMatches*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlMatches*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

```java
@Action(object = ObjectType.BROWSER, desc = "Assert if Browser's Url Matches [<Data>]", input = InputType.YES)
    public void assertUrlMatches() {
        assertUrl(SpecText.Type.MATCHES);
    }
```

----------------------


## **assertUrlIEquals**

**Description**:  This function will validate if the URL of the current page is equals the user-provided data. This function will ignore case of user provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlIEquals*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlIEquals*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlIEquals*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

```java
@Action(object = ObjectType.BROWSER,
            desc = "Assert if Browser's Url Equals [Ignorecase] [<Data>]",
            input = InputType.YES)
    public void assertUrlIEquals() {
        assertUrlI(SpecText.Type.IS);
    }
```

----------------------


## **assertUrlIContains**

**Description**:  This function will validate if the URL of the current page contains the user-provided data. This function will ignore case of the user-provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlIContains*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlIContains*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlIContains*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

```java
@Action(object = ObjectType.BROWSER,
            desc = "Assert if Browser's Url Contains [Ignorecase] [<Data>]",
            input = InputType.YES)
    public void assertUrlIContains() {
        assertUrlI(SpecText.Type.CONTAINS);
    }
```

----------------------


## **assertUrlIStartsWith**

**Description**: This function will validate if the current page URL begins with the user-provided data. This function will ignore case of the user-provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlIStartsWith*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlIStartsWith*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlIStartsWith*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

```java
 @Action(object = ObjectType.BROWSER,
            desc = "Assert if Browser's Url StartsWith [Ignorecase] [<Data>]",
            input = InputType.YES)
    public void assertUrlIStartsWith() {
        assertUrlI(SpecText.Type.STARTS);
    }
```

----------------------


## **assertUrlIEndsWith**

**Description**:  This function will validate if the URL of the current page ends with the user-provided data. This function will ignore case of the user-provided data.

**Input Format** : @Expected text

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Object     |*assertUrlIEndsWith*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Object     |*assertUrlIEndsWith*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Object     |*assertUrlIEndsWith*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

```java
@Action(object = ObjectType.BROWSER,
            desc = "Assert if Browser's Url EndsWith [Ignorecase] [<Data>]",
            input = InputType.YES)
    public void assertUrlIEndsWith() {
        assertUrlI(SpecText.Type.ENDS);
    }
```
