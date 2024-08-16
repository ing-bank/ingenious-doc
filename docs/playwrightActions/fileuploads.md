---
icon: material/upload
---


# File Upload Actions
------------------------

## **SetInputFile**

**Description**: This function is used to **set a single file** for upload.

**Input Format** : @File Path

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle:[`SetInputFile`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle:[`SetInputFile`](#)  | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle:[`SetInputFile`](#) | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Set Single InputFile path in [<Object>]", input = InputType.YES)
        public void SetInputFile() {
            try
            {
            Locator.setInputFiles(Paths.get(Data));
            Report.updateTestLog(Action, "File Path '" + Data
                            + "' is set on [" + ObjectName +"]", Status.DONE);
            }
            catch (Exception e){
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **SetInputFiles**

**Description**: This function is used to **set multiple files** for upload

**Input Format** : @File Paths seperated by Pipe. For example `Path1`|`Path2`|`Path3`|`Path4`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle:[`SetInputFiles`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle:[`SetInputFiles`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle:[`SetInputFiles`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Set Multiple InputFile paths in [<Object>]", input = InputType.YES)
        public void SetInputFiles() {
            try
            {
            String paths[] = Data.split("|");
            Path filepaths[] = new Path[paths.length];
            for (int i=0;i<paths.length;i++){
                filepaths[i] = Paths.get(paths[i]);
            }
            Locator.setInputFiles(filepaths);
            Report.updateTestLog(Action, "File Paths '" + Data
                            + "' are set on" + " from list [" + ObjectName +"]", Status.DONE);
            }
            catch (Exception e){
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }

    ```

----------------------

## **RemoveInputFile**

**Description**: This function is used to **remove all selected files** from upload object.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle:[`RemoveInputFile`](#)   |       |       | PageName|


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Remove all selected files from [<Object>]", input = InputType.YES)
        public void RemoveInputFile() {
            try
            {
            Locator.setInputFiles(new Path[0]);
            Report.updateTestLog(Action, "File Path '" + Data
                            + "' is removed from [" + ObjectName +"]", Status.DONE);
            }
            catch (Exception e){
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **FileChooser**

**Description**: This function is used to **set file paths** to a **File Chooser** object.

**Input Format** : @File Path

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle:[`FileChooser`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle:[`FileChooser`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle:[`FileChooser`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Set InputFile path in [<Object>]", input = InputType.YES)
        public void FileChooser() {
            try
            {
            FileChooser fileChooser = Page.waitForFileChooser(() -> Locator.click());
            fileChooser.setFiles(Paths.get(Data));
            Report.updateTestLog(Action, "File Path '" + Data
                            + "' is set on [" + ObjectName +"]", Status.DONE);
            }
            catch (Exception e){
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **DownloadandSaveAs**

**Description**: This function is used to **download a file and save it in a desired path**.

**Input Format** : @File Path

**Condition Format** : Optional. Leave it blank if you want to handle the file name as default. If you want a specific name, pass it in the Condition.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle:[`DownloadandSaveAs`](#)   | @value       | FileName     | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Object     |:green_circle:[`DownloadandSaveAs`](#)   | Sheet:Column |  FileName     | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Object     |:green_circle:[`DownloadandSaveAs`](#)   | %dynamicVar% |  FileName     | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Set InputFile path in [<Object>]", input = InputType.YES, condition = InputType.OPTIONAL)
        public void DownloadandSaveAs() {
            String fileName = "";
            try
            {
            Download download  = Page.waitForDownload(() -> Locator.click());
            if (!Condition.isEmpty())
                fileName = Condition;
            else
                fileName = download.suggestedFilename();
            download.saveAs(Paths.get(Data,fileName));
            Report.updateTestLog(Action, "File downloaded at path '" + Data + "'", Status.DONE);
            }
            catch (Exception e){
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```