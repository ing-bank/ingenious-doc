---
icon: material/swap-horizontal
---

# Context Actions
------------------------

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

