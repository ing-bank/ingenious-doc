# Playwright Recording
----------------------------------

**Prerequsite :** `Maven` is installed in the system

## Steps for Recording :


 * Launch **INGenious Playwright Studio**

 * Click on the **Recorder** icon

   ![record](../img/recording/1.JPG "record")

   Internally this will call the following `mvn` command : `mvn exec:java -f engine/pom.xml -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args=codegen`

 * A loader will show up while the playwright-recorder is being loaded

> **If a new version of Playwright is available, this step will try to download that first. So the recorder can time out** - Pay attention to the logs!!

 * The **Playwright Inspector** will launch along with chromium browser

 * Enter the URL of the Application Under Test (AUT) in the **chromium** browser and perform the actions you want to perform on the application

 * You will see the steps getting recorded in the **Playwright Inspector**

 * Once the recording is done, **save the steps in a `.txt` file**
 <br>
 Currently only `.txt` is supported. Going forward all formats : `.java`, `.cs`, `.py`, `.js` will be supported for import

 

## Import the recorded steps to create automation test case scaffolding :


 * From **INGenious Playwright Studio**, navigate to **Tools** > **Import Playwright Recording** > **Import Playwright Recording**.

 * Locate the **.txt file** and click [OK].

 * The file is immediately rendered as **Scenario** and **Test Case**. All the relevant **test steps** with all the **web objects** and **test data** are imported.

 * All the objects are loaded in the **Object Repository**.

 