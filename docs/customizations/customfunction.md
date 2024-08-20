# **Customization & Source Code Maintenance**  
---------------------- 

!!! abstract

    The framework mostly covers all the functions under the predefined list of available actions. But some times your scenario might demand a new **`action`** or **`utility`** to be implemented, for example performing PDF or Excel validation. This can be done by creating your own custom method.


### Requirements 

For your Custom Methods to appear in the INGenious IDE and available for auto-suggestion :

* [x] Custom Methods should be **`public`**.
 
* [x] The return type of Custom Methods should be **`void`**.

*  [x] Custom Methods should not contain parameters (use **Data** or **Input** or **Condition** variable for fetching data from the test case).

*  [x] Custom Method should contain the **`@Action`** annotation in order for it to get auto-suggested in the INGenious IDE.

*  [x] Ensure that you import all the jars mentioned below, in your java file containing the
Custom Method.

```{.java .copy}
import com.ing.engine.commands.General;
import com.ing.engine.core.CommandControl;
import com.ing.engine.support.Status;
import com.ing.engine.support.methodInf.Action;
import com.ing.engine.support.methodInf.ObjectType;
import com.ing.engine.support.methodInf.InputType;
import java.util.logging.Level;
import java.util.logging.Logger;
```

* [x] The java class file containing the Custom Method should always have a **`constructor`** as shown below, since it must extend the **General** class.

```{.java .copy}

public class SampleScript extends General {
    public SampleScript(CommandControl cc) {
        super(cc);
    }

    @Action(object = ObjectType.BROWSER, desc = "<Description of the Method>", input = InputType.YES)
    public void customfunction() {
        try {

            // Here in goes the logic of the method 

        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
        }
    }
}
```

---------------------- 

??? example "Reporting" 
 
    ### Reporting

    To display the status of the custom action in the report, you can use the function **`Report.updateTestLog`** as described below.

    ```{.java .copy}
    Report.updateTestLog("Userdefined Action", "Operation Done successfully", Status.PASS);

    // Possible Statuses are Status.PASS, Status.PASSNS, Status.FAIL, Status.FAILNS, Status.DONE, Status.DEBUG, Status.WARNING,Status.SCREENSHOT
    // NS = No Screenshot
    ```

    To display with **custom html tags** in the report, use the following,

    ```{.java .copy}
    Report.updateTestLog("Userdefined Action", "#CTAG &lt;b&gt; Operation Done successfully&lt;b&gt;;", Status.PASS);
    ```

---------------------- 

??? example "External Libraries" 
    ### Adding External Libraries

    - Create your custom method that uses external jar(s) apart from the existing set
    of libraries under the lib folder.

    - Add your external maven dependencies to the POM file.

    - Always ensure that your custom method is working fine from your source code
    before introducing it in to the framework

    - Run `mvn install` to build the output jar


------------------------------

??? example "Globally Exposed Variables you can use in your Custom Method" 
    ### Globally Exposed Variables


    Following variables are defined internally and can be used in your custom method for deriving various kinds of information like the action in execution or the value stored under the Input column and etc. Given below is the description about each of the variable or keyword on the basis of it's functionality and usage.

    !!! tip "Playwright"
        
        #### **Playwright**
        - **Type** : `Playwright`
        - **Description** : This variable will store the instance of the Playwright for the current execution. Hence you can perform all the Playwright related functions using this.

        :octicons-file-code-16: **Usage** :

        ```{.java .copy}
            Playwright.close();
        ```
    
    
    !!! tip "Page"
       
        #### **Page**
        - **Type** : `Page`
        - **Description** : This variable will store the instance of the Page for the current execution. Hence you can perform all the Page related functions using this.

        :octicons-file-code-16: **Usage** :

        ```{.java .copy}
            Page.bringToFront();
        ```
      

    !!! tip "BrowserContext"
        
        #### **BrowserContext**
        - **Type** : `BrowserContext`
        - **Description** : This variable will store the instance of the BrowserContext for the current execution. Hence you can perform all the BrowserContext related functions using this.

        :octicons-file-code-16: **Usage** :

        ```{.java .copy}
            BrowserContext.newPage();
        ```
    
    !!! tip "Locator"
        
        #### **Locator**
        - **Type** : `Locator`
        - **Description** : This variable corresponds to the Web Object used under the ObjectName column of your currently executing test step. If there is no Object used in the ObjectName column of your Test step, then this variable will be Null. You can perform all WebElement related functions using this variable like for instance.


        :octicons-file-code-16: **Usage** :

        ```{.java .copy}
           Locator.highlight();
        ```
  

    !!! tip "Data"       

        #### Data

        - **Type** : `String`

        - **Description** :This variable stores the **resolved data** from the **Input Column** of the current test step
        in execution. That means if the step is being fed a data from the datasheet like **SheetName:ColumnName** or variable like **%var%** or hardcoded as **@data**, the `Data` variable will hold the **actual value** inside.

        :octicons-file-code-16: **Usage** :

        ```{.java .copy}
        System.out.println(Data + "Resolved Input used in InputColumn in the currentTestStep");
        ```



    !!! tip "Input"

        #### Input


        - **Type** : `String`
        - **Description** : This variable stores the **visible text/string** in the **Input Column** of the current test step
        in execution. That means if the step is being fed a data from the datasheet like **SheetName:ColumnName** or variable like **%var%** or hardcoded as **@data**, the `Input` variable will hold the values as **SheetName:ColumnName**, **%var%** and **@data** respectivey

        :octicons-file-code-16: **Usage** :
        ```{.java .copy}
        System.out.println(Input + "Input used in InputColumn in the currentTestStep");
        ```

    !!! tip "Description"

        #### Description


        - **Type** : `String`
        - **Description** : This variable stores the description present in the description column of the current test step.

        :octicons-file-code-16: **Usage** :
        ```{.java .copy}
        System.out.println(Description + "Description used in DescriptionColumn in the currentTestStep");
        ```

    !!! tip "Action"

        #### **Action**
        - **Type** : `String`
        - **Description** : This variable stores the name of the action used in the Action column of the current test step.

        :octicons-file-code-16: **Usage** :
            ```{.java .copy}
            System.out.println(Action + "Action/Command used in ActionColumn in the currentTestStep");
            ```
        
    !!! tip "Reference"

        #### **Reference**
        - **Type** : `String`
        - **Description** : TThis variable stores the **Name of the Page** given under the Reference column of the current test step in execution. This Name of the Page is actually defined in the Object Repository.

        :octicons-file-code-16: **Usage** :
        ```{.java .copy}
        System.out.println(Reference + "Reference/PageName used in ReferenceColumn in the currentTestStep");
        ```


------------------------------


??? example "Execute A Specific Test Case From Custom Method" 
    ### Execute Test Case from Code

    There is an inbuilt method available called **`executeTestCase`**, which can be used to execute a particular test case under a particular scenario.

    ```{.java .copy}
    public void executeTestCase(String scenarioName, String testCaseName);
    public void executeTestCase(String scenarioName, String testCaseName, int subIteration);
    ```

    The above method will execute the test case under the particular scenario and for that particular **subiteration**.



------------------------------

??? example "Execute An Action From  Custom Method" 
    ### Execute Action from Code

    A method called **executeMethod** is available with the Engine and is overloaded in 4 different ways as follows.
    The name of the Action to be executed, should be passed as an argument and must be same as the action in the Engine.

    === "Type 1"

        ```{.java .copy}
        public void executeMethod(WebElement element, String Action);
        ```
        Using this function you can provide the element and the action name, in the argument list, to execute the action on the element passed. For example,

        ```{.java .copy}
        executeMethod(element, "Click");
        ```

    === "Type 2"
    
        ```{.java .copy}
        public void executeMethod(String Action, String Input);
        ```

        Using this function you can execute the action on the **`current`** element which also requires the information under the Input column or some String information that can be given directly.
        
        For example:

        ```{.java .copy}
        executeMethod("Open", "@http://something");
        executeMethod("Open", input);
        ```

    === "Type 3"
        ```{.java .copy}
        public void executeMethod(WebElement element, String Action, String Input);
        ```

        Using this function you can execute the action on the **supplied element** which requires the information under the **Input column** or some String information that can be given directly.
        
        For example:

        ```{.java .copy}
        executeMethod(element, "Set", input);
        ```

    === "Type 4"

        ```{.java .copy}
        public void executeMethod(String Action);
        ```
        This will just call the method of the action that was instructed. 

    -----------------------------------------------------

    **Any of these overloaded methods can be used that suits your requirements best.**


    Another method to call an action without using the **executeMethod** function is to go with the code described below, Here, we have to set the **Data variable** for the current step and call the `Set` action for execution.

    ```{.java .copy}
    getCommander().Data = "guest";//This line will assign a value to the Data variable used in the current test step.
    new Basic(getCommander()).Set();//This line will call the Set action under the Basic java class file.
    ```

    Another example of using the **getCommander()** function to call an action is as follows.Here the method containing the definition for the action **assertElementNotDisplayed** is available under the **AssertElement** java class file.

    ```{.java .copy}
    new AssertElement(getCommander()).assertElementNotDisplayed();//This line will just make a call to the action "assertlementNotDisplayed"
    ```

------------------------------------

??? example "Access An Object From Object Repository" 

    ### Access Object from OR

    It is possible to access a specific object from the object repository using the function **AObject.findElement** as shown below.

    ```{.java .copy}
    Locator locator = AObject.findElement(ObjectName, Reference);
    ```

    Now all element related functions can be used for this **`element`** variable like;

    ```{.java .copy}
    element.fill(Data);
    ```

    It is also possible to use **conditioned find** method.Suppose you want to find an object on a web page using a particular property,obtained from the **stored set of object properties in the Object Repository (OR)**, then you can use the following function.

    ```{.java .copy}
    Locator locator = AObject.findElement("p", "Yahoo", ObjectProperty.Id);
    ```

    In the example below, a list of objects so obtained can be accessed by storing them in an **ArrayList**.

    ```{.java .copy}
    List <Locator> locatorList= AObject.findElements("p", "Yahoo", ObjectProperty.ClassName);
    ```

    In the above example `object` **p** under the `page` with name **Yahoo** (from the object repository) is found on the web page by using the Id property.

-----------------------------------------------


??? example "If-Else or other Conditions Inside A Custom Method" 
    ### If-Else/Conditional statement

    It is possible to write a custom function, that checks for a condition and if the
    condition passes it will execute a set of code and if it fails then it will execute a
    different set of code.The custom method example **`handleCondition`** defined below, will check
    if the element is displayed and if so, it will execute the test case **`cancelTicket`** but if
    it is not displayed then it will just update the report with a *DONE* status.

    ```{.java .copy}
    public void handleCondition() throws FrameworkException {

        // No argument should be given here. Only then will this function be executed


        //Step 1: Getting object from the object repository
        Locator locator = AObject.findElement("ObjectName", "PageName");

        //Step 2: Base the condition on object being displayed or not
        if (locator.isVisible()) {

            //Calling another test case if the condition is matched

            //Pass the Scenario name,Test case name and sub-iteration index
            executeTestCase("testscenario1", "cancelTicket", 1);
            Report.updateTestLog("Userdefined Action ", "inside reusable", Status.PASS);


            //If needed you can break the test case also by calling existing functions
            executeMethod("StopBrowser");

        } else {

            Report.updateTestLog("Userdefined Action ", "switch to origional", Status.DONE);

        }
    }
    ```

-----------------------------------------------

??? example "Access Test Data Sheet In Custom Method" 
    ### Access Data Sheet from Code

    ??? tip "Local Data Sheet"
        #### Local Data Sheet

        !!! quote "Get Data"
            ##### **getData**

            There are functions to access the data from the datasheet. The **getData**
            function is overloaded in the following ways and can be used accordingly in your
            custom method.

            === "Type 1"

                ```{.java .copy}
                public String getData(String DataSheetName, String ColumnName);
                ```

                Provide the name of the data sheet (**Sample**) and column (**Data1**) that contains the data
                and this function will return a string which is the value of the required data. 
                For instance:

                ```{.java .copy}
                String input = userData.getData("Sample", "Data1");
                ```

            === "Type 2"
                ```{.java .copy}
                public String getData(String DataSheetName, String ColumnName, String Iteration, String SubIteration);
                ```

                Provide the **sheet name, column, iteration and subiteration** values if you want
                to be specific, as shown in the example below;

                ```{.java .copy}
                String input = userData.getData("Sample", "Data1", "1", "1");
                ```
                Here the data stored in the sheet **Sample**, under the column **Data1** having the
                **subiteration** and **iteration** value as **1**, is stored in the input string variable.
                Another way is to provide all the information as given above in the argument list and
                also include the scenario and test case name.

            === "Type 3"

                ```{.java .copy}
                public String getData(String DataSheetName, String ColumnName, String ScenarioName,String TestCase, String Iteration, String SubIteration);
                ```
                Example :
                ```{.java .copy}
                String input = userData.getData("Sample", "Data1", "scenario","testcase", "1", "1");
                ```

                In the example above the data stored in the sheet **Sample** under the column **Data1**
                and belonging to the testcase named **testcase** and **scenario** named scenario having
                the iteration and subiteration value as **1**, is stored in input string.

        !!! quote "Put Data"
            ##### **putData**

            It is also possible to write to the data sheet using **"putData"**.
            The **putData()** function is overloaded in the following ways,

            === "Type 1"
                ```{.java .copy}
                userData.putData("DatasheetName", "ColumnName", "value to be written");
                ```
                Example:

                ```{.java .copy}
                userData.putData("Sample", "Data1", "John Doe");
                ```

                where **Sample** is the datasheet name, **Data1** is the column name and **John Doe** is the value
                to be written under the respective column.

            === "Type 2"

                You can also provide the **iteration** and **subiteration** values in the argument list.

                ```{.java .copy}
                userData.putData("DatasheetName", "ColumnName", "value to be written", "Iterationvalue", "SubIteration value");
                ```
                An example for this is,

                ```{.java .copy}
                userData.putData("Sample", "Data1", "John Doe", "1", "1");
                ```

                where **Sample** is the datasheet name, **Data1** is the column name and **John Doe** is the value
                to be written under the respective column for the iteration value of **1** and subiteration value of **1**.

            === "Type 3"

                Apart from the information above you can also include the test case and scenario name as shown below,

                ```{.java .copy}
                userData.putData("DatasheetName","columnName","value to be written","scenario name","test case name","Iteration value","SubIteration value");
                ```

                An example for the above scenario is shown below,

                ```{.java .copy}
                userData.putData("Sample", "Data1", "John Doe", "scenario", "testcase", "1", "1");
                ```

                where **Sample** is the datasheet name, **Data1** is the column name, **testcase** is the
                testcase name,**scenario** is the scenario name and **John Doe** is the value to be written under
                the respective column for the iteration and subiteration value of **1**.

    ??? tip "Global Data Sheet"
        #### Global Data Sheet

        To access a global data sheet from the custom method to read a global data value, use the method below :

        ```{.java .copy}
        userData.getGlobalData(globalDataID, columnName);
        ```
        Example:
        ```{.java .copy} 
        String datavalue = userData.getGlobalData("Glob1", "username");
        ```

        To write or update a global data sheet, call the method below in your custom method,

        ```{.java .copy}
        userData.putGlobalData(globalDataID, columnName, value);
        ```
        Example:
        ```{.java .copy}
        userData.putGlobalData("Glob1", "username", "LukeSkywalker");
        ```

    ??? tip "Test Data Model"
        #### TestDataModel

        As an alternative, you can use the following code to access the data sheet by its name and update the same, traversing through every record in the test data sheet.

        ```{.java .copy}
        TestDataModel tdModel = Control.getCurrentProject().getTestData().getTestDataByName("TestDataSheetName");
        tdModel.loadTableModel();
        int rowsCount = tdModel.getRowCount();
        for (int row = 0; row < tdModel.getRowCount(); row++) {

            // Where orderId is a column in my data sheet
            int colIndex = tdModel.getColumnIndex("orderId");

            //To get value
            String orderId = (String) tdModel.getValueAt(row, colIndex);

            // To put values in to the sheet
            tdModel.setValueAt("New Value", row, colIndex);
        }

        ```

------------------------------------------------

??? example "Stop Current Execution/Iteration Based On A Condition" 
    ### Stop Current Execution

    The following code can be used to stop the **current iteration** based on a condition.

    ```{.java .copy}
    Boolean something = false;
    if (something) {
        SystemDefaults.stopCurrentIteration.set(true);//Stop the iteration
    }
    ```

    The following code can be used to stop the **current execution** based on a condition.

    ```{.java .copy}
    Boolean something = false;
    if (something) {
        SystemDefaults.stopExecution.set(true);//Stop the execution
    }
    ```

------------------------------------------------

??? example "Get Iteration/Subiteration Value Of The Current TestStep"
    ### Get Iteration/Subiteration

    It is possible to get the value of current iteration using the function **"getIteration"**

    ```{.java .copy}
    String iterationValue=userData.getIteration();
    ```

    This function returns a string value containing the **Iteration number** of the current iteration.


    It is also possible to get the value of current subiteration using the function **getSubIteration**

    ```{.java .copy}
    String subiterationValue=userData.getSubIteration();
    ```

    This function returns a string value containing the **Subiteration number** of the current sub iteration that is in execution.

------------------------------------------------

??? example "Get Current Scenario/TestCase"
    ### Get Current Scenario/TestCase

    The **getScenario** function returns a string value containing the name of the current scenario that is in execution.

    ```{.java .copy}
    String scenarioName=userData.getScenario();
    ```

    The **getCurrentScenario** function returns a string value containing the name of the current `Reusable` scenario that is in execution.

    ```{.java .copy}
    String reusableScenarioName=userData.getCurrentScenario();
    ```

    The **getTestCase** function returns a string value containing the name of the current test case in execution.

    ```{.java .copy}
    String testcaseName= userData.getTestCase();
    ```

    The **getCurrentTestCase** function returns a string value containing the name of the current `Reusable` test case in execution.

    ```{.java .copy}
    String testcaseName= userData.getCurrentTestCase();
    ```

------------------------------------------------

??? example "Get ObjectRepository Properties Of WebElement"

    ### Get ObjectRepository Properties


    It is possible to access the specific property of an element stored in the Object Repository  using the function **`AObject.getObjectProperty()`** described below.

    ```{.java .copy}
    String prop = AObject.getObjectProperty("pageName", "objectName", ObjectProperty.Id);
    ```

    In the above scenario, pass the name of the **page** (under which the object is present
    in the Object Repository), **objectName** and **object property** that you want to access.
    You can also use the following method to get the particular property of the object from the OR.

    ```{.java .copy}
    String prop = AObject.getWebObject("pageName", "objectName").getId();
    prop = AObject.getWebObject(Reference, ObjectName).getAttributeByName(ObjectProperty.Id); //to get current step object's Id property
    ```

------------------------------------------------

??? example "Add Value To A Variable"

    ### Add Value To A Variable

    Suppose you want to create a variable and define a value to it, you can go for **addVar(arg1,arg2)** function or **addGlobalVar(arg1,arg2)** methods.

    The **`addVar(arg1,arg2)`** function takes the variable name and it's value as parameters and is defined under the **com.ing.engine.commands.Command** java file as shown below,

    ```{.java .copy}
    public void addVar(String key, String val) {
    Commander.addVar(key, val);
    }
    ```

    This method can be used as shown below:

    ```{.java .copy}
    addVar("%nameVar%", "LukeSkywalker");
    ```

    > The scope of this variable is only till the end of the execution of the test case in which it is defined.

    The **`addGlobalVar(arg1,arg2)`** function is used to add a value to a variable whose scope is till the end of the execution of the testset i.e. till the end of execution of the last test case under the test set. This function can be used in your custom code as
    shown below:

    ```{.java .copy}
    addGlobalVar("%nameVar%", "LukeSkywalker");
    ```

    This function is defined as shown below under the **com.ing.engine.commands.Command** java file.

    ```{.java .copy}
    public void addGlobalVar(String key, String val) {
        if (key.matches("%.*%")) {
        key = key.substring(1, key.length() - 1);
        }
        Commander.putUserDefinedData(key, val);
    }
    ```

----------------------------------------------

??? example "Access A Variable's Value In Custom Method"

    ### Access A Variable


    The value of a **`variable`** created in your test case can be accessed using the function
    **getVar** which is defined, as shown below, under the **com.ing.engine.commands.Command** java file.

    ```{.java .copy}
    public String getVar(String key) {
        return Commander.getVar(key);
    }
    ```
    This function can be used,as shown below, in your custom method. 

    Provide the variable name between two `percentage symbols`(%%)

    ```{.java .copy}
    String value = getVar("%newVar%");
    System.out.println(value);
    ```
    Suppose you have defined some variables in the **userdefined** tab of the Settings window, which can be opened by navigating through **Run Settings icon** >> **UserDefined Tab**, then you can access them in your custom method in two ways :

    === "**`getVar`**"

        ```{.java .copy}
        String value;
        value = getVar("%userdefinedVar%");
        value = getVar("userdefinedVar");//This also will work
        ```

    === "**`getUserDefinedData`**"

        ```{.java .copy}
        String value = getUserDefinedData("userdefinedVar");
        System.out.println(value);
        ```

---------------------------------

??? example "Sample Custom Method" 

    ### Sample Custom Method

    For creating any Custom Method, a java class is required. The following sample code can be used for understanding the usage of various variables and functions that you can access in your custom method.

    ```java linenums="1"
    package com.ing.engine.commands;

    import com.ing.engine.commands.General;
    import com.ing.engine.core.CommandControl;
    import com.ing.engine.support.Status;
    import com.ing.engine.support.methodInf.Action;
    import com.ing.engine.support.methodInf.ObjectType;
    import com.ing.engine.support.methodInf.InputType;
    import com.microsoft.playwright.Locator;
    import java.util.List;

    //extend Command to access elements

    public class SampleScript extends General {

        public SampleScript(CommandControl cc) {
            super(cc);
        }

        public void textExe() {
            Report.updateTestLog(Action, "textExe", Status.DONE);
            executeTestCase("testWeb", "search");
        }


        @Action(object = ObjectType.BROWSER, desc = "open given url", input = InputType.YES)
        public void prinThis(){  // (1)!
            try {

                /**********************************/
                Locator.click(); // (2)!
                System.out.println(ObjectName + "ObjectName used in ObjectColumn in the currentTestStep");
                System.out.println(Description + "Description used in DescriptionColumn in the currentTestStep");
                System.out.println(Action + "Action/Command used in ActionColumn in the currentTestStep");
                System.out.println(Input + "Input used in InputColumn in the currentTestStep");
                System.out.println(Data + "Resolved Input used in InputColumn in the currentTestStep");
                System.out.println(Reference + "Reference/PageName used in ReferenceColumn in the currentTestStep");

                /**********************************/
                System.out.println(getCurrentBrowserName() + "To get the current browserName");

                /**********************************/                
                String value = getVar("%newVar%"); //(3)!
                System.out.println(value);

                /**********************************/
                value = getVar("%userdefinedVar%"); //(4)!
                value = getVar("userdefinedVar"); //This also will work

                value = getUserDefinedData("userdefinedVar"); //(5)!
                System.out.println(value);

                /**********************************/
                addVar("%dyanmicVar%", "Value to be Stored"); //(6)!
                addGlobalVar("%dyanmicVar%", "Value to be Stored"); //(7)!

                /**********************************/
                AObject.findElement(ObjectName, Reference); 
                AObject.findElements(ObjectName, Reference); // (8)!

                Locator locator = AObject.findElement("p", "Yahoo"); //(9)!
                List<Locator>locatorList = AObject.findElements("p", "Yahoo");                
                System.out.println("No of locators" + locatorList.size());

                /**********************************/
                locator.fill("Normal"); //(10)!
                locator.fill(Data);

                /**********************************/
                String input_text = userData.getData("Sample", "Data1"); //(11)!
                input_text = userData.getData("Sample", "Data1", "1", "1"); //(12)!
                input_text = userData.getData("Sample", "Data1", "scenario","testcase", "1", "1"); //(13)!
                locator.fill(input_text);

                /**********************************/
                userData.putData("Sample", "Data1", "John Doe"); //(14)!
                userData.putData("Sample", "Data1", "John Doe", "1", "1"); //(15)!
                userData.putData("Sample", "Data1", "John Doe", "scenario", "testcase", "1", "1"); //(16)!

                /**********************************/
                TestDataModel tdModel = Control.getCurrentProject().getTestData().getTestDataByName("TestDatasheetName");
                int rowsCount = tdModel.getRowCount();
                for (int row = 0; row < tdModel.getRowCount(); row++) {
    
                    int colIndex = tdModel.getColumnIndex("orderId"); // (17)!                    
                    String orderId = (String) tdModel.getValueAt(row, colIndex);// (18)!               
                    tdModel.setValueAt("New Value", row, colIndex); //(19)! 
                }

                /**********************************/
                Report.updateTestLog("Userdefined Action ", "Operation Done successfully", Status.PASS); //(20)!
                Report.updateTestLog("Userdefined Action ", "#CTAG<b>Operation Done successfully<b>", Status.PASS); //(21)!

                /**********************************/
                userData.getIteration(); //(22)!
                userData.getSubIteration(); //(23)!
                userData.getScenario(); //(24)!
                userData.getTestCase(); //(25)!
                System.out.println(getCurrentBrowserName()); //(26)!

                /**********************************/
                Boolean something = false;
                if (something) {

                    SystemDefaults.stopCurrentIteration.set(true); // (27)! 
                    SystemDefaults.stopExecution.set(true); // (28)!

                }

                /**********************************/
                executeMethod(locator, "Click");
                executeMethod("Open", "@http://something");
                executeMethod("Open", input);
                executeMethod(locator, "Fill", input);

                /**********************************/
                executeTestCase("OnlineShopping", "BuyProduct", 2); //(29)!
                executeTestCase("OnlineShopping", "BuyProduct");   //(30)!

            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            }
        }

               /**********************************/

        public void handleCondition() throws UnCaughtException {            
            Locator locator = AObject.findElement("ObjectName", "PageName");
            if (locator.isVisible()) { // (31)!

                executeTestCase("testscenario1", "cancelTicket", 1); //(32)!
                Report.updateTestLog("Userdefined Action ", "inside reusable", Status.PASS);
                executeMethod("StopBrowser"); //(33)!
            } else {
                Report.updateTestLog("Userdefined Action ", "switch to origional", Status.DONE);
            }
        }
    }
    ```

    1. 
       :material-arrow-right-thin: No argument should be specifed. Only then will your custom method be executed. <br>
       :material-arrow-right-thin: To do any operation before and/or after execution of each Step, add your desired code to functions `beforeStepExecution` / `afterStepExecution` in `Annotation.java` inside `com.ing.engine.core package`. <br>
       :material-arrow-right-thin: To do any operation after execution [execution is finished] add your code to `afterReportComplete` function in `SummaryReport.java` inside `com.ing.engine.reporting package`.
    
    2. Object in ObjectName is resolved as Playwright Locator and assigned to this variable **`Locator`**

    3. If you store some dynamic value in a variable **`%newVar%`** you can get the value from the variable using **`getVar()`**

    4. **`getVar()`** can also be used to fetch user defined data created from **UserDefined Settings panel**

    5. In addition to **`getVar()`**, you can also use **`getUserDefined()`** to fetch user defined data created from **UserDefined Settings panel**

    6. If you want to store some value in a variable[%dyanmicVar%] you can store the value into a variable using **`addVar()`**. The scope is for __Current Testcase only__

    7. Unlike **`addVar()`**, the scope for **`addGlobalVar()`** is for __All Testcases in the Current Execution__

    8. To find the current step's **`object`**

    9. To access the object value pass ObjectName and PageName as inputs.

        :material-arrow-right-thin: ObjectName = **p**

        :material-arrow-right-thin: PageName = **Yahoo**
                
    10. Using this **`locator`** you can perform Playwright Operations

    11. To access the data from DataSheets pass DataSheetName and ColumnName as inputs.
                    
        SheetName = **Sample**, Columnname = **Data1**

        :warning: Don't pass GlobalData as inputsheet

    12. To get values from specified Iteration and Subiteration   
    13. To get values from specified Scenario, Testcase, Iteration and Subiteration
    14. To write values into DataSheet pass DataSheetName and ColumnName as inputs.
       
        SheetName = **Sample**, Columnname = **Data1**, Data = **"John Doe"**

        :warning: Don't pass GlobalData as inputsheet
    15. To write values for specified Iteration and Subiteration 
    16. To write values for specified Scenario, Testcase, Iteration and Subiteration 
    17. Where **orderId** is a column in the data sheet
    18. To get value
    19. To put values in the sheet
    20. To display in Report
    21. To display in Report with custom html tags
    22. To get the current Iteration
    23. To get the current SubIteration
    24. To get the current Scenario
    25. To get the current Testcase
    26. To get the current BrowserName
    27. To stop the current iteration if you want to... based on a condition
    28. Stop the execution
    29. To execute other testcases - **scenario name**, **testcase name**, **subiteration**
    30. **scenario name**, **testcase name**
    31. Basing the condition on a web locator being visible
    32. Calling another test case if the condition is matched
    
        Pass the **Scenario name**, **Testcase name** and **Subiteration index**
    33. If needed you can break the test case also by calling existing function **StopBrowser**  


------------------------------