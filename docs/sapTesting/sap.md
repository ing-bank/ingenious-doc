# **Working with SAP**
--------------------------------

## Create your first SAP Test

Follow the steps below to create an SAP-based test case in INGenious.

* Click on the Configuration icon ![browserConfig](../img/toolui/BrowserConfiguration.png "browserConfig")

* Inside the **Manage Browser** tab, enter the name of the **SAP Configuration** you want to create, in the `Browser` textbox and hit ++enter++

* Inside new browser config, set your SAP connection details:
	* `app` - is the path to your SAP GUI logon application
	* `libraryPath` - is the path to your JACOB library
	* `dllPath`- is the path to your JACOB DLL file
	* `connectionName` - is the connection name for your SAP connection
	* `platformName` - is the platform of SAP GUI

![sapConfig](../img/sap/sap-sample-config.png "SAP Config Example"){ width=35% }

* Click on **Save** button to save your SAP Configuration.

> **Note:** Make sure you have the correct SAP connection details from your SAP GUI.

---------------------------     

## Write Tests

* Head over to the **Design Pane** of INGenious

* Create **Objects** in the SAP Object Repository with appropriate attributes like `id`, `name` and `Text`. These can easily be captured using **SAP Sripting Tracker Tool**

* Drag and drop the objects into the test case canvas

* Select appropriate **actions** for each relevant step like **`sapFill`, `sapClick`**, etc. 

![sapConfig](../img/sap/sap-sample-tc.png "SAP Config Example"){ width=85% }

---------------------------     

## Test Execution - Design Pane

While running the test from the Design Pane, make sure to select the appropriate **SAP Configuration** that was created for the test. You can do that by right clicking on the Run Button and selecting the Configuration.

![execution](../img/sap/testexecutionsap1.png "execution"){ width=85% }

---------------------------     

## Test Execution - Execution Pane

While running the test from the Execution Pane, make sure to select the appropriate **SAP Configuration** that was created for the test. You can do that by selecting the Configuration in the `Browser` Column.

![execution](../img/sap/testexecutionsap2.png "execution"){ width=85% }