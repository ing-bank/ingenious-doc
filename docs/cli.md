# **Command Line Interface**  
---------------------- 

!!! note "CLI"
    INGenious has a rich set of command line options for execution with parameters, retrieving execution details, setting variables, change settings etc.


## CLI Options (Modern)

### Project Management

Use [`ingenious project`](#) to use project management commands. You can append [`--help`](#) to the command to display possible commands.

|<div style="color:#349651;width:100px">Options</div>|<div style="color:#AB0066;width:400px">Output</div>
|-------------------------------|---------------------------
|[`list`](#)          |List all projects in a directory
|[`info`](#)          |Show project information
|[`validate`](#)          |Show a health dashboard for the project
|[`create`](#)          |Create a new project
|[`upgrade`](#)          |Interactive upgrade wizard: modernise ORs, test cases, and clean up legacy files

---------------------------

### Run

Use [`ingenious run`](#) to run from the CLI. You can append [`--help`](#) to the commands below to display usage.

|<div style="color:#349651;width:100px">Options</div>|<div style="color:#AB0066;width:400px">Output</div>
|-------------------------------|---------------------------
|[`testcase`](#)          |Run a specific test case
|[`testset`](#)          |Run a specific test set
|[`tags`](#)          |Run tests with matching tags
|[`rerun`](#)          |Rerun failed tests from last execution

The `run` command also supports **auto-detection** — you can pass a path directly and it detects whether it is a test case or test set:

```
ingenious run <Project>/<Scenario>/<TestCase>
ingenious run <Project>/<Release>/<TestSet>
```

---------------------------

### Configuration Management

Use [`ingenious config`](#) to use configuration management commands. You can append [`--help`](#) to the command to display possible commands.

|<div style="color:#349651;width:100px">Options</div>|<div style="color:#AB0066;width:400px">Output</div>
|-------------------------------|---------------------------
|[`show`](#)          |Show all configuration settings
|[`get`](#)          |Get a configuration value
|[`set`](#)          |Set a configuration value
|[`drivers`](#)          |Manage browser drivers
|[`reset`](#)          |Reset configuration to defaults
|[`prefixes`](#)          |List all recognised -setEnv / set-env override prefixes

---------------------------

### Report Management

Use [`ingenious report`](#) to use report management commands. You can append [`--help`](#) to the command to display possible commands.

|<div style="color:#349651;width:100px">Options</div>|<div style="color:#AB0066;width:400px">Output</div>
|-------------------------------|---------------------------
|[`latest`](#)          |Show latest test execution results
|[`history`](#)         |Show test execution history
|[`show`](#)          |Show details of a specific run
|[`export`](#)          |Export report in various formats
|[`compare`](#)          |Compare two test runs

---------------------------

### Server Commands

Use [`ingenious server`](#) to use server commands. You can append [`--help`](#) to the command to display possible commands.

|<div style="color:#349651;width:100px">Options</div>|<div style="color:#AB0066;width:400px">Output</div>
|-------------------------------|---------------------------
|[`mcp`](#)          |Start MCP (Model Context Protocol) server
|[`rest`](#)         |Start REST API Server
|[`status`](#)          |Check server status

---------------------------

---------------------------

### Shell Session

Use [`ingenious shell`](#) to  You can append [`--help`](#) to the command to display usage.

---------------------------
---------------------------

## CLI Options (Legacy)

|<div style="color:#349651;width:100px">Options</div>|<div style="color:#AB0066;width:400px">Output</div>
|-------------------------------|---------------------------
|[`-v`](#),[`-version`](#)              |Display current build details
|[`-run`](#)                         |Run with the given details
|[`-rerun`](#)                       |Rerun the last execution
|[`-project_location`](#) <arg>      |Project Location for Execution
|[`-scenario`](#) <arg>              |Scenario Name
|[`-testcase`](#) <arg>              |Testcase Name
|[`-browser`](#) <arg>               |Browser Name (Not applicable for Testset Execution)
|[`-release`](#) <arg>               |Release Name
|[`-testset`](#) <arg>               |Testset Name
|[`-tags`](#) <arg>                  |Tags of Test Cases to be exceuted
|[`-bDate`](#)                       |Display current build date
|[`-bTime`](#)                       |Display current build time
|[`-bVersion`](#)                    |Display current build version
|[`-dont_launch_report`](#)          |Disables launching summary report after execution
|[`-help`](#)                        |Help
|[`-hi`](#)                          |Says Hello!
|[`-t`](#)                           |Display Current Time
|[`-latest_exe`](#) <arg>            |Returns the given property value for the latest execution
|[`-latest_exe_loc`](#)              |Returns the results folder for the latest execution
|[`-latest_exe_status`](#)           |Returns the status for the latest execution
|[`-latest_exe_data_loc`](#)         |Returns the Report data location for the latest execution
|[`-latest_exe_data_raw`](#)         |Returns the Report data for the latest execution
|[`-latest_exe_log_loc`](#)          |Returns the log file location for the latest execution
|[`-latest_exe_log_raw`](#)          |Returns the log file for the latest execution
|[`-latest_exe_perf_status`](#) <arg>|Returns the page load performance results for latest execution
|[`-latest_exe_perf_report`](#) <arg>|Returns the page load performance report for latest execution
|[`-checkPagePerf`](#) <arg>         |Returns the page load performance results after Run
|[`-setVar`](#) <arg>                |Create/Set user defined variable [[`-setVar "var=value"]`](#)
|[`-setEnv`](#) <arg>                |Create/Set Env settings <override>
|[`-standalone_report`](#)           |Create Standalone Report instead of Relative one

---------------------------


### Modern Examples

:octicons-check-24: **Single Test Case Execution**

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo/NewScenario/NewTestCase --browser Chromium
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewScenario/NewTestCase --browser Chromium
    ```

The modern `run` command **auto-detects** whether the path refers to a test case or a test set. The above is equivalent to the explicit:

=== "Windows"

    ```{ .powershell .copy }
    ingenious run testcase --project "Projects\Demo" --scenario NewScenario --testcase NewTestCase --browser Chromium
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run testcase --project "Projects/Demo" --scenario NewScenario --testcase NewTestCase --browser Chromium
    ```

---------------------- 

:material-check-all: **Test Set Execution**

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewRelease\NewTestSet
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewRelease/NewTestSet
    ```

Or explicitly:

=== "Windows"

    ```{ .powershell .copy }
    ingenious run testset --project "Projects\Demo" --release NewRelease --testset NewTestSet
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run testset --project "Projects/Demo" --release NewRelease --testset NewTestSet
    ```

---------------------- 

:octicons-tag-16: **Test Set Execution with specific tags**

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewRelease\NewTestSet --tags @smoke
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewRelease/NewTestSet --tags @smoke
    ```

Or explicitly:

=== "Windows"

    ```{ .powershell .copy }
    ingenious run testset --project "Projects\Demo" --release NewRelease --testset NewTestSet --tags @smoke
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run testset --project "Projects/Demo" --release NewRelease --testset NewTestSet --tags @smoke
    ```

---------------------- 

:octicons-gear-24: **Test Set Execution with Updated Environment Settings**

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewRelease\NewTestSet --set-env "run.TestEnv=Acceptance"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewRelease/NewTestSet --set-env "run.TestEnv=Acceptance"
    ```

In the above example, the test set will be forced to be executed on `Acceptance` Environment.

---------------------- 

:octicons-check-24: **Rerun Failed Tests**

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewRelease\NewTestSet --rerun
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewRelease/NewTestSet --rerun
    ```

Re-executes only the test cases that failed in the last run of the given target.

---------------------- 

:material-check-all: **Headless Execution**

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewScenario\NewTestCase --browser Chromium --headless
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewScenario/NewTestCase --browser Chromium --headless
    ```

---------------------- 

**Parallel Test Set Execution**

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewRelease\NewTestSet --parallel 4
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewRelease/NewTestSet --parallel 4
    ```

Runs the test set across 4 parallel threads.

---------------------- 

**Project Management**

=== "Windows"

    ```{ .powershell .copy }
    ingenious project list
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command project list
    ```

List projects in a specific directory:

=== "Windows"

    ```{ .powershell .copy }
    ingenious project list "Projects"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command project list "Projects"
    ```

Show project information:

=== "Windows"

    ```{ .powershell .copy }
    ingenious project info Demo
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command project info Demo
    ```

Validate project health:

=== "Windows"

    ```{ .powershell .copy }
    ingenious project validate Demo
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command project validate Demo
    ```

Create a new project:

=== "Windows"

    ```{ .powershell .copy }
    ingenious project create NewProject --directory "Projects"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command project create NewProject --directory "Projects"
    ```

---------------------- 

**Upgrade Wizard**

=== "Windows"

    ```{ .powershell .copy }
    ingenious project upgrade Demo
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command project upgrade Demo
    ```

Automatically accept all defaults:

=== "Windows"

    ```{ .powershell .copy }
    ingenious project upgrade Demo --yes
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command project upgrade Demo --yes
    ```

Preview changes without modifying files:

=== "Windows"

    ```{ .powershell .copy }
    ingenious project upgrade Demo --dry-run
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command project upgrade Demo --dry-run
    ```

The upgrade wizard walks through:
1. **Test Data Migration** — adds the `Scope` field to test datasheets
2. **Object Repository Conversion** — converts XML ORs to YAML
3. **Test Case Migration** — converts CSV test cases to YAML
4. **Deprecated File Cleanup** — removes legacy XML stubs
5. **Reusable Relocation** — moves mislocated reusables to `ReusableComponents/`

---------------------- 

:octicons-gear-24: **Configuration Management**

Show all configuration:

=== "Windows"

    ```{ .powershell .copy }
    ingenious config show --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command config show --project "Projects/Demo"
    ```

Get a specific value:

=== "Windows"

    ```{ .powershell .copy }
    ingenious config get browser --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command config get browser --project "Projects/Demo"
    ```

Set a value:

=== "Windows"

    ```{ .powershell .copy }
    ingenious config set timeout 60 --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command config set timeout 60 --project "Projects/Demo"
    ```

List all recognised override prefixes:

=== "Windows"

    ```{ .powershell .copy }
    ingenious config prefixes
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command config prefixes
    ```

Check browser drivers:

=== "Windows"

    ```{ .powershell .copy }
    ingenious config drivers --check
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command config drivers --check
    ```

---------------------- 

**Report Management**

Show latest execution results:

=== "Windows"

    ```{ .powershell .copy }
    ingenious report latest --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command report latest --project "Projects/Demo"
    ```

Show test execution history (last 10 runs):

=== "Windows"

    ```{ .powershell .copy }
    ingenious report history --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command report history --project "Projects/Demo"
    ```

Show details of a specific run:

=== "Windows"

    ```{ .powershell .copy }
    ingenious report show Run_2024_01_15_10_30_00 --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command report show Run_2024_01_15_10_30_00 --project "Projects/Demo"
    ```

Export report to JSON:

=== "Windows"

    ```{ .powershell .copy }
    ingenious report export --project "Projects\Demo" --format json --output report.json
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command report export --project "Projects/Demo" --format json --output report.json
    ```

Compare two runs:

=== "Windows"

    ```{ .powershell .copy }
    ingenious report compare Run_2024_01_15_10_30_00 Run_2024_01_16_14_00_00 --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command report compare Run_2024_01_15_10_30_00 Run_2024_01_16_14_00_00 --project "Projects/Demo"
    ```

---------------------- 

**Server Commands**

Start the REST API server:

=== "Windows"

    ```{ .powershell .copy }
    ingenious server rest --port 8090 --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command server rest --port 8090 --project "Projects/Demo"
    ```

Start the MCP server (for AI agent integration):

=== "Windows"

    ```{ .powershell .copy }
    ingenious server mcp --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command server mcp --project "Projects/Demo"
    ```

Check server status:

=== "Windows"

    ```{ .powershell .copy }
    ingenious server status --port 8090
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command server status --port 8090
    ```

---------------------- 

**Interactive Shell**

=== "Windows"

    ```{ .powershell .copy }
    ingenious shell
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command shell
    ```

Start with a pre-set project:

=== "Windows"

    ```{ .powershell .copy }
    ingenious shell --project "Projects\Demo"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command shell --project "Projects/Demo"
    ```

Inside the shell you can use shorter commands like `run Login/Smoke`, `scenario list`, `config show`, etc.

---------------------- 

**Version Information**

=== "Windows"

    ```{ .powershell .copy }
    ingenious --version
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command --version
    ```

---------------------- 

**Action Discovery**

List all available Browser actions:

=== "Windows"

    ```{ .powershell .copy }
    ingenious action list Browser
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command action list Browser
    ```

Search for actions by keyword:

=== "Windows"

    ```{ .powershell .copy }
    ingenious action search click
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command action search click
    ```

Show detailed action information:

=== "Windows"

    ```{ .powershell .copy }
    ingenious action info Click
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command action info Click
    ```

List action categories with counts:

=== "Windows"

    ```{ .powershell .copy }
    ingenious action categories
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command action categories
    ```

---------------------- 

#### Legacy Commands

:octicons-check-24: **Single Test Case Execution**

=== "Windows"

    ```{ .powershell .copy }
    ingenious.bat -run -project_location "Projects\Demo" -scenario "NewScenario" -testcase "NewTestCase" -browser "Chrome"
    ```

=== "Mac/Linux"
    ```{ .shell .copy }
    ./ingenious.command -run -project_location "Projects\Demo" -scenario "NewScenario" -testcase "NewTestCase" -browser "Chrome"
    ```

---------------------- 

:material-check-all: **Test Set Execution**


=== "Windows"

    ```{ .powershell .copy }
    ingenious.bat -run -project_location "Projects\Demo" -release "NewRelease" -testset "NewTestSet"
    ```

=== "Mac/Linux"
    ```{ .shell .copy }
    ./ingenious.command -run -project_location "Projects\Demo" -release "NewRelease" -testset "NewTestSet"
    ```

---------------------- 

:octicons-tag-16: **Test Set Execution with specific tags**

=== "Windows"

    ```{ .powershell .copy }
    ingenious.bat -run -project_location "Projects\Demo" -release "NewRelease" -testset "NewTestSet" -tags "@smoke"
    ```

=== "Mac/Linux"
    ```{ .shell .copy }
    ./ingenious.command -run -project_location "Projects\Demo" -release "NewRelease" -testset "NewTestSet" -tags "@smoke"
    ```

---------------------- 

:octicons-gear-24: **Test Set Execution with Updated Environment Settings**

=== "Windows"

    ```{ .powershell .copy }
    ingenious.bat -run -project_location "Projects\Demo" -release "NewRelease" -testset "NewTestSet" -setEnv "run.TestEnv=Acceptance"
    ```

=== "Mac/Linux"
    ```{ .shell .copy }
    ./ingenious.command -run -project_location "Projects\Demo" -release "NewRelease" -testset "NewTestSet" -setEnv "run.TestEnv=Acceptance"
    ```
In the above example, the test set will be forced to be executed on `Acceptance` Environment

---------------------- 

### Override Settings

**`-setEnv`** is a very powerful command to override all the environment settings and userdefined variables.
This can override the values in all of these settings :

![settings](img/cli/3.png "settings")

Lets look at the `Run Settings` for a Test Set. If we enter into the project location and navigate to the following location :

`Settings\TestExecution\`<`ReleaseName`>`\`<`TestSetName`> 

We will find the `RunSettings.Properties` and the `TestMgmtSettings.Properties` files.

The `RunSettings.Properties` holds all the corresponding settings that we enter via the UI of the framework.

![runsettings](img/cli/1.png "runsettings")

Any of these properties can be overriden by **`-setEnv`**. 

For Example: `-setEnv "run.TakeFullPageScreenShot=False"`

Similarly, if we go to the **project location** and navigate to `Settings\` directory, the `userDefinedSettings.Properties` holds all the corresponding data that we enter via the UI of the framework.

![usersettings](img/cli/2.png "usersettings")

We can use by **`-setEnv`** to override these values too.

For Example: `-setEnv "user.Key1=NewValue1"`

Similarly, if we go to the **project location** and navigate to `Settings\` directory, the `KafkaSSLConfigurations.Properties` holds all the corresponding data that we enter via the UI of the framework.

![kafkasettings](img/cli/4.png "kafkasettings")

We can use by **`-setEnv`** to override these values too.

For Example: `-setEnv "kafkaSSl.Producer_Key_Password=P@ssw0rd"`

For the following settings, **`-setEnv`** can be used as follows :

|Settings|option|
|--------|-------|
|Global Settings| -setEnv "`exe`.SettingName=Value"|
Run Settings | -setEnv "`run`.SettingName=Value"|
User Defined Settings | -setEnv "`user`.SettingName=Value"|
Kafka SSL Configurations | -setEnv "`kafkaSSl`.SettingName=Value"|
Driver Settings | -setEnv "`driver`.SettingName=Value"|
Test Management Settings | -setEnv "`tm`.SettingName=Value"|
Browser Capability Settings | -setEnv "`capability`.`browserName`.SettingName=Value"|
Browser Context Settings |-setEnv "`context`.`aliasName`.SettingName=Value"|
Database Settings | -setEnv "'`db`.`aliasName`.SettingName=Value"|
API Settings | -setEnv "'`api`.`aliasName`.SettingName=Value"|

**NOTE:** These prefixes can also be showed in the console with command 'config prefixes'

Examples :

```{ .shell .copy }
-setEnv "capability.chromium.setheadless=false"` 
```
```{ .shell .copy }
-setEnv "context.test.password=Value"
```

Multiple settings can be altered via a single command as well :

```{ .shell .copy }
-setEnv "run.var=value;exe.var=value;user.var=value"
```

### Modern Override Settings

The modern CLI provides **typed override flags** as a more ergonomic alternative to `-setEnv`. These are available on all `ingenious run …` subcommands and accept `key=value` pairs for their respective bucket.

|Flag|Bucket|Example|
|--------|-------|-------|
|[`--set-env`](#) |Raw pass-through | `--set-env "run.var=value"`
|[`--driver`](#) |Driver / Launch Configurations | `--driver "RemoteURL=http://hub:4444"`
|[`--user`](#) |User Defined Settings | `--user "Key1=NewValue1"`
|[`--tm`](#) |Test Management Settings | `--tm "ProjectKey=DEMO"`
|[`--capability`](#) |Per-browser capability | `--capability "Chrome.headless=true"`
|[`--db`](#) |Database properties | `--db "mydb.ConnectionString=server=..."`
|[`--context`](#) |Browser Context | `--context "test.password=secret"`
|[`--api`](#) |API properties | `--api "myapi.BaseURL=https://api.example.com"`
|[`--kafka-ssl`](#) |Kafka SSL Config | `--kafka-ssl "Producer_Key_Password=P@ssw0rd"`
|[`--lambdatest-cap`](#) |LambdaTest Grid Capabilities | `--lambdatest-cap "build=ci-1234"`
|[`--browser-arg`](#) |Per-browser launch flag | `--browser-arg "Chrome.1=--headless=new"`
|[`--browser-set`](#) |Per-browser property | `--browser-set "Chrome.mySetting=value"`
|[`--device`](#) |Per-device override | `--device "Pixel5.RemoteURL=http://hub:4723"`
|[`--tm-module`](#) |AzureDevOps TestPlan module | `--tm-module "AzureDO.__enabled=true"`

**Examples using typed overrides:**

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewRelease\NewTestSet --capability "Chromium.headless=true" --user "TestEnv=Acceptance"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewRelease/NewTestSet --capability "Chromium.headless=true" --user "TestEnv=Acceptance"
    ```

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewScenario\NewTestCase --browser Chromium --headless --db "mydb.ConnectionString=jdbc:mysql://localhost:3306/test"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewScenario/NewTestCase --browser Chromium --headless --db "mydb.ConnectionString=jdbc:mysql://localhost:3306/test"
    ```

Multiple overrides can be combined:

=== "Windows"

    ```{ .powershell .copy }
    ingenious run Demo\NewRelease\NewTestSet --device "Pixel5.RemoteURL=http://hub:4723" --tm-module "AzureDO.__enabled=true" --lambdatest-cap "build=ci-5678"
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command run Demo/NewRelease/NewTestSet --device "Pixel5.RemoteURL=http://hub:4723" --tm-module "AzureDO.__enabled=true" --lambdatest-cap "build=ci-5678"
    ```

Find all recognised prefix names at any time with:

=== "Windows"

    ```{ .powershell .copy }
    ingenious config prefixes
    ```

=== "Mac/Linux"

    ```{ .shell .copy }
    ./ingenious.command config prefixes
    ```
