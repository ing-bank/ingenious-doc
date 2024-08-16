---
icon: octicons/browser-16
---

# Browser/Page Actions
------------------------

## **Open**

**Description**: This function will **open the URL** provided by the user in the selected browser

**Input Format** : @URL

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`Open`](#)  | @value       |`optional` page timeout in milliseconds | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`Open`](#)  | Sheet:Column |`optional` page timeout in milliseconds | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`Open`](#)  | %dynamicVar% | `optional` page timeout in milliseconds | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Open the Url [<Data>] in the Browser", input = InputType.YES, condition = InputType.OPTIONAL)
        public void Open() {
            Boolean pageTimeOut = false;
            NavigateOptions navigateOptions = new NavigateOptions();
            try {
                if (Condition.matches("[0-9]+")) {
                    navigateOptions.setTimeout(Double.valueOf(Condition));
                }
                Page.navigate(Data, navigateOptions);
                Report.updateTestLog("Open", "Opened Url: " + Data, Status.DONE);
            } catch (TimeoutError e) {
                Report.updateTestLog("Open",
                        "Opened Url: " + Data + " and cancelled page load after " + Condition + " seconds", Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Open", e.getMessage(), Status.FAIL);
                throw new ForcedException("Open", e.getMessage());
            }
            if (pageTimeOut) {
                setPageTimeOut(300);
            }
        }

    ```

---------------------------------------------------------


## **GoForward**

**Description**:  This function is used to navigate to the next page in history.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | Browser     |:green_circle: [`GoForward`](#)   |   |`optional` page timeout in milliseconds | 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Navigate to the next page in history", input = InputType.NO, condition = InputType.OPTIONAL)
        public void GoForward() {
            GoForwardOptions goForwardOptions = new GoForwardOptions();
            try {
                if (Condition.matches("[0-9]+")) {
                    goForwardOptions.setTimeout(Double.valueOf(Condition));
                }
                Page.goForward(goForwardOptions);
                Report.updateTestLog(Action, "Successfully navigated to the next page", Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
            }

        }
    ```
------------------------------------------------------

## **GoBack**

**Description**:  This function is used to navigate to the previous page in history.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | Browser     |:green_circle: [`GoBack`](#)    |   |`optional` page timeout in milliseconds | 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Navigate to the previous page in history", input = InputType.NO, condition = InputType.OPTIONAL)
        public void GoBack() {
            GoBackOptions goBackOptions = new GoBackOptions();
            try {
                if (Condition.matches("[0-9]+")) {
                    goBackOptions.setTimeout(Double.valueOf(Condition));
                }
                Page.goBack(goBackOptions);
                Report.updateTestLog(Action, "Successfully navigated to the previous page", Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
            }

        }
    ```
------------------------------------------------------

## **Reload**

**Description**:  This method reloads the current page, in the same way as if the user had triggered a browser refresh.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | Browser     |:green_circle: [`Reload`](#)   |   | `optional` page timeout in milliseconds| 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Reload the current page", input = InputType.NO, condition = InputType.OPTIONAL)
        public void Reload() {
            ReloadOptions reloadOptions = new ReloadOptions();
            try {
                if (Condition.matches("[0-9]+")) {
                    reloadOptions.setTimeout(Double.parseDouble(Condition));
                }
                Page.reload(reloadOptions);
                Report.updateTestLog(Action, "Successfully reloaded to the current page", Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
            }

        }
    ```
------------------------------------------------------

## **pause**

**Description**:  This function is used to **pause** the execution for a specific duration

**Input Format** : @duration in milliseconds. Example: @`5000` - this will pause the execution for 5 seconds.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | Browser     |:green_circle: [`pause`](#)  |@value   | | 


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Wait for [<Data>] milli seconds", input = InputType.YES)
        public void pause() {
            try {
                Thread.sleep(Long.parseLong(Data));
                Report.updateTestLog(Action, "Thread sleep for '" + Long.parseLong(Data), Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }

        }
    ```   

----------------------------------------------------

## **clearCookies**

**Description**:  This function is used to **clearCookies** from the browser

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| 
    |------------|--------|--------------|-----------|---------|
    | Browser     |:green_circle: [`clearCookies`](#)  |   | | 


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Clear Cookies", input = InputType.NO)
        public void clearCookies() {      
            try {
                
                BrowserContext.clearCookies();
                Report.updateTestLog(Action, "Cookies clear from the Browser", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```   

----------------------------------------------------

## **storeCookiesInVariable**

**Description**:  This function is used to **storeCookiesInVariable** 

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference| |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`storeCookiesInVariable`](#)  |  %dynamicVar%  | | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column should be passed as a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Store Cookies in a Variable", input = InputType.YES)
        public void storeCookiesInVariable() {
            String strObj = Input;
            String cookieString = "";
            try{
                List<Cookie> cookies = BrowserContext.cookies();
                for (Cookie cookie : cookies)
                {
                    cookieString+="Name="+cookie.name+" ; "+"Value="+cookie.value+" ; "+"Domain="+cookie.domain+" ; "+"URL="+cookie.url+" ; "+"Path="+cookie.path+"\n";
                }
                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, cookieString);
                    Report.updateTestLog(Action, "Cookies stored in variable", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
                }
                
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```   

----------------------------------------------------

## **RecordFromHere**

**Description**:  This function will start `recording` from the current page.

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`RecordFromHere`](#)         |               |           |         |--|

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Start Recorder from the current page", input = InputType.NO, condition = InputType.NO)
        public void RecordFromHere() {
            try {
                Page.pause();
                Report.updateTestLog(Action, "Successfully started Playwright recorder", Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------------------