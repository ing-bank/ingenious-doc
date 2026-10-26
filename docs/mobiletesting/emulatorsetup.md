# **Appium Configuration**

## Set up an Appium Configuration

Follow the steps below to create an Appium configuration in INGenious.

* Click on the Configuration icon ![browserConfig](/img/toolui/BrowserConfiguration.png "browserConfig"){ width="20px" }

* In the **Manage Devices** tab, click the `+` icon beside the **Device** dropdown, and enter the name of the **Appium Configuation** you want to create and hit ++enter++ 

* Inside the same tab, you can set your **Appium Capabilities/Options** and **Remote URL/Appium** from the textbox. By default, it's set to `http://127.0.0.1:4723/`

     ![createConfig](/img/mobiletesting/sampleRemoteURL.png "remoteurl"){ width=50% }

* By default, `automationName`, `deviceName`, `platformName` and `platformVersion` are the required key-value pairs for **Appium configuration** when creating new emulators. Additional Appium configurations can be included as needed.

* Click on **Save** button to save your Appium Configuration.

> **Note:** Make sure you have already tested your configurations from Appium Inspector. See section [Appium Inspector](tools/appiuminspector.md) for more details.  

-----------------------
## Sample Emulator Configurations

=== "Sample Android Emulator Configurations"
    
    **Sample Android Emulator INGenious Configurations**

    ![createConfig](/img/mobiletesting/config-android.png "createConfig"){ width=50% }
   
    **Sample Android Appium Capabilities Set**

    ```json
          {
               "deviceName": "emulator-5554",
               "automationName": "UIAutomator2",
               "platformVersion": "15.0",
               "platformName": "Android",
               "appActivity": ".MainActivity",
               "appPackage": "com.swaglabsmobileapp"
          }
    ```

=== "Sample iOS Emulator Configurations"

    **Sample iOS Emulator INGenious Configurations**

    ![createConfig](/img/mobiletesting/config-ios.png "createConfig"){ width=50% }

    **Sample iOS Appium Capabilities Set**

    ```json
          {
               "udid": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
               "bundleId": "com.saucelabs.SwagLabsMobileApp",
               "automationName": "XCUITest",
               "platformName": "iOS",
               "deviceName": "emulator-ios"
          }
    ```

=== "Sample Lambda Configurations"

    **Sample Lambda INGenious Configurations**

    ***Remote URL***

    > **Note:** Make sure you have an active account in [TestMu AI / LambdaTest](https://www.testmuai.com/){:target="_blank"}
    
    Your remote url to make connection with **LAMBDATEST** is your connection URL with combination of your Lambda **Username**, **Access key** and extends with `@mobile-hub.lambdatest.com/wd/hub`

    * For this example, remote url is set to `https://<UserName>:<AccessKey>@mobile-hub.lambdatest.com/wd/hub`

        ![createConfig](/img/mobiletesting/remoteurl-lambda.png "remoteUrl"){ width=50% }

    * To get your **Username** and **Access Key**
        * Login to LAMBDATEST Portal, go to **Home** > **Account Settings** > **Password & Security**
        * Under **Username and Access Key**, copy **Username** and **Access Key** as shown from example `https://<UserName>:<AccessKey>@mobile-hub.lambdatest.com/wd/hub`.

            ![createConfig](/img/mobiletesting/Lambda-user-token.jpeg "user-token"){ width=60% }
    
    ***Appium Capabilities/Options***

    * For this example, you can set the capabilities as seen below:

        ![createConfig](/img/mobiletesting/config-lambda.png "createConfig"){ width=50% }

    * To get **`app` capability**   
        * To load application and get **App Id**, follow step from Lambda Official Documentaion 
            * [Application Setup via GUI](https://www.lambdatest.com/support/docs/application-setup-via-gui/)
            * [Application Setup via API](https://www.lambdatest.com/support/docs/application-setup-via-api/)

    * For Android Mobile in LAMBDATEST, you can use capabilities
        * `automatorName` as `UIAutomator2`
        * `platformName` as `Android`
        * `platformVersion` as the Android platform version you want to use

    * For iOS Mobile in LAMBDATEST, you can use capabilities
        * `automatorName` as `XCUITest`
        * `platformName` as `iOS`
    
    * You can also add your other desired capabilities for LAMBDATEST. 
        * For more information related to capabilities, you can visit **[Desired Capabilities for LAMBDATEST](https://www.lambdatest.com/support/docs/desired-capabilities-in-appium/)**
        * To check capabilites, you can visit **[Lambda Test Automation Capabilities Generator Tool](https://www.lambdatest.com/capabilities-generator/)**
   
    **Sample LAMBDATEST Appium Capabilities Set**

    ```json
          {
               "deviceName": "Galaxy S23",
               "automationName": "UIAutomator2",
               "platformVersion": "15.0",
               "platformName": "Android",
               "app": "lt://APPXXXXXXXXXXXXXXX",
               "w3c": "true",
               "language": "nl",
               "isRealMobile": "true",
               "locale": "true",
               "build": "Sample-Build-Name",
               "autoGrantPermissions": "true",
          }
    ```