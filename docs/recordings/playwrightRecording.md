# Playwright Recording
----------------------------------

**Prerequsite :** `Maven` is installed in the system

## Steps for Recording :


 * Launch **INGenious Playwright Studio**

 * Click on the **Recorder** icon

   ![record](../img/recording/1.JPG "record")

   Internally this will call the following `mvn` command : `mvn exec:java -f engine/pom.xml -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args=codegen`

 * The following message will be shown as a reminder:
 
 ![Reminder](../img/recording/RecorderReminder.png "Reminder")
 
 * Playwright logs will be shown during the playwright-recorder's loading process

!!! warning 
    
    If a new version of Playwright is available, this step will try to download that first. So the recorder can time out if the network speed is slow.

    **Pay attention to the logs!!**

 * The **Playwright Inspector** will launch along with **Chromium** browser

 * Enter the URL of the Application Under Test (AUT) in the **Chromium** browser and perform the actions you want to perform on the application

 * You will see the steps getting recorded in the **Playwright Inspector**

 * Once the recording is done, **manually copy the recorded steps using the Copy button in the Playwright Inspector, or by Ctrl + C (Windows) or Command + C (Mac)** so the recorded steps will be saved as a `.txt` file.
 
 * A notification will appear upon successful copy of the recorded steps.

 ![Notification](../img/recording/CopyNotif.png "Notification")
 

## Import the recording

### Import from Playwright Recorder:

 * Once the recorded steps have been succesfully copied, close the Playwright Recorder.

 * A prompt will appear asking whether to proceed with the import. Select Yes.

![Import](../img/recording/Import.png "Import") 

 * Provide a Test Scenario Name or use the default name NewScenario.

![TestScenarioName](../img/recording/TestScenarioName.png "TestScenarioName")

 * Once completed, the recording will be imported and displayed as a **Scenario** and **Test Case** . All relevant **test steps**, along with associated **web objects** and **test data**, will be included. The objects will be loaded into the **Object Repository**.


### Import from `.txt` file:


 * From **INGenious Playwright Studio**, navigate to **Tools** > **Import Playwright Recording** > **Import Playwright Recording**.

 * Locate the **.txt file** and click [OK].

 * The file is immediately rendered as **Scenario** and **Test Case**. All the relevant **test steps** with all the **web objects** and **test data** are imported.

 * All the objects are loaded in the **Object Repository**.

 