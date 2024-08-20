# **Frequently Asked Questions (FAQs)**

---------------------------------------
??? example "Unable to launch INGenious, getting "Windows protected your PC" pop-up when clicking on Run.bat file in Windows"
    ## Unable to launch INGenious, getting "Windows protected your PC" pop-up when clicking on Run.bat file in Windows.

    **Why am I unable to launch Ingenious and getting the below mentioned Windows pop-up when clicking on the Run.bat file ?**

    ![WindowsErrorPopUp](img/Things/WindowsErrorPopUp.png "WindowsErrorPopUp")

    Right click on **Run.bat --> Properties -->Unblock --> Apply**
  

---------------------------------------
??? example "Browser not coming up while running tests from Ingenious"
    ## Unable to launch Browser while running the automated test cases from Ingenious.

    **Why am I unable to launch Browser while running the automated test cases from Ingenious ?**

    Try to run the test cases after doing this setting in INGenious Playwirght Studio 
    Navigate to Configuration --> Select Browser Configuration --> Manage Browsers --> Capabilities/Options --> Add 'setHeadless' property with its value as 'False' --> Save**

    ![SetHeadlessConfiguration](img/Things/SetHeadlessConfiguration.png "SetHeadlessConfiguration") 
    
  
--------------------------------------- 

??? example "java.lang.OutOfMemoryError: Java heap space"

    ## Handle `java.lang.OutOfMemoryError: Java heap space`

    **How to handle "java.lang.OutOfMemoryError: Java heap space" ?**

    While executing the test scripts, the BDD json reporter was throwing "java.lang.OutOfMemoryError: Java heap space". This happens because of the large number of test steps with screenshots. In order to handle it, **modify the Run.bat and/or Run.command files to increase the Java contiguous memory allocation before startup.**
    So, here is an example of the corresponding Run.bat file.

    ![JavaHeapSize](img/Things/JavaHeapSize.png "JavaHeapSize")

-------------------------------------

??? example "Q. Unable to launch INGenious, getting "Windows protected your PC" pop-up when clicking on Run.bat file in Windows.

    ## Unable to launch INGenious, getting "Windows protected your PC" pop-up when clicking on Run.bat file in Windows.

    **Why am I unable to launch Ingenious and getting the below mentioned Windows pop-up when clicking on the Run.bat file ?**

    ![WindowsErrorPopUp](img/Things/WindowsErrorPopUp.png "WindowsErrorPopUp")

    Right click on **Run.bat --> Properties -->Unblock --> Apply**
  
--------------------------------------- 