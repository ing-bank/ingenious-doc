# **Working with INGenious**  
-----------------------------------


### **Menu Ribbon**


=== ":gear: Setting options"
     ![tools](img/toolui/01.png "tools")
  

=== ":octicons-play-16: Execution options"
      ![execution](img/toolui/2.JPG "execution")     

 <br>
----------------------------------------------------------------------
------------------------------------ 
 </br>
 

### **Test Design Pane**

 This is where the test cases are designed and debugged. On opening the framework, the user, by default, lands on this pane.

 ![design](img/toolui/design.png "design")

 **The Design Pane is composed of the following 5 sections (as shown in the picture above):**


=== ":one: Test Plan"
      This is where the Test Scenarios and Test Cases are created and organized.
      Every `Scenario` in the INGenious IDE , is a `Directory` in the backend and every `Test case` is a `.csv` file.

      To see this, you can navigate to the location of your tool, then `Projects` :material-arrow-right: `Your Project` :material-arrow-right: `Test Plan`

      ![testplan1](img/toolui/TestPlan1.JPG "testplan1")

      If you select a Scenario or Test Case and **Right Click**, you will have some interesting and handy options to work with :

      ![testplan2](img/toolui/TestPlan2.JPG "testplan2")
  

=== ":two: Reusable Components"
       This is where the **Reusable** Test Scenarios and Test Cases (**logical grouping of test steps**) are created and organized. Every `Scenario` in the INGenious IDE , is a `Directory` in the backend and every `Test case` is a `.csv` file.

      To see this, you can navigate to the location of your tool, then `Projects` :material-arrow-right: `Your Project` :material-arrow-right: `Test Plan`

      ![reusables](img/toolui/Reusables.JPG "reusables")

      What differentiates the Scenarios and Test Cases in the Test Plan compared to those in the Reusable Component is the purpose :
      * **Test Plan** is supposed contain Functional/Regression/E2E/Business Test Cases
      * **Reusable Component** is supposed contain logical test step groupings, to be used in multiple test cases in the test plan.

      The tool makes use of the **`ReusableComponent.xml`** located in the Project Location, to differentiate between the above 2 type :

      Here is the `ReusableComponent.xml` for the above example :

      ``` xml

         <Root ref="Example" type="RC">
            <Folder ref="UI">
               <Scenario ref="Common">
                  <TestCase exeType="Executable" ref="Login"/>
               </Scenario>
               <Scenario ref="Purchase">
                  <TestCase exeType="Executable" ref="Add to Cart"/>
                  <TestCase exeType="Executable" ref="Checkout"/>
                  <TestCase exeType="Executable" ref="Logout"/>
               </Scenario>
            </Folder>
         </Root>

      ```

      If you select a Reusable Scenario or Reusable Test Case and **Right Click**, you will have some interesting and handy options to work with :

      ![reusable1](img/toolui/Reusables2.JPG "reusables1")

=== ":three: Test Steps"

      This is the canvas where you have your test steps in sequential order

      ![steps1](img/toolui/TestSteps1.JPG "steps1")

      To make working simple, intuitive and easy, you can also use the **drag and drop** to create test steps.

      In the following example, we can create the **Login** Reusable simply by **dragging and dropping the objects** from the Object Repository and parameterizing them by **dragging and dropping the datasheet columns**

      ![drag_drop1](img/toolui/draganddrop1.gif "drag_drop1")
     

      As a best practice, it is advisable to compose your test case **only with Reusables** and not have any loose (orphan) steps.

      You can also drag and drop the Reusables to create test cases like this :

      ![drag_drop2](img/toolui/draganddrop2.gif "drag_drop2")
      
  

=== ":four: Test Data"
      This is the area where you can set up your test data in multiple sheets.

      ![data1](img/toolui/Data1.JPG "data1")

      If you select a data cell and **Right Click**, you will have some interesting and handy options to work with :

      ![data3](img/toolui/data3.JPG "data3")

      **Set up Multiple Test Environments**

      To set up environment based execution, you can set up mutiple environments following the 5 steps as below :

      ![data2](img/toolui/data2.JPG "data2")

      * **Step 1** : From **Test Data** >> Make sure **Multiple Environments** is selected
      * **Step 2** : Click the **[+]** icon in the Data Section, to add a new Environment
      * **Step 3** : Enter the [Environment] Name
      * **Step 4** : Check **[Copy Data from Other Environments]**
      * **Step 5** : Select the Environment and the corresponding Data sheets to be copied and then click **[Create] Button**

=== ":five: Object Repository"
      This is the area where the Locators/Objects are present along with the multiple attributes/properties to be used to find that element on the Application.

      ![or1](img/toolui/OR1.JPG "or1")
      
      If you select a Property and **Right Click**, you will have some interesting and handy options to work with. These options are applicable to used for :

      * Selected Object
      * All objects in the Page
      * All Objects in the OR 


      ![or2](img/toolui/OR2.JPG "or2")

 


 <br>
----------------------------------------------------------------------
------------------------------------ 
 </br>

### **Test Execution Pane**

 ![nav1](img/toolui/NavigateToExecute.png "nav1")

In this pane we can club our test cases together into logical **test sets** or **test suites** and execute them - Either locally (on the workstation) or via a CICD pipeline.

 ![execution](img/toolui/execution.JPG "execution")

 * **Step 1** : Right Click on the Project Name :material-arrow-right: **Add Release** :material-arrow-right: Right Click on the Release Name :material-arrow-right: **Add TestSet**
 * **Step 2** : Select the test cases that you want to add to the set. You can do individual selections or bulk selection by simply selecting the entire Scenario. Once selected, click on the <span style="color:Green">**Green :material-arrow-left: Arrow**</span> to pull your selections into the set.
 * **Step 3** : Order the Test Cases in the sequence of your choice. Choose the appropriate Browsers.
 * **Step 4** : Click on the **gear icon** :gear: and open up the **Run Settings**. Here you can configure many settings like :
    * Parallel Thread count
    * Execution Mode as Grid or Local
    * Which Environment to pick for execution

Once done, we are good to start our execution by clicking on the <span style="color:Green">**Green Play/Run button :octicons-play-16:**</span>

 <br>
----------------------------------------------------------------------
------------------------------------ 
 </br>

### **Report/Dashboard Pane**

 ![nav2](img/toolui/NavigateToDashboard.png "nav2")

In this pane we can view the detailed summary report and even access historical individual reports.

The **Detailed Summary Report** tab looks like this :

![dashboard1](img/toolui/Dashboard1.JPG "dashboard1")


The **Latest Summary Report** tab looks like this :

![dashboard2](img/toolui/Dashboard2.JPG "dashboard2")

[Browser Testing](browsertesting/index.md){ .md-button } [API Testing](api.md){ .md-button }


 <br>
----------------------------------------------------------------------
------------------------------------ 
 </br>

### **Search Functionality**

 ![search](img/toolui/Search1.png "search")

In the above image you can see how INGenious allows you to search for your assets very easily.

   * Test Cases 
   * Test Steps 
   * Test Data 
   * Objects

To activate the **Search Bar**, simply click on the corresponding pane and press :

++ctrl+f++  :arrow_right: For Windows

++cmd+f++   :arrow_right: For Mac

To do a search on Table headers or Column Names, just prepend the **@** symbol before your search text :

![headersearch](img/toolui/Search2.png "headersearch")

  <br>
----------------------------------------------------------------------
------------------------------------ 
 </br>

### Inspiration

The Framework is inspired from :

* [CITS](https://github.com/CognizantQAHub/Cognizant-Intelligent-Test-Scripter)
