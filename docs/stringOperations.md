# **String Operations**

-------------------------------------

!!! info "String Operations"

    Below are actions you may use to perform several string manipulations. 
    
    The result will be stored to dynamic variable *`%variableName%`* provided from the *Condition* column.

-----------------------------------

!!! abstract "Different *Input* formats for String Operations"

    | Input Type | Format |
    |-----------|-------------|
    |  **Hardcoded String** | *`"String value"`* |
    |  **Input from Datasheet** | *`{SheetName:ColumnName}`* |
    |  **Input from Dynamic Variable** | *`%DynamicVariableName%`* |

### **Concat**

**Description** : This function appends the strings provided from the *Input* column.

**Input Format** : Comma separated strings, (i.e. *`"string_value 1"`,`"string_value 2"`,`"string_value 3"`,`"string_value 4"`,`"string_value 5"`*)

**Parameter** : 

`string_value` - set of strings to be concatenated to a new string, max number of `string_value` is `5`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *Concat* | "Hello,"," World","!","!","!" | %variableName% | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | String Operations | *Concat* | {Sheet:Column}," World","!","!","!" | %variableName%  | |<span style="color:Blue"><< *Input from Datasheet*</span> 
    | String Operations | *Concat* | %dynamicVar%," World","!","!","!" | %variableName% | |<span style="color:Brown"><< *Input from variable*</span> 
    
=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *Concat*

    **Sample Test Case:**

    ![Concat Examples](../img/stringoperations/Concat-1.png "examples")

    **Sample Report:**

    ![Concat Examples](../img/stringoperations/Concat-2.png "report")

-----------------------------------------------------

### **GetLength**

**Description** : This function returns the length of the string.

**Input Format** : Single string value, (i.e. *`"string_value"`*)

**Parameter** : 

`string_value` - string value to get length
       
=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *GetLength* | "Hello, World!" | %variableName% | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | String Operations | *GetLength* | {Sheet:Column} | %variableName% | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | String Operations | *GetLength* | %dynamicVar% | %variableName% | |<span style="color:Brown"><< *Input from variable*</span>
    
=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *GetLength*

    **Sample Test Case:**

    ![GetLength Examples](../img/stringoperations/GetLength-1.png "examples")

    **Sample Report:**

    ![GetLength Examples](../img/stringoperations/GetLength-2.png "report")

-----------------------------------------------------

### **GetOccurence**

**Description** : This function returns the number of occurrences of the searched character.

**Input Format** : Comma separated string, (i.e. *`"target_string"`,`"search_character"`*)

**Parameter** : 

`target_string` - target string value to search
                
`search_character` - character value to search from the target string

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *GetOccurence* | "Hello, World!","e" | %variableName% | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | String Operations | *GetOccurence* | {Sheet:Column},"e" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | String Operations | *GetOccurence* | %dynamicVar%,"e" | %variableName% | |<span style="color:Brown"><< *Input from variable*</span>

=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *GetOccurence*

    **Sample Test Case:**

    ![GetOccurence Examples](../img/stringoperations/GetOccurence-1.png "examples")

    **Sample Report:**

    ![GetOccurence Examples](../img/stringoperations/GetOccurence-2.png "report")

-----------------------------------------------------

### **Replace**

**Description** : This function replaces the first or all occurrences of a character or substring within a string.

**Input Format** : Comma separated string, (i.e. *`"string_value"`,`"target_string"`,`"replacement_string"`,`"first/all"`*)

**Parameter** :

`string_value` - original string value to replace 

`target_string` - target string value or substring value to be replaced 

`replacement_string` - string value or substring value to replace the `target_string` in the original `string_value`

`first/all` - type of string replacement if `first` instance only or `all` instance in the original `string_value`   

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *Replace* | "Hello, World!","o","a","first" | %variableName% | |<span style="color:Green"><< *Hardcoded Input, Single character replace first instance only*</span> 
    | String Operations | *Replace* | {Sheet:Column},"o","a","first" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet, Single character replace first instance only*</span>
    | String Operations | *Replace* | %dynamicVar%,"o","a","first" | %variableName% | |<span style="color:Brown"><< *Input from variable, Single character replace first instance only*</span>
    | String Operations | *Replace* | "Hello, World!","o","a","all" | %variableName% | |<span style="color:Green"><< *Hardcoded Input, Single character replace all instance*</span> 
    | String Operations | *Replace* | {Sheet:Column},"o","a","all" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet, Single character replace all instance*</span>
    | String Operations | *Replace* | %dynamicVar%,"o","a","all" | %variableName% | |<span style="color:Brown"><< *Input from variable, Single character replace all instance*</span>
    | String Operations | *Replace* | "apple pie pie","pie","cake","first" | %variableName% | |<span style="color:Green"><< *Hardcoded Input, Multi-character replace first instance only*</span>
    | String Operations | *Replace* | {Sheet:Column},"pie","cake","first" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet, Multi-character replace first instance only*</span>
    | String Operations | *Replace* | %dynamicVar%,"pie","cake","first" | %variableName% | |<span style="color:Brown"><< *Input from variable, Multi-character replace first instance only*</span>
    | String Operations | *Replace* | "apple pie pie","pie","cake","all" | %variableName% | |<span style="color:Green"><< *Hardcoded Input, Multi-character replace all instance*</span>
    | String Operations | *Replace* | {Sheet:Column},"pie","cake","all" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet, Multi-character replace all instance*</span>
    | String Operations | *Replace* | %dynamicVar%,"pie","cake","all" | %variableName% | |<span style="color:Brown"><< *Input from variable, Multi-character replace all instance*</span>
    
=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *Replace*

    **Sample Test Case:**

    ![Replace Examples](../img/stringoperations/Replace-1.png "examples")

    **Sample Report:**

    ![Replace Examples](../img/stringoperations/Replace-2.png "report")

-----------------------------------------------------

### **Split**

**Description** : The function splits the string using the specified delimeter and returns a substring based on the provided index or number of limit the string will be splitted.

**Input Format** : Comma separated string, (i.e. *`"string_value"`,`"delimeter"`,`"index"`,`"limit"`*)

**Parameter** :

`string_value` - string value to split

`delimeter` - separator to split the string

`index` - key index value to return in the action where base index is `0`

`limit` - number of times the string will be splitted

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *Split* | "one@two@three@four","@","1" | %variableName% | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | String Operations | *Split* | {Sheet:Column},"@","1" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | String Operations | *Split* | %dynamicVar%,"@","1" | %variableName% | |<span style="color:Brown"><< *Input from variable*</span>
    | String Operations | *Split* | "one@two@three@four","@","1","2" | %variableName% | |<span style="color:Green"><< *Hardcoded Input, with limited no. of split*</span> 
    | String Operations | *Split* | {Sheet:Column},"@","1","2" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet, with limited no. of split*</span>
    | String Operations | *Split* | %dynamicVar%,"@","1","2"| %variableName% | |<span style="color:Brown"><< *Input from variable, with limited no. of split*</span>
    
=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *Split*

    **Sample Test Case:**

    ![Split Examples](../img/stringoperations/Split-1.png "examples")

    **Sample Report:**

    ![Split Examples](../img/stringoperations/Split-2.png "report")

-----------------------------------------------------
    
### **Substring**

**Description** : This function returns a new string that is a substring of the original string.

**Input Format** : Comma separated string, (i.e. *`"string_value"`,`"begin_index"`,`"end_index(optional)"`*)

**Parameter** :

`string_value` - string value to get a substring value

`begin_index` - starting index of the substring

`end_index`(`optional`) - ending index of the substring 

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *Substring* | "Hello, World!","7" | %variableName% | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | String Operations | *Substring* | {Sheet:Column},"7" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | String Operations | *Substring* | %dynamicVar%,"7" | %variableName% | |<span style="color:Brown"><< *Input from variable*</span>
    | String Operations | *Substring* | "Hello, World!","1","7" | %variableName% | |<span style="color:Green"><< *Hardcoded Input, with end index*</span> 
    | String Operations | *Substring* | {Sheet:Column},"1","7" | %variableName% | |<span style="color:Blue"><< *Input from Datasheet, with end index*</span>
    | String Operations | *Substring* | %dynamicVar%,"1","7"| %variableName% | |<span style="color:Brown"><< *Input from variable, with end index*</span>
    
=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *Substring*

    **Sample Test Case:**

    ![Substring Examples](../img/stringoperations/Substring-1.png "examples")

    **Sample Report:**

    ![Substring Examples](../img/stringoperations/Substring-2.png "examples")

-----------------------------------------------------

### **ToLower**

**Description** : This function converts a String to lowercase.

**Input Format** : Single string value, (i.e. *`"string_value 1"`*)

**Parameter** :

`string_value` - string value to be converted to lowercase

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *ToLower* | "Hello, World!" | %variableName% | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | String Operations | *ToLower* | {Sheet:Column} | %variableName% | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | String Operations | *ToLower* | %dynamicVar% | %variableName% | |<span style="color:Brown"><< *Input from variable*</span>
    
=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *ToLower*

    **Sample Test Case:**

    ![ToLower Examples](../img/stringoperations/ToLower-1.png "examples")

    **Sample Report:**

    ![ToLower Examples](../img/stringoperations/ToLower-2.png "report")

-----------------------------------------------------
    
### **ToUpper**

**Description** : This function converts a String to uppercase.

**Input Format** : Single string value, (i.e. *`"string_value 1"`*)

**Parameter** :

`string_value` - string value to be converted to uppercase

=== "Usage"
        
    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *ToUpper* | "Hello, World!" | %variableName% | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | String Operations | *ToUpper* | {Sheet:Column} | %variableName% | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | String Operations | *ToUpper* | %dynamicVar% | %variableName% | |<span style="color:Brown"><< *Input from variable*</span>
    
=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *ToUpper*

    **Sample Test Case:**

    ![ToUpper Examples](../img/stringoperations/ToUpper-1.png "examples")

    **Sample Report:**

    ![ToUpper Examples](../img/stringoperations/ToUpper-2.png "report")

-----------------------------------------------------
    
### **Trim**

**Description** : This function removes any leading or trailing whitespace characters (including spaces, tabs and newline characters).

**Input Format** : Single string value, (i.e. *`"string_value 1"`*)

**Parameter** : 

`string_value` - string value to be trimmed

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | String Operations | *Trim* | " Hello, World! " | %variableName% | |<span style="color:Green"><< *Hardcoded Input*</span> 
    | String Operations | *Trim* | {Sheet:Column} | %variableName% | |<span style="color:Blue"><< *Input from Datasheet*</span>
    | String Operations | *Trim* | %dynamicVar% | %variableName% | |<span style="color:Brown"><< *Input from variable*</span>
    
=== "Examples"

    Below are sample Test Case and generated report on how to use String Operations *Trim*

    **Sample Test Case:**

    ![Trim Examples](../img/stringoperations/Trim-1.png "examples")

    **Sample Report:**

    ![Trim Examples](../img/stringoperations/Trim-2.png "report")

-------------------------