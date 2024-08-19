![GitHub Actions](../img/cicd/githubActions.png){ .center width="100" }

---- 

# Integration of INGenious with GitHub Actions 

## **Pipeline yaml**

```{.yaml .copy}

name: Test Execution

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Set up JDK 17        # (1)!
      uses: actions/setup-java@v4 
      with:
        java-version: '17'
        distribution: 'temurin'
        cache: maven
    - name: Maven Initialize     # (2)!
      run: mvn initialize --file Engine/pom.xml
    - name: Maven Install        # (3)!
      run: mvn install --file Engine/pom.xml
    - name: Set Permissions      # (4)!
      run: chmod -R 755 ./
    - name: Run tests            # (5)!
      run: ./Run.command -run -project_location "Projects/ING-Public-Web" -release "Release1" -testset "Set1"
    - name: Upload Reports       # (6)!
      uses: actions/upload-artifact@v4.3.6
      with:
        name: Execution Reports
        path: Projects/ING-Public-Web/Results/TestExecution/Release1/Set1/Latest
```
 
 1. This is to set up the Java version. In this case this is set as 17. But you can set it to 11 or above 
 2. This is to perform `mvn initialize` which makes the ingenious specific jar files, known to the **`.m2`** of the agent
 3. This is to install maven dependencies of your project
 4. This sets the permission to the working directory. A `chmod 755` for a folder gives the owner full permissions, group members and others read and access permissions
 5. This executes the INGenious tests. You need to specify the `project_location`, the name of the `release` and `testset`. Additionally the **`-setEnv "run.AzureReport=true"`** will make sure that the Azure DevOps compatible reports (nunit xml) are generated which shows the test results, screenshots and videos as attachments.
 6. This is to upload the test results as a build artifact

----

## **Pipeline Analysis**

 * [x] Once the execution is over, the logs will appera in the pipeline console

  ![report](../img/cicd/githubactions1.png "Report")

 * [x] You can download the **Test Execution Reports** (as Build Artifacts) from the overview page

  ![report](../img/cicd/githubactions2.png "Report") 

