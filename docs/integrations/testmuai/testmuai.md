# **LambdaTest (TestMu AI) Test Manager Integration** 
-------------------------------------------

!!! abstract "Using Test Manager"

    TestMu AI, part of the LambdaTest platform, provides centralized test management and execution visibility for INGenious test runs. By integrating INGenious with TestMu AI, teams can consolidate automated execution results, track build history, review execution trends, and collaborate through a single test management project.

---------------------------------------------- 
## TestMu AI Projects

The Project feature in TestMu AI helps organize and manage related test executions under a common workspace.

When multiple users, pipelines, or environments execute automated tests, associating executions with a single TestMu AI project provides the following benefits:

- [x] Consolidates all INGenious executions under a single project.
- [x] Maintains a centralized history of builds and test runs.
- [x] Enables easier tracking of execution trends across releases.
- [x] Simplifies collaboration between Test Engineers, Developers, and Product Owners.
- [x] Provides a structured view of test results, execution status, and historical reports.
- [x] Allows teams to separate test activities by application, domain, or release stream using different projects.

Using projects is highly recommended for organizations executing tests from multiple environments or CI/CD pipelines, as it keeps related executions grouped together and easier to analyze.

!!! Important 
    **Additional access to Test Manager should be requested from your account manager.**

---------------------------------------------- 
## Create a Project in Test Manager

As a prerequisite to using the Project Manager integration, you must create a project in LambdaTest and retrieve the project ID.

1. In the LambdaTest web portal, select **Test Manager** > **Projects** from the sidebar menu.
2. If you do not have an existing project, click **Create Project** and enter your desired values.
3. Open the project and retrieve the **ProjectID** from the URL.
![projectid](/img/testmuai/testmu-project-id.png "projectid")


---------------------------------------------- 
## Configuration

To ensure that all INGenious executions are reported and consolidated into the correct TestMu AI project, configure the following settings. 

![tmsettings](/img/testmuai/testmu-tm-settings.png "tmsettings"){ width="90%" }

1. Go to **Configurations** > **Settings** > **TM Settings**
2. Select **Test Manager** in the dropdown menu then tick **Update Results back to**
3. Provide the following required configurations

|Key|Value|
|-------------|---------------|
|`Username`| See [LambdaTest Configuration](/browsertesting/config/#lambdatest-configuration)|
|`AccessKey`| See [LambdaTest Configuration](/browsertesting/config/#lambdatest-configuration)|
|`ProjectId`| See [Create a Project in Test Manager](/testmuai/testmuai/#create-a-project-in-test-manager)|
|`TestManager URL`|https://test-manager-api.lambdatest.com/api/v1/|


Optional: You may click **Test Connection** to validate the inputs. The bulb should turn green once connection is successful.

![testconnection](/img/testmuai/testmu-test-connect-success.png "testconnection"){ width="70%" }

---------------------------------------------- 
## Test Execution

After configuring the integration, you can execute tests directly from INGenious and validate the published results in TestMu AI.

1. Go to **Test Execution** window
2. Select or create a test set for the test cases to be executed
3. Set the proper LambdaTest devices or browsers for each test case. For mobile devices, refer to [Mobile App Testing - Sample Emulator Configurations](/mobiletesting/emulatorsetup/#sample-emulator-configurations)
4. Start the execution.
5. Monitor the execution progress until completion.
6. Open TestMu AI and navigate to the configured project and view the test results.

![testconnection](/img/testmuai/testmu-test-execution-config.png "testconnection")

The complete execution set should be published to the configured TestMu AI project, allowing stakeholders to review execution results and historical trends from a centralized location.

Here's a sample view of a completed test displayed within the configured project.
![testconnection](/img/testmuai/testmu-sample-completed-run.png "testconnection")