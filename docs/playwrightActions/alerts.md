---
icon: material/alert
---

# Alerts

----------------------------------

## **answerNextAlert**

**Description**:  This function will **answer the next alert** with given data

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`answerNextAlert`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`answerNextAlert`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`answerNextAlert`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Answer the next alert with [<Data>]", input = InputType.YES)
        public void answerNextAlert() {
            String setAlertText = Data;
            try {
                Page.onceDialog(dialog -> {
                    dialog.accept(setAlertText);
                });
                Report.updateTestLog(Action, "Message '" + setAlertText
                        + "' will be set in the next alert window", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------

## **answerAllAlerts**

**Description**:  This function will **answer all alerts** with given data

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`answerAllAlerts`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`answerAllAlerts`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`answerAllAlerts`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Answer all the alerts with [<Data>]", input = InputType.YES)
        public void answerAllAlerts() {
            String setAlertText = Data;
            try {
                Page.onDialog(dialog -> {
                    dialog.accept(setAlertText);
                });
                Report.updateTestLog(Action, "Message '" + setAlertText
                        + "' will be set in all the alert windows", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------

## **acceptNextAlert**

**Description**:  This function will **accept next alert**

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  
    |------------|----------------------------|---------------|-----------|---------|
    | Browser     |:green_circle: [`acceptNextAlert`](#)   |       |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Accept the next alert")
        public void acceptNextAlert() {
            try {
                Page.onceDialog(dialog -> {
                    dialog.accept();
                });
                Report.updateTestLog(Action, "The next alert will be accepted", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------

## **acceptAllAlerts**

**Description**:  This function will **accept all alerts**

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  
    |------------|----------------------------|---------------|-----------|---------|
    | Browser     |:green_circle: [`acceptAllAlerts`](#)   |       |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Accept all the alerts")
        public void acceptAllAlerts() {
            try {
                Page.onDialog(dialog -> {
                    dialog.accept();
                });
                Report.updateTestLog(Action, "All alerts will be accepted", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------

## **dismissAllAlerts**

**Description**:  This function will **dismiss all alerts**

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  
    |------------|----------------------------|---------------|-----------|---------|
    | Browser     |:green_circle: [`dismissAllAlerts`](#)   |       |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Dismiss all alerts")
        public void dismissAllAlerts() {
            try {
                Page.onDialog(dialog -> {
                    dialog.dismiss();
                });
                Report.updateTestLog(Action, "All alerts will be dismissed",
                        Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------

## **dismissNextAlert**

**Description**:  This function will **dismiss next alert**

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  
    |------------|----------------------------|---------------|-----------|---------|
    | Browser     |:green_circle: [`dismissNextAlert`](#)   |       |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Dismiss the next alert")
        public void dismissNextAlert() {
            try {
                Page.onceDialog(dialog -> {
                    dialog.dismiss();
                });
                Report.updateTestLog(Action, "Next alert will be dismissed",
                        Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------

## **storeAlertMessageinVariable**

**Description**:  This function will **store alert message in a runtime variable**

**Input:** %dynamicVar%

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  
    |------------|----------------------------|---------------|-----------|---------|
    | Browser     |:green_circle: [`storeAlertMessageinVariable`](#)  |  %varname%     |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Store next Alert message into the Runtime variable: [<Data>]", input = InputType.YES)
        public void storeAlertMessageinVariable() {
            String strObj = Input;
            try {
                Page.onceDialog(dialog -> {           
                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, dialog.message());
                    Report.updateTestLog(Action, "Alert Message " + dialog.message() + " is stored in variable " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
                }
            });
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------

## **storeAlertTypeinVariable**

**Description**:  This function will **store alert type in a runtime variable**

**Input:** %dynamicVar%

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  
    |------------|----------------------------|---------------|-----------|---------|
    | Browser     |:green_circle: [`storeAlertTypeinVariable`](#)   |  %varname%     |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Store Alert type into the Runtime variable: [<Data>]", input = InputType.YES)
        public void storeAlertTypeinVariable() {
            String strObj = Input;
            try {
                Page.onceDialog(dialog -> {           
                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, dialog.type());
                    Report.updateTestLog(Action, "Alert Type " + dialog.type() + " is stored in variable " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
                }
            });
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------

## **storeDefaultAlertValueinVariable**

**Description**:  This function will **store default alert value in a runtime variable**

**Input:** %dynamicVar%

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  
    |------------|----------------------------|---------------|-----------|---------|
    | Browser     |:green_circle: [`storeDefaultAlertValueinVariable`](#)   |  %varname%     |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Store default Alert value into the Runtime variable: [<Data>]", input = InputType.YES)
        public void storeDefaultAlertValueinVariable() {
            String strObj = Input;
            try {
                Page.onceDialog(dialog -> {           
                if (strObj.startsWith("%") && strObj.endsWith("%")) {
                    addVar(strObj, dialog.defaultValue());
                    Report.updateTestLog(Action, "Default Alert Value " + dialog.defaultValue() + " is stored in variable " + strObj, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Invalid variable format", Status.DEBUG);
                }
            });
            } catch (Exception e) {
                Report.updateTestLog(Action, e.getMessage(), Status.FAILNS);
                Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, null, e);
            }
        }
    ```
----------------------------------