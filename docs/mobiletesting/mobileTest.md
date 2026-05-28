# **Creating Mobile App Tests**

## Write Tests

* Head over to the **Design Pane** of INGenious

* Create **Objects** in the Object Repository with appropriate selectors like `xpath`, `AccessibilityId` etc. These can easily be captured from **Appium Inspector**

* Drag and drop the objects into the test case canvas

* Select appropriate **actions** like **`Tap`, `Scroll`** or **`Set`** for each relevant step

=== "Sample Android Test Case"

    ![testcase](../img/mobiletesting/testcase-android.png "testcase")  

=== "Sample iOS Test Case"

    ![testcase](../img/mobiletesting/testcase-ios.png "testcase")

=== "Sample LambdaTest Test Case"

    > Any Android and iOS Test Case can be used as a LambdaTest.<br>
    Setup a LambdaTest configuration by following the steps in [Sample Lambda Configurations](../emulatorsetup/#__tabbed_1_3)

    ![testcase](../img/mobiletesting/testcase-ios.png "testcase")


---------------------------     

## Test Execution - Design Pane

While running the test from the Design Pane, make sure to select the appropriate **Appium Configuration** that was created for the test. You can do that by right clicking on the Run Button and selecting the Configuration.

![execution](../img/mobiletesting/testexecution1.png "execution")  

---------------------------     

## Test Execution - Execution Pane

While running the test from the Execution Pane, make sure to select the appropriate **Appium Configuration** that was created for the test. You can do that by selecting the Configuration in the `Browser` Column.

![execution](../img/mobiletesting/testexecution2.png "execution")

---------------------------  

## Test Results

Results of tests are automatically opened in a test browser after execution.

![result](../img/mobiletesting/passed-mobile-test.png "result")

### Test Results for LambdaTest Test Cases

In addtion to test results from the IDE, results can also be found under **App Automation** in the LambdaTest web application.

![app-automation](../img/lambdatest/lambda-app-automation.png "app-automation")

The results come with a video recording of the executed test steps as well as logs and network information during the run.

![app-automation](../img/lambdatest/lambda-app-result.png "app-automation")

