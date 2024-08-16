# **Troubleshooting**
-------------------------------


Please join this [Teams Channel](https://teams.microsoft.com/l/team/19%3afMr7ZiBuDSIecPQP5yeTdO5yPi9nZtQvx48PSGh0gr41%40thread.tacv2/conversations?groupId=849b8346-0976-4dcb-9e43-b16efaa867dc&tenantId=587b6ea1-3db9-4fe1-a9d7-85d4c64ce5cc) to post questions or inquiries about the solution. The community will try to respond.

-------------------------------

## Error in Connection

Follow the below steps for such scenario:

**Checking Connection status and establishing the same**

**For Chrome and Firefox:**

Follow the steps below to troubleshoot the "error in Connection" error message, 
 
 * Open the **options window, right-click** the add-on to launch options window in **chrome** and use the shortcut **Ctrl+Shift+O** in firefox for the same.

 * Launch **spy or heal or record** from the IDE 

 * Click on **Test Connection**, use the default port **8887**, this port can also be changed as per your choice.

 * If you are getting a **red bulb**, the certificate is not installed properly, so click on the bulb again, you will be navigated to the url **https://localhost:8887/status**, you need to give "**Proceed to unsafe**" in chrome and **Add exception** in Firefox to get to this link

 * If you do not get this message then you need to install the certificates manually.


> **NOTE**: A green bulb indicates that the connection between browser extension and the UI is established and is working fine.

------------------------------------------

## Unable To Open The Framework After Introducing Your Custom Method

This happens when the **ingenious-engine-<version_number>.jar** found in **INGenious
installation_location/lib**, gets corrupted while exporting the **ingenious-engine-<version_number>.jar** back from **Engine** or while inject script is performed. You might get an exception stating that **main class not found**.

To overcome this issue, always take a backup of the **ingenious-engine-<version_number>.jar** before you export the jar from **Engine**. So even when the jar is corrupt you can still replace the existing jar by the new one. Also do not change the name of the **ingenious-engine-<version_number>.jar** available inside the lib folder.

Another alternative is to delete the **recent items** file present in the installation location when INGenious is closed and open again.

> **Note:** Please do not take the back up in the same location or inside the lib folder. Place it in a different location.

If you face this issue after performing inject script then delete the **.class file** of your custom method found in the **userdefined** folder of installation location and close and reopen.

> **Note:** This could also be because the **.jar** files present in the **location\lib\commands** might have got corrupted. So you can simply remove those files to open INGenious.



**How To Hard Code Java Path Variable For INGenious**

> It is possible to hard code the java path in the **Run.bat** file.Refer the section below on how it can be done.

**Prerequisites**

Following must be installed in your system:

 * INGenious setup

 * Java 11 and above

 **How to do it?**

 * Navigate to the location where **INGenious** is installed in your system.

 * Right-click the **Run** batch file.

 * Click the edit option in the context menu.

 * Give the path of the **jre** location under the **'SET PATH'** like this, **SET PATH="C:\Program Files\Java\jdk1.x.x_xx\jre\bin"**.

 * Save the file.

 * Double-click the **Run.bat** file and launch Application.

 -----------------------------------------------


##	If you get a certification path error like this :

`PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target` 

You need to add the certificate of the application whose APIs you are trying to test. This error can also come if the certificates of Global Selenium Grid is not added (in case of Web Testing using Selenium Grid)

To add the certificate follow the steps below :

a.	Download the certificate. you can refer to [these](https://medium.com/@menakajain/export-download-ssl-certificate-from-server-site-url-bcfc41ea46a2) steps.

b. Create a folder called `Security` in your INGenious root instance.

c. Copy the existing Java `cacerts` file to this folder. Also copy the above downloaded certificate file to this location.

e. Using command prompt, navigate to this `Security` folder

d. Import the Trusted Root Certificate into your `cacerts` keystore, using following command :

`<path/to/your>keytool -import -trustcacerts -keystore cacerts -storepass changeit -alias <logical_name_of_your_cert> -file your_certificate.crt`

Example :

`"C:\Program Files\Java\jdk-11.0.2\bin\keytool" -import -trustcacerts -keystore cacerts -storepass changeit -alias testApp -file testApp.crt`

e. Make sure in your INGenious `Run.bat` or/and `Run.command file`, the reference of the above `cacerts` is present.

**Run.bat**

```powershell

@echo off
pushd %~dp0

rem For App to load lib from
SET APP_CLASSPATH=lib\*;lib\clib\*

IF "%~1" == "" (
start javaw -Xms128m -Xmx1024m -Dfile.encoding=UTF-8 -Djavax.net.ssl.trustStore=Security\cacerts -Djavax.net.ssl.trustStorePassword=changeit -cp ingenious-ide-1.1.jar;%APP_CLASSPATH%; com.ing.ide.main.Main %*
) ELSE (
java -Xms128m -Xmx1024m -Dfile.encoding=UTF-8 -cp ingenious-ide-1.1.jar;%APP_CLASSPATH%; com.ing.ide.main.Main %*
)



```



