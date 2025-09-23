# **Creating Mobile App Tests**

## Set up an Appium Configuration

Follow the steps below to create an Appium configuration in INGenious.

* Click on the Configuration icon ![browserConfig](../img/toolui/BrowserConfiguration.png "browserConfig")

* Inside the **Manage Browser** tab, Enter the name of the **Appium Configuation** you want to create, in the `Browser` textbox and hit ++enter++ 

* Inside the **Mobile Tab**, you can set your **Remote URL/Appium** from the textbox. By default, it is set to `http://127.0.0.1:4723/`

     ![createConfig](../img/mobiletesting/sampleRemoteURL.jpeg "remoteurl"){ width=50% }

* Inside the **Capabilities/Options Tab**, you can set your **Appium Capabilities/Options**

     ![createConfig](../img/mobiletesting/sampleCapabilities.jpeg "createConfig"){ width=50% }

* By default, `automationName`, `deviceName`, `platformName` and `platformVersion` are the required key-value pairs for **Appium configuration** when creating new emulators. Additional Appium configurations can be included as needed.

* Click on **Save** button to save your Appium Configuration.

> **Note:** Make sure you have already tested your configurations from Appium Inspector. See section [Appium Inspector](appiuminspector.md) for more details.  

=== "Sample Android Emulator Configurations"

    **Sample Android Emulator INGenious Configurations**

    Remote URL:

    ![createConfig](../img/mobiletesting/remoteurl-android.png "remoteUrl"){ width=50% }
    
    Appium Capabilities/Options:

    ![createConfig](../img/mobiletesting/config-android.png "createConfig"){ width=50% }
   
    **Sample Android Appium Capabilities Set**

    ```json
          {
               "appium:deviceName": "emulator-5554",
               "appium:automationName": "UIAutomator2",
               "appium:platformVersion": "15.0",
               "platformName": "Android",
               "appium:appActivity": ".MainActivity",
               "appium:appPackage": "com.swaglabsmobileapp"
          }
    ```

=== "Sample iOS Emulator Configurations"

    **Sample iOS Emulator INGenious Configurations**

    Remote URL:

    ![createConfig](../img/mobiletesting/remoteurl-ios.png "remoteUrl"){ width=50% }

    Appium Capabilities/Options:

    ![createConfig](../img/mobiletesting/config-ios.png "createConfig"){ width=50% }

    **Sample iOS Appium Capabilities Set**

    ```json
          {
               "appium:udid": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
               "appium:bundleId": "com.saucelabs.SwagLabsMobileApp",
               "appium:automationName": "XCUITest",
               "platformName": "iOS",
               "appium:deviceName": "emulator-ios"
          }
    ```

=== "Sample Lambda Configurations"

    **Sample Lambda INGenious Configurations**

    ***Remote URL***

    Your remote url for Lambda Testing is your connection string with combination of your Lmabda **Username**, **Access key** and `@mobile-hub.lambdatest.com/wd/hub`

    * For this example, remote url is set to `https://<UserName>:<AccessKey>@mobile-hub.lambdatest.com/wd/hub`:

        ![createConfig](../img/mobiletesting/remoteurl-lambda.png "remoteUrl"){ width=50% }

    * To get your Username and Access Token
        * From you Lambda Testing Portal, go to **Home** > **Account Settings** > **Password & Security**
        * Under **Username and Access Key**, copy your **Username** and **Access Key** as shown from example `https://<UserName>:<AccessKey>@mobile-hub.lambdatest.com/wd/hub`.

            ![createConfig](../img/mobiletesting/Lambda-user-token.jpeg "user-token"){ width=60% }
    
    ***Appium Capabilities/Options***

    * For this example, you can set the capabilities as below:

        ![createConfig](../img/mobiletesting/config-lambda.png "createConfig"){ width=50% }

    * To get you `app` capability
        * From you Lambda Testing Portal, go to **Real time** or **Real Device** > **App Testing** > **Virtual Mobile** 
        * Click on the **App Settings,**  

            ![createConfig](../img/mobiletesting/virtualMachine-settings.jpeg "virtual device"){ width=60% }

        * Under **App Settings**, copy your **App Id** to `app` capabilities in INGenious Configurations

            ![createConfig](../img/mobiletesting/AppSettings.png "App Settings"){ width=60% }

    * For Android Mobile in Lambda Testing, you can use capabilities
        * `automatorName` as `UIAutomator2`
        * `platformName` as `Android`
        * `platformVersion` as the Android platform version you want to use

    * For iOS Mobile in Lambda Testing, you can use capabilities
        * `automatorName` as `XCUITest`
        * `platformName` as `iOS`
    
    * You can also add your other desired capabilities for Lambda Testing. 
        * For more information, you can visit **[Desired Capabilities for Lambda Testing](https://www.lambdatest.com/support/docs/desired-capabilities-in-appium/)**
        * or visit **[Lambda Test Automation Capabilities Generator Tool](https://www.lambdatest.com/capabilities-generator/)**
   
    **Sample Lambda Appium Capabilities Set**

    ```json
          {
               "appium:deviceName": "Galaxy S23",
               "appium:automationName": "UIAutomator2",
               "appium:platformVersion": "15.0",
               "platformName": "Android",
               "appium:app": "lt://APPXXXXXXXXXXXXXXX",
               "appium:w3c": "true",
               "appium:language": "nl",
               "appium:isRealMobile": "true",
               "appium:locale": "true",
               "appium:build": "Sample-Build-Name",
               "appium:autoGrantPermissions": "true",
          }
    ```

---------------------------     

## Write Tests

* Head over to the **Design Pane** of INGenious

* Create **Objects** in the Object Repository with appropriate selectors like `xpath`, `AccessibilityId` etc. These can easily be captured from **Appium Inspector**

* Drag and drop the objects into the test case canvas

* Select appropriate **actions** like **`Tap`, `Scroll`** or **`Set`** for each relevant step

=== "Sample Android Test Case"

    ![testcase](../img/mobiletesting/testcase-android.png "testcase")  

=== "Sample iOS Test Case"

    ![testcase](../img/mobiletesting/testcase-ios.png "testcase")  

---------------------------     

## Test Execution - Design Pane

While running the test from the Design Pane, make sure to select the appropriate **Appium Configuration** that was created for the test. You can do that by right clicking on the Run Button and selecting the Configuration.

![execution](../img/mobiletesting/testexecution1.png "execution")  

---------------------------     

## Test Execution - Execution Pane

While running the test from the Execution Pane, make sure to select the appropriate **Appium Configuration** that was created for the test. You can do that by selecting the Configuration in the `Browser` Column.

![execution](../img/mobiletesting/testexecution2.png "execution")  