---
icon: material/cellphone
---

# New Mobile Actions
------------------------

This page documents mobile actions newly introduced between branch `release/4.0.0` and `feature/inlineObjectPropOverride-rebase`.

## **executeAdbShellCommand**

**Description**: This function is used to execute adb shell command

**Input Format** : @ADBShellCommand

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`executeAdbShellCommand`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`executeAdbShellCommand`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`executeAdbShellCommand`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Execute adb shell <Input> command and store output in [Condition] variable",
            input = InputType.YES,
            condition = InputType.OPTIONAL
        )
        public void executeAdbShellCommand() {
            if (!isAndroid()) return;
            try {
                String output = runShell(Data);
                if (!Condition.isEmpty()) {
                    addVar(Condition, output);
                }
                Report.updateTestLog(Action, "adb shell output: " + output, Status.DONE);
            } catch (Exception e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(Action, "adb shell failed: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **assertAdbShellOutput**

**Description**: This function is used to execute adb shell <Input> command and assert output contains [Condition] text.

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`assertAdbShellOutput`](#)  | @value       | @value      | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`assertAdbShellOutput`](#)  | Sheet:Column | Sheet:Column | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`assertAdbShellOutput`](#)  | %dynamicVar% | %dynamicVar% | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Execute adb shell <Input> command and assert output contains [Condition] text",
            input = InputType.YES,
            condition = InputType.YES
        )
        public void assertAdbShellOutput() {
            if (!isAndroid()) return;
            try {
                String output = runShell(Data);
                if (output.contains(Condition)) {
                    Report.updateTestLog(
                        Action,
                        "Output contained '" + Condition + "': " + output,
                        Status.PASS
                    );
                } else {
                    Report.updateTestLog(
                        Action,
                        "Expected output to contain '" + Condition + "' but got: " + output,
                        Status.FAIL
                    );
                }
            } catch (Exception e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(Action, "adb shell failed: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **clearAppData**

**Description**: This function is used to clear data for app with package name <Input>.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`clearAppData`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`clearAppData`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`clearAppData`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Clear data for app with package name <Input>",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void clearAppData() {
            if (!isAndroid()) return;
            try {
                String output = runShell("pm clear " + Data);
                Report.updateTestLog(Action, "pm clear " + Data + ": " + output, Status.DONE);
            } catch (Exception e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(Action, "clearAppData failed: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **forceStopApp**

**Description**: This function is used to force-stop app with package name <Input>.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`forceStopApp`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`forceStopApp`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`forceStopApp`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Force-stop app with package name <Input>",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void forceStopApp() {
            if (!isAndroid()) return;
            try {
                runShell("am force-stop " + Data);
                Report.updateTestLog(Action, "Force-stopped " + Data, Status.DONE);
            } catch (Exception e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(Action, "forceStopApp failed: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **getDeviceProperty**

**Description**: This function is used to get Android system property <Input> and store in [Condition] variable.

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`getDeviceProperty`](#)  | @value       | @value | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`getDeviceProperty`](#)  | Sheet:Column | Sheet:Column | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`getDeviceProperty`](#)  | %dynamicVar% | %dynamicVar% | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Get Android system property <Input> and store in [Condition] variable",
            input = InputType.YES,
            condition = InputType.YES
        )
        public void getDeviceProperty() {
            if (!isAndroid()) return;
            try {
                String value = runShell("getprop " + Data);
                addVar(Condition, value);
                Report.updateTestLog(Action, Data + " = " + value, Status.DONE);
            } catch (Exception e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "getDeviceProperty failed: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **pushFileToDevice**

**Description**: This function is used to push local file <Input> to device path [Condition].

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`pushFileToDevice`](#)  | @value       | @value | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`pushFileToDevice`](#)  | Sheet:Column | Sheet:Column | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`pushFileToDevice`](#)  | %dynamicVar% | %dynamicVar% | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Push local file <Input> to device path [Condition]",
            input = InputType.YES,
            condition = InputType.YES
        )
        public void pushFileToDevice() {
            if (!isAndroid()) return;
            try {
                byte[] fileBytes = Files.readAllBytes(Path.of(Data));
                ((AndroidDriver) mDriver).pushFile(Condition, fileBytes);
                Report.updateTestLog(Action, "Pushed " + Data + " to " + Condition, Status.DONE);
            } catch (IOException e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(Action, "pushFileToDevice failed: " + e.getMessage(), Status.FAIL);
            } catch (Exception e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(Action, "pushFileToDevice failed: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **pullFileFromDevice**

**Description**: This function is used to pull file from device path <Input> to local path [Condition].

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`pullFileFromDevice`](#)  | @value       | @value | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`pullFileFromDevice`](#)  | Sheet:Column | Sheet:Column | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`pullFileFromDevice`](#)  | %dynamicVar% | %dynamicVar% | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Pull file from device path <Input> to local path [Condition]",
            input = InputType.YES,
            condition = InputType.YES
        )
        public void pullFileFromDevice() {
            if (!isAndroid()) return;
            try {
                byte[] fileBytes = ((AndroidDriver) mDriver).pullFile(Data);
                Files.write(Path.of(Condition), fileBytes);
                Report.updateTestLog(Action, "Pulled " + Data + " to " + Condition, Status.DONE);
            } catch (IOException e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "pullFileFromDevice failed: " + e.getMessage(),
                    Status.FAIL
                );
            } catch (Exception e) {
                LOG.log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "pullFileFromDevice failed: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **doubleTap**

**Description**: This function is used to double tap the [<Object>].

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`doubleTap`](#)  |              |       | |

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.APP,
            desc = "Double tap the [<Object>]",
            input = InputType.NO,
            condition = InputType.NO
        )
        public void doubleTap() {
            try {
                Rectangle rectangle = Element.getRect();
                Point point = new Point(
                    rectangle.x + (rectangle.width / 2),
                    rectangle.y + (rectangle.height / 2)
                );
                PointerInput finger = new PointerInput(PointerInput.Kind.TOUCH, "finger");
                Sequence seq = new Sequence(finger, 1);
                seq.addAction(
                    finger.createPointerMove(
                        Duration.ofMillis(0),
                        PointerInput.Origin.viewport(),
                        point.x,
                        point.y
                    )
                );
                seq.addAction(finger.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
                seq.addAction(finger.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
                seq.addAction(new Pause(finger, Duration.ofMillis(100)));
                seq.addAction(finger.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
                seq.addAction(finger.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
                ((RemoteWebDriver) mDriver).perform(Arrays.asList(seq));
                Report.updateTestLog(
                    Action,
                    "Double tap performed on [" + ObjectName + "]",
                    Status.DONE
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Unable to perform double tap, Error: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **activateApp**

**Description**: This function is used to activate app by package/bundle id [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`activateApp`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`activateApp`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`activateApp`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Activate app by package/bundle id [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void activateApp() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "App id input is empty", Status.FAIL);
                    return;
                }
                String appId = Data.trim();
                if (mDriver instanceof AndroidDriver) {
                    ((AndroidDriver) mDriver).activateApp(appId);
                } else if (mDriver instanceof IOSDriver) {
                    ((IOSDriver) mDriver).activateApp(appId);
                } else {
                    Report.updateTestLog(Action, "Driver does not support activateApp", Status.FAIL);
                    return;
                }
                Report.updateTestLog(Action, "Activated app: " + appId, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Unable to activate app, Error: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **terminateApp**

**Description**: This function is used to terminate app by package/bundle id [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`terminateApp`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`terminateApp`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`terminateApp`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Terminate app by package/bundle id [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void terminateApp() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "App id input is empty", Status.FAIL);
                    return;
                }
                String appId = Data.trim();
                boolean terminated;
                if (mDriver instanceof AndroidDriver) {
                    terminated = ((AndroidDriver) mDriver).terminateApp(appId);
                } else if (mDriver instanceof IOSDriver) {
                    terminated = ((IOSDriver) mDriver).terminateApp(appId);
                } else {
                    Report.updateTestLog(Action, "Driver does not support terminateApp", Status.FAIL);
                    return;
                }
                Report.updateTestLog(
                    Action,
                    "Terminate app " + appId + " result: " + terminated,
                    terminated ? Status.DONE : Status.DEBUG
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Unable to terminate app, Error: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **runAppInBackground**

**Description**: This function is used to run app in background for [<Data>] seconds (default 5).

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`runAppInBackground`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`runAppInBackground`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`runAppInBackground`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Run app in background for [<Data>] seconds (default 5)",
            input = InputType.OPTIONAL,
            condition = InputType.NO
        )
        public void runAppInBackground() {
            try {
                int seconds = 5;
                if (Data != null && !Data.trim().isEmpty()) {
                    seconds = Integer.parseInt(Data.trim());
                }
                Duration duration = Duration.ofSeconds(seconds);
                if (mDriver instanceof AndroidDriver) {
                    ((AndroidDriver) mDriver).runAppInBackground(duration);
                } else if (mDriver instanceof IOSDriver) {
                    ((IOSDriver) mDriver).runAppInBackground(duration);
                } else {
                    Report.updateTestLog(
                        Action,
                        "Driver does not support runAppInBackground",
                        Status.FAIL
                    );
                    return;
                }
                Report.updateTestLog(
                    Action,
                    "App sent to background for " + seconds + " second(s)",
                    Status.DONE
                );
            } catch (NumberFormatException e) {
                Report.updateTestLog(Action, "Invalid seconds input: " + Data, Status.FAIL);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Unable to run app in background, Error: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **queryAppState**

**Description**: This function is used to query app state for package/bundle id [<Data>] and optionally store in [Condition].

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`queryAppState`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`queryAppState`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`queryAppState`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Query app state for package/bundle id [<Data>] and optionally store in [Condition]",
            input = InputType.YES,
            condition = InputType.OPTIONAL
        )
        public void queryAppState() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "App id input is empty", Status.FAIL);
                    return;
                }
                String appId = Data.trim();
                String state;
                if (mDriver instanceof AndroidDriver) {
                    state = ((AndroidDriver) mDriver).queryAppState(appId).name();
                } else if (mDriver instanceof IOSDriver) {
                    state = ((IOSDriver) mDriver).queryAppState(appId).name();
                } else {
                    Report.updateTestLog(Action, "Driver does not support queryAppState", Status.FAIL);
                    return;
                }
                if (Condition != null && !Condition.trim().isEmpty()) {
                    addVar(Condition, state);
                }
                Report.updateTestLog(Action, "App state for " + appId + " is " + state, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Unable to query app state, Error: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **installMobileApp**

**Description**: This function is used to install app from local path [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`installMobileApp`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`installMobileApp`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`installMobileApp`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Install app from local path [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void installMobileApp() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "App path input is empty", Status.FAIL);
                    return;
                }
                invokeDriverMethod(
                    "installApp",
                    new Class[] { String.class },
                    new Object[] { Data.trim() }
                );
                Report.updateTestLog(Action, "App installed from: " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(Action, "Failed to install app: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **removeMobileApp**

**Description**: This function is used to uninstall app by package/bundle id [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`removeMobileApp`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`removeMobileApp`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`removeMobileApp`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Uninstall app by package/bundle id [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void removeMobileApp() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "App id input is empty", Status.FAIL);
                    return;
                }
                Object removed = invokeDriverMethod(
                    "removeApp",
                    new Class[] { String.class },
                    new Object[] { Data.trim() }
                );
                Report.updateTestLog(
                    Action,
                    "Remove app result for " + Data + ": " + String.valueOf(removed),
                    Status.DONE
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(Action, "Failed to remove app: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **storeAppInstalledState**

**Description**: This function is used to store whether app [<Data>] is installed into runtime variable [<Condition>].

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeAppInstalledState`](#)  | @value       | @value | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeAppInstalledState`](#)  | Sheet:Column | Sheet:Column | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeAppInstalledState`](#)  | %dynamicVar% | %dynamicVar% | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store whether app [<Data>] is installed into runtime variable [<Condition>]",
            input = InputType.YES,
            condition = InputType.YES
        )
        public void storeAppInstalledState() {
            try {
                if (
                    Data == null ||
                    Data.trim().isEmpty() ||
                    Condition == null ||
                    Condition.trim().isEmpty()
                ) {
                    Report.updateTestLog(Action, "Input/Condition cannot be empty", Status.FAIL);
                    return;
                }
                Object installed = invokeDriverMethod(
                    "isAppInstalled",
                    new Class[] { String.class },
                    new Object[] { Data.trim() }
                );
                addVar(Condition, String.valueOf(installed));
                Report.updateTestLog(
                    Action,
                    "Stored app installed state for " + Data + " in variable " + Condition,
                    Status.DONE
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to read app installed state: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **simulateBiometricMatch**

**Description**: This function is used to simulate biometric match with [<Data>] (iOS: true/false, Android: fingerprint id).

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`simulateBiometricMatch`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`simulateBiometricMatch`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`simulateBiometricMatch`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Simulate biometric match with [<Data>] (iOS: true/false, Android: fingerprint id)",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void simulateBiometricMatch() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Biometric input is empty", Status.FAIL);
                    return;
                }
                String input = Data.trim().toLowerCase();
                if (mDriver instanceof IOSDriver) {
                    boolean match = Boolean.parseBoolean(input);
                    ((IOSDriver) mDriver).executeScript(
                            "mobile: sendBiometricMatch",
                            Map.of("type", "touchId", "match", match)
                        );
                    Report.updateTestLog(
                        Action,
                        "iOS biometric simulated with match=" + match,
                        Status.DONE
                    );
                } else if (mDriver instanceof AndroidDriver) {
                    int fingerId = Integer.parseInt(input);
                    ((AndroidDriver) mDriver).executeScript(
                            "mobile: fingerPrint",
                            Map.of("fingerprintId", fingerId)
                        );
                    Report.updateTestLog(
                        Action,
                        "Android fingerprint simulated with id=" + fingerId,
                        Status.DONE
                    );
                } else {
                    Report.updateTestLog(Action, "Unsupported driver/platform", Status.FAIL);
                }
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to simulate biometric: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **setAirplaneMode**

**Description**: This function is used to set Android airplane mode with [<Data>] as on|off.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`setAirplaneMode`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`setAirplaneMode`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`setAirplaneMode`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Set Android airplane mode with [<Data>] as on|off",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void setAirplaneMode() {
            try {
                if (!(mDriver instanceof AndroidDriver)) {
                    Report.updateTestLog(Action, "Airplane mode action is Android-only", Status.DEBUG);
                    return;
                }
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Input cannot be empty. Use on|off", Status.FAIL);
                    return;
                }
                String mode = Data.trim().toLowerCase();
                String value;
                if ("on".equals(mode)) {
                    value = "1";
                } else if ("off".equals(mode)) {
                    value = "0";
                } else {
                    Report.updateTestLog(Action, "Invalid input. Use on|off", Status.FAIL);
                    return;
                }
                ((AndroidDriver) mDriver).executeScript(
                        "mobile: shell",
                        Map.of(
                            "command",
                            "settings",
                            "args",
                            List.of("put", "global", "airplane_mode_on", value)
                        )
                    );
                ((AndroidDriver) mDriver).executeScript(
                        "mobile: shell",
                        Map.of(
                            "command",
                            "am",
                            "args",
                            List.of(
                                "broadcast",
                                "-a",
                                "android.intent.action.AIRPLANE_MODE",
                                "--ez",
                                "state",
                                "on".equals(mode) ? "true" : "false"
                            )
                        )
                    );
                Report.updateTestLog(Action, "Airplane mode set to " + mode, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to set airplane mode: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **pressMobileKeyOrButton**

**Description**: This function is used to press mobile key/button [<Data>] (Android: back/home/recent/menu/enter or keycode, iOS: home).

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`pressMobileKeyOrButton`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`pressMobileKeyOrButton`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`pressMobileKeyOrButton`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Press mobile key/button [<Data>] (Android: back/home/recent/menu/enter or keycode, iOS: home)",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void pressMobileKeyOrButton() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Key/button input is empty", Status.FAIL);
                    return;
                }
                String key = Data.trim().toLowerCase();
                if (mDriver instanceof AndroidDriver) {
                    Map<String, Object> args;
                    if (key.matches("[0-9]+")) {
                        args = Map.of("keycode", Integer.parseInt(key));
                    } else {
                        int keycode;
                        switch (key) {
                            case "home":
                                keycode = 3;
                                break;
                            case "back":
                                keycode = 4;
                                break;
                            case "enter":
                                keycode = 66;
                                break;
                            case "menu":
                                keycode = 82;
                                break;
                            case "recent":
                            case "appswitch":
                                keycode = 187;
                                break;
                            default:
                                Report.updateTestLog(
                                    Action,
                                    "Unsupported Android key: " + Data,
                                    Status.FAIL
                                );
                                return;
                        }
                        args = Map.of("keycode", keycode);
                    }
                    ((AndroidDriver) mDriver).executeScript("mobile: pressKey", args);
                    Report.updateTestLog(Action, "Pressed Android key: " + Data, Status.DONE);
                } else if (mDriver instanceof IOSDriver) {
                    if (!"home".equals(key)) {
                        Report.updateTestLog(
                            Action,
                            "Unsupported iOS button: " + Data + " (currently supports home)",
                            Status.FAIL
                        );
                        return;
                    }
                    ((IOSDriver) mDriver).executeScript("mobile: pressButton", Map.of("name", "home"));
                    Report.updateTestLog(Action, "Pressed iOS button: home", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Unsupported driver/platform", Status.FAIL);
                }
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Unable to press key/button, Error: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **switchToWebView**

**Description**: This function is used to switch to first available WebView context.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`switchToWebView`](#)  |              |       | |

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Switch to first available WebView context",
            input = InputType.NO,
            condition = InputType.NO
        )
        public void switchToWebView() {
            try {
                Set<String> contextNames = ((SupportsContextSwitching) mDriver).getContextHandles();
                String webViewContext = contextNames
                    .stream()
                    .filter(c -> c.startsWith("WEBVIEW"))
                    .findFirst()
                    .orElse(null);
                if (webViewContext != null) {
                    ((SupportsContextSwitching) mDriver).context(webViewContext);
                    Report.updateTestLog(
                        Action,
                        "Switched to WebView context: " + webViewContext,
                        Status.DONE
                    );
                } else {
                    Report.updateTestLog(
                        Action,
                        "No WebView context found. Available: " + contextNames,
                        Status.FAIL
                    );
                }
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to switch to WebView: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **switchToNativeApp**

**Description**: This function is used to switch to Native App context.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`switchToNativeApp`](#)  |              |       | |

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Switch to Native App context",
            input = InputType.NO,
            condition = InputType.NO
        )
        public void switchToNativeApp() {
            try {
                SupportsContextSwitching contextDriver = (SupportsContextSwitching) mDriver;
                String startContext = contextDriver.getContext();
                Set<String> contextNames = contextDriver.getContextHandles();
    
                if (startContext != null && startContext.startsWith("WEBVIEW")) {
                    try {
                        Set<String> windowHandles = mDriver.getWindowHandles();
                        if (windowHandles.size() > 1) {
                            String currentWindowHandle = mDriver.getWindowHandle();
                            mDriver.close();
                            Set<String> remainingHandles = mDriver.getWindowHandles();
                            if (!remainingHandles.isEmpty()) {
                                mDriver.switchTo().window(remainingHandles.iterator().next());
                            }
                            Report.updateTestLog(
                                Action,
                                "Closed WebView window " +
                                currentWindowHandle +
                                " before switching to native",
                                Status.DEBUG
                            );
                        }
                    } catch (Exception windowEx) {
                        Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, windowEx);
                        Report.updateTestLog(
                            Action,
                            "Could not close/switch WebView window before native switch: " +
                            windowEx.getMessage(),
                            Status.DEBUG
                        );
                    }
                }
    
                contextDriver.context("NATIVE_APP");
                String currentContext = contextDriver.getContext();
                if ("NATIVE_APP".equals(currentContext)) {
                    Element = null;
                    Report.updateTestLog(Action, "Switched to NATIVE_APP context", Status.DONE);
                    return;
                }
    
                mDriver.navigate().back();
                currentContext = contextDriver.getContext();
                if ("NATIVE_APP".equals(currentContext)) {
                    Element = null;
                    Report.updateTestLog(
                        Action,
                        "Context switched to NATIVE_APP after back navigation",
                        Status.DONE
                    );
                } else {
                    Report.updateTestLog(
                        Action,
                        "Switch to NATIVE_APP failed even after back. Current context: " +
                        currentContext +
                        ", Start context: " +
                        startContext +
                        ", Available contexts: " +
                        contextNames,
                        Status.FAIL
                    );
                }
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to switch to NATIVE_APP: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **switchContextByIndex**

**Description**: This function is used to switch to context by index [<Data>] (0-based).

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`switchContextByIndex`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`switchContextByIndex`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`switchContextByIndex`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Switch to context by index [<Data>] (0-based)",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void switchContextByIndex() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Context index input is empty", Status.FAIL);
                    return;
                }
                List<String> contexts = new ArrayList<>(
                    ((SupportsContextSwitching) mDriver).getContextHandles()
                );
                int index = Integer.parseInt(Data.trim());
                if (index < 0 || index >= contexts.size()) {
                    Report.updateTestLog(
                        Action,
                        "Context index " +
                        index +
                        " is out of range. Available contexts (" +
                        contexts.size() +
                        "): " +
                        contexts,
                        Status.FAIL
                    );
                    return;
                }
                String target = contexts.get(index);
                ((SupportsContextSwitching) mDriver).context(target);
                Report.updateTestLog(
                    Action,
                    "Switched to context[" + index + "]: " + target,
                    Status.DONE
                );
            } catch (NumberFormatException e) {
                Report.updateTestLog(
                    Action,
                    "Invalid index '" + Data + "': must be a number",
                    Status.FAIL
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to switch context by index: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **listAvailableContexts**

**Description**: This function is used to list all available contexts (logged to report).

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`listAvailableContexts`](#)  |              |       | |

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "List all available contexts (logged to report)",
            input = InputType.NO,
            condition = InputType.NO
        )
        public void listAvailableContexts() {
            try {
                Set<String> contextNames = ((SupportsContextSwitching) mDriver).getContextHandles();
                String current = ((SupportsContextSwitching) mDriver).getContext();
                StringBuilder sb = new StringBuilder("Available contexts: ");
                int i = 0;
                for (String ctx : contextNames) {
                    sb.append("[").append(i++).append("] ").append(ctx);
                    if (ctx.equals(current)) sb.append(" (current)");
                    sb.append("  ");
                }
                Report.updateTestLog(Action, sb.toString().trim(), Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(Action, "Failed to list contexts: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **storeAvailableContexts**

**Description**: This function is used to store all available contexts into runtime variable [<Data>] (comma-separated).

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeAvailableContexts`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeAvailableContexts`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeAvailableContexts`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store all available contexts into runtime variable [<Data>] (comma-separated)",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void storeAvailableContexts() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Variable name input is empty", Status.FAIL);
                    return;
                }
                Set<String> contextNames = ((SupportsContextSwitching) mDriver).getContextHandles();
                String value = String.join(",", contextNames);
                addVar(Data, value);
                Report.updateTestLog(Action, "Stored contexts in variable " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to store contexts: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **scrollToElement**

**Description**: This function is used to scroll to element using [<Data>] as strategy=value and optional [Condition] direction:attempts.

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`scrollToElement`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`scrollToElement`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`scrollToElement`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Scroll to element using [<Data>] as strategy=value and optional [Condition] direction:attempts",
            input = InputType.YES,
            condition = InputType.OPTIONAL
        )
        public void scrollToElement() {
            try {
                if (Data == null || !Data.contains("=")) {
                    Report.updateTestLog(
                        Action,
                        "Invalid input format. Use strategy=value, for example id=my.element",
                        Status.FAIL
                    );
                    return;
                }
                String[] parts = Data.split("=", 2);
                String strategy = parts[0].trim().toLowerCase();
                String selector = parts[1].trim();
                String direction = "down";
                int attempts = 10;
                if (Condition != null && !Condition.trim().isEmpty()) {
                    String[] opts = Condition.split(":", 2);
                    direction = opts[0].trim().toLowerCase();
                    if (opts.length > 1 && opts[1].trim().matches("[0-9]+")) {
                        attempts = Integer.parseInt(opts[1].trim());
                    }
                }
                if (!direction.matches("up|down|left|right")) {
                    Report.updateTestLog(
                        Action,
                        "Invalid direction in Condition: " + direction + ". Use up|down|left|right",
                        Status.FAIL
                    );
                    return;
                }
    
                WebElement target = null;
                for (int i = 0; i <= attempts; i++) {
                    try {
                        target = findElementByStrategy(strategy, selector);
                        if (target != null && target.isDisplayed()) {
                            break;
                        }
                    } catch (Exception ignored) {}
    
                    if (i == attempts) break;
    
                    if (mDriver instanceof AndroidDriver) {
                        boolean vertical = direction.equals("up") || direction.equals("down");
                        boolean forward = direction.equals("down") || direction.equals("right");
                        String scrollable =
                            "new UiScrollable(new UiSelector().scrollable(true))" +
                            (vertical ? ".setAsVerticalList()" : ".setAsHorizontalList()");
                        String uia = scrollable + (forward ? ".scrollForward()" : ".scrollBackward()");
                        mDriver.findElement(AppiumBy.androidUIAutomator(uia));
                    } else if (mDriver instanceof IOSDriver) {
                        ((IOSDriver) mDriver).executeScript(
                                "mobile:scroll",
                                Map.of("direction", direction)
                            );
                    } else {
                        Report.updateTestLog(Action, "Unsupported driver/platform", Status.FAIL);
                        return;
                    }
                }
    
                if (target != null && target.isDisplayed()) {
                    Report.updateTestLog(
                        Action,
                        "Element found using " + strategy + "=" + selector,
                        Status.DONE
                    );
                } else {
                    Report.updateTestLog(
                        Action,
                        "Element not found after " + attempts + " scroll attempts",
                        Status.FAIL
                    );
                }
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(Action, "scrollToElement failed: " + e.getMessage(), Status.FAIL);
            }
        }
    ```
----------------------
## **storeCurrentContext**

**Description**: This function is used to store current context name into runtime variable [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeCurrentContext`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeCurrentContext`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeCurrentContext`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store current context name into runtime variable [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void storeCurrentContext() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Variable name input is empty", Status.FAIL);
                    return;
                }
                String current = ((SupportsContextSwitching) mDriver).getContext();
                addVar(Data, current);
                Report.updateTestLog(Action, "Stored current context in variable " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to store current context: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **updateRuntimePermission**

**Description**: This function is used to update Android runtime permission using [<Data>] format package:permission:grant|revoke.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`updateRuntimePermission`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`updateRuntimePermission`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`updateRuntimePermission`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Update Android runtime permission using [<Data>] format package:permission:grant|revoke",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void updateRuntimePermission() {
            try {
                if (!(mDriver instanceof AndroidDriver)) {
                    Report.updateTestLog(
                        Action,
                        "Runtime permission update is Android-only",
                        Status.DEBUG
                    );
                    return;
                }
                if (Data == null || !Data.contains(":")) {
                    Report.updateTestLog(
                        Action,
                        "Invalid input. Expected package:permission:grant|revoke",
                        Status.FAIL
                    );
                    return;
                }
                String[] parts = Data.split(":", 3);
                if (parts.length < 3) {
                    Report.updateTestLog(
                        Action,
                        "Invalid input. Expected package:permission:grant|revoke",
                        Status.FAIL
                    );
                    return;
                }
                String appId = parts[0].trim();
                String permission = parts[1].trim();
                String operation = parts[2].trim().toLowerCase();
                if (!operation.matches("grant|revoke")) {
                    Report.updateTestLog(Action, "Operation must be grant or revoke", Status.FAIL);
                    return;
                }
                ((AndroidDriver) mDriver).executeScript(
                        "mobile: shell",
                        Map.of("command", "pm", "args", List.of(operation, appId, permission))
                    );
                Report.updateTestLog(
                    Action,
                    "Permission update executed: " + operation + " " + permission + " for " + appId,
                    Status.DONE
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to update runtime permission: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **setClipboardText**

**Description**: This function is used to set clipboard text to [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`setClipboardText`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`setClipboardText`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`setClipboardText`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Set clipboard text to [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void setClipboardText() {
            try {
                if (Data == null) {
                    Report.updateTestLog(Action, "Clipboard text input is null", Status.FAIL);
                    return;
                }
                invokeDriverMethod(
                    "setClipboardText",
                    new Class[] { String.class },
                    new Object[] { Data }
                );
                Report.updateTestLog(Action, "Clipboard text updated", Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to set clipboard text: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **storeClipboardText**

**Description**: This function is used to store clipboard text into runtime variable [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeClipboardText`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeClipboardText`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeClipboardText`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store clipboard text into runtime variable [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void storeClipboardText() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Variable name input is empty", Status.FAIL);
                    return;
                }
                Object value = invokeDriverMethod("getClipboardText", new Class[] {}, new Object[] {});
                addVar(Data, value == null ? "" : value.toString());
                Report.updateTestLog(Action, "Clipboard text stored in variable " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to read clipboard text: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **startScreenRecording**

**Description**: This function is used to start screen recording.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`startScreenRecording`](#)  |              |       | |

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Start screen recording",
            input = InputType.NO,
            condition = InputType.NO
        )
        public void startScreenRecording() {
            try {
                invokeDriverMethod("startRecordingScreen", new Class[] {}, new Object[] {});
                Report.updateTestLog(Action, "Screen recording started", Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to start screen recording: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **stopScreenRecording**

**Description**: This function is used to stop screen recording and save to [<Data>] path (mp4).

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`stopScreenRecording`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`stopScreenRecording`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`stopScreenRecording`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Stop screen recording and save to [<Data>] path (mp4)",
            input = InputType.YES,
            condition = InputType.OPTIONAL
        )
        public void stopScreenRecording() {
            try {
                Object result = invokeDriverMethod(
                    "stopRecordingScreen",
                    new Class[] {},
                    new Object[] {}
                );
                String base64 = result == null ? "" : result.toString();
                if (Data == null || Data.trim().isEmpty()) {
                    if (Condition != null && !Condition.trim().isEmpty()) {
                        addVar(Condition, base64);
                        Report.updateTestLog(
                            Action,
                            "Screen recording stopped and stored in variable " + Condition,
                            Status.DONE
                        );
                    } else {
                        Report.updateTestLog(
                            Action,
                            "Screen recording stopped. No file path provided; output discarded",
                            Status.DEBUG
                        );
                    }
                    return;
                }
                byte[] bytes = Base64.getDecoder().decode(base64);
                Path target = Path.of(Data.trim());
                Files.createDirectories(target.getParent() == null ? Path.of(".") : target.getParent());
                Files.write(target, bytes);
                Report.updateTestLog(Action, "Screen recording saved to " + target, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to stop/save screen recording: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **setDeviceLocation**

**Description**: This function is used to set device location using [<Data>] as latitude,longitude[,altitude].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`setDeviceLocation`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`setDeviceLocation`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`setDeviceLocation`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Set device location using [<Data>] as latitude,longitude[,altitude]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void setDeviceLocation() {
            try {
                if (Data == null || !Data.contains(",")) {
                    Report.updateTestLog(
                        Action,
                        "Invalid input. Expected latitude,longitude[,altitude]",
                        Status.FAIL
                    );
                    return;
                }
                String[] p = Data.split(",");
                double latitude = Double.parseDouble(p[0].trim());
                double longitude = Double.parseDouble(p[1].trim());
                double altitude = p.length > 2 ? Double.parseDouble(p[2].trim()) : 0.0;
                Map<String, Double> args = Map.of(
                    "latitude",
                    latitude,
                    "longitude",
                    longitude,
                    "altitude",
                    altitude
                );
                if (mDriver instanceof AndroidDriver) {
                    ((AndroidDriver) mDriver).executeScript("mobile: setLocation", args);
                } else if (mDriver instanceof IOSDriver) {
                    ((IOSDriver) mDriver).executeScript("mobile: setLocation", args);
                } else {
                    Report.updateTestLog(Action, "Unsupported driver/platform", Status.FAIL);
                    return;
                }
                Report.updateTestLog(
                    Action,
                    "Location set to lat=" + latitude + ", lon=" + longitude + ", alt=" + altitude,
                    Status.DONE
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to set device location: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **storeDeviceLocation**

**Description**: This function is used to store device location into runtime variable [<Data>].

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`storeDeviceLocation`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`storeDeviceLocation`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`storeDeviceLocation`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Store device location into runtime variable [<Data>]",
            input = InputType.YES,
            condition = InputType.NO
        )
        public void storeDeviceLocation() {
            try {
                if (Data == null || Data.trim().isEmpty()) {
                    Report.updateTestLog(Action, "Variable name input is empty", Status.FAIL);
                    return;
                }
                Object location = invokeDriverMethod("getLocation", new Class[] {}, new Object[] {});
                addVar(Data, location == null ? "" : location.toString());
                Report.updateTestLog(Action, "Device location stored in variable " + Data, Status.DONE);
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to get device location: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **dragElementToObject**

**Description**: This function is used to drag [<Object>] to target object [<Condition>].

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`dragElementToObject`](#)  |              | @value      | |

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.APP,
            desc = "Drag [<Object>] to target object [<Condition>]",
            input = InputType.NO,
            condition = InputType.YES
        )
        public void dragElementToObject() {
            try {
                if (Condition == null || Condition.trim().isEmpty()) {
                    Report.updateTestLog(
                        Action,
                        "Target object name in Condition is empty",
                        Status.FAIL
                    );
                    return;
                }
                WebElement target = mObject.findElement(Condition, Reference);
                if (Element == null || target == null) {
                    Report.updateTestLog(Action, "Source/target element not found", Status.FAIL);
                    return;
                }
                Rectangle src = Element.getRect();
                Rectangle dst = target.getRect();
                int startX = src.x + (src.width / 2);
                int startY = src.y + (src.height / 2);
                int endX = dst.x + (dst.width / 2);
                int endY = dst.y + (dst.height / 2);
                performTouchDrag(startX, startY, endX, endY, 600);
                Report.updateTestLog(
                    Action,
                    "Dragged [" + ObjectName + "] to [" + Condition + "]",
                    Status.DONE
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to drag to target object: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **dragByCoordinates**

**Description**: This function is used to drag using coordinates from [<Data>] to [<Condition>] where each is x,y.

**Input Format** : @Expected Text

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`dragByCoordinates`](#)  | @value       | @value | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`dragByCoordinates`](#)  | Sheet:Column | Sheet:Column | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`dragByCoordinates`](#)  | %dynamicVar% | %dynamicVar% | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Drag using coordinates from [<Data>] to [<Condition>] where each is x,y",
            input = InputType.YES,
            condition = InputType.YES
        )
        public void dragByCoordinates() {
            try {
                if (Data == null || Condition == null) {
                    Report.updateTestLog(Action, "Input/Condition cannot be empty", Status.FAIL);
                    return;
                }
                int[] from = parseCoordinates(Data);
                int[] to = parseCoordinates(Condition);
                performTouchDrag(from[0], from[1], to[0], to[1], 600);
                Report.updateTestLog(
                    Action,
                    "Dragged from (" + from[0] + "," + from[1] + ") to (" + to[0] + "," + to[1] + ")",
                    Status.DONE
                );
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Failed to drag by coordinates: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **waitForWebViewAndSwitch**

**Description**: This function is used to wait up to [<Condition>] seconds for a WebView to appear then switch to it.

**Condition Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`waitForWebViewAndSwitch`](#)  |              | @value      | |

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Wait up to [<Condition>] seconds for a WebView to appear then switch to it",
            input = InputType.NO,
            condition = InputType.OPTIONAL
        )
        public void waitForWebViewAndSwitch() {
            try {
                int timeoutSecs = 30;
                if (
                    Condition != null &&
                    !Condition.trim().isEmpty() &&
                    Condition.trim().matches("[0-9]+")
                ) {
                    timeoutSecs = Integer.parseInt(Condition.trim());
                }
                long deadline = System.currentTimeMillis() + timeoutSecs * 1000L;
                String webViewContext = null;
                while (System.currentTimeMillis() < deadline) {
                    Set<String> contextNames = ((SupportsContextSwitching) mDriver).getContextHandles();
                    webViewContext =
                        contextNames
                            .stream()
                            .filter(c -> c.startsWith("WEBVIEW"))
                            .findFirst()
                            .orElse(null);
                    if (webViewContext != null) break;
                    Thread.sleep(1000);
                }
                if (webViewContext != null) {
                    ((SupportsContextSwitching) mDriver).context(webViewContext);
                    Report.updateTestLog(
                        Action,
                        "Switched to WebView context: " + webViewContext,
                        Status.DONE
                    );
                } else {
                    Report.updateTestLog(
                        Action,
                        "WebView context did not appear within " + timeoutSecs + " seconds",
                        Status.FAIL
                    );
                }
            } catch (Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog(
                    Action,
                    "Error waiting for WebView: " + e.getMessage(),
                    Status.FAIL
                );
            }
        }
    ```
----------------------
## **launchAndSwitchToDevice**

**Description**: This function is used to launch a new device session and switch to it.

**Condition Format** : #contextAlias

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`launchAndSwitchToDevice`](#)  |              | #contextAlias | |<span style="color:#9C27B0">:arrow_left:   *Device Alias with # prefix*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Launch a new device session and switch to it",
            input = InputType.NO,
            condition = InputType.YES
        )
        public void launchAndSwitchToDevice() {
            try {
                if (!Condition.startsWith("#")) {
                    Report.updateTestLog(
                        Action,
                        "Device alias must be prefixed with '#' (e.g. #Pixel9Pro)",
                        Status.FAIL
                    );
                    return;
                }
                String alias = Condition.substring(1);
    
                // Primary driver is registered in Task.launchWebDriver; fallback check for non-standard setups
                if (!Command.deviceSessions.containsKey("default") && mDriver != null) {
                    Command.deviceSessions.put("default", mDriver);
                }
    
                RunContext ctx = new RunContext();
                ctx.BrowserName = alias;
                ctx.PlatformValue = System.getProperty("os.name");
                ctx.BrowserVersion = "default";
                ctx.Scenario = "DeviceSession";
                ctx.TestCase = alias;
                ctx.Iteration = "Single";
    
                WebDriverCreation newDriverCreation = new WebDriverCreation();
                newDriverCreation.launchDriver(ctx);
                WebDriver newDriver = newDriverCreation.driver;
    
                Command.deviceSessions.put(alias, newDriver);
                switchActiveWebDriver(newDriver);
    
                Report.updateTestLog(
                    Action,
                    "Successfully launched and switched to device session [" + alias + "]",
                    Status.DONE
                );
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong: " + e.getMessage(), Status.DEBUG);
                throw new com.ing.ingenious.api.exception.ActionException(e);
            }
        }
    ```
----------------------
## **switchToDevice**

**Description**: This function is used to switch to an already-launched device session.

**Condition Format** : #contextAlias

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`switchToDevice`](#)  |              | #contextAlias | |<span style="color:#9C27B0">:arrow_left:   *Device Alias with # prefix*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Switch to an already-launched device session",
            input = InputType.NO,
            condition = InputType.YES
        )
        public void switchToDevice() {
            try {
                if (!Condition.startsWith("#")) {
                    Report.updateTestLog(
                        Action,
                        "Device alias must be prefixed with '#' (e.g. #Pixel9Pro)",
                        Status.FAIL
                    );
                    return;
                }
                String alias = Condition.substring(1);
                WebDriver target = Command.deviceSessions.get(alias);
                if (target == null) {
                    Report.updateTestLog(
                        Action,
                        "No device session found for alias [" +
                        alias +
                        "]. " +
                        "Use launchAndSwitchToDevice first.",
                        Status.FAIL
                    );
                    return;
                }
                switchActiveWebDriver(target);
                Report.updateTestLog(
                    Action,
                    "Successfully switched to device session [" + alias + "]",
                    Status.DONE
                );
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong: " + e.getMessage(), Status.DEBUG);
                throw new com.ing.ingenious.api.exception.ActionException(e);
            }
        }
    ```
----------------------
## **closeDeviceSession**

**Description**: This function is used to close a device session by alias.

**Input Format** : #contextAlias

**Condition Format** : @Expected Text (optional)

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`closeDeviceSession`](#)  | #contextAlias |       | |<span style="color:#9C27B0">:arrow_left:   *Device Alias with # prefix*</span>

=== "Corresponding Code"

    ```java
    @Action(
            object = ObjectType.MOBILE,
            desc = "Close a device session by alias",
            input = InputType.YES,
            condition = InputType.OPTIONAL
        )
        public void closeDeviceSession() {
            try {
                if (!Data.startsWith("#")) {
                    Report.updateTestLog(
                        Action,
                        "Device alias must be prefixed with '#' (e.g. #Pixel9Pro)",
                        Status.FAIL
                    );
                    return;
                }
                String alias = Data.substring(1);
                WebDriver target = Command.deviceSessions.remove(alias);
                if (target != null) {
                    try {
                        target.quit();
                    } catch (Exception ignore) {}
                }
                // Optionally switch active driver to another session
                if (Condition != null && !Condition.isEmpty() && Condition.startsWith("#")) {
                    String switchAlias = Condition.substring(1);
                    WebDriver switchTarget = Command.deviceSessions.get(switchAlias);
                    if (switchTarget != null) {
                        switchActiveWebDriver(switchTarget);
                        Report.updateTestLog(
                            Action,
                            "Closed device session [" +
                            alias +
                            "] and switched to [" +
                            switchAlias +
                            "]",
                            Status.DONE
                        );
                        return;
                    }
                }
                Report.updateTestLog(
                    Action,
                    "Successfully closed device session [" + alias + "]",
                    Status.DONE
                );
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong: " + e.getMessage(), Status.DEBUG);
                throw new com.ing.ingenious.api.exception.ActionException(e);
            }
        }
    ```
----------------------
