---
icon: material/mouse-scroll-wheel
---

# **Scroll Actions** 

## **scrollInAndroid**

**Description**: This function will scroll to element text in Android

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`scrollInAndroid`](#)   | @value       |  | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`scrollInAndroid`](#)   | Sheet:Column |  | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`scrollInAndroid`](#)   | %dynamicVar% |  | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc ="Scroll to Element Text in Android", input = InputType.YES)
    public void scrollInAndroid() {
        try {
            mDriver.findElement(AppiumBy.androidUIAutomator("new UiScrollable(new UiSelector().scrollable(true)).scrollIntoView(new UiSelector().text(\"" + Data + "\"))"));
            Report.updateTestLog(Action, "Scrolled to '" + Data + "'", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog("Could not perfom [" + Action + "] action", "Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
----------------------


## **scrollInIOS**

**Description**: This function will scroll to element in IOS

=== "Usage"

    | ObjectName | Action            | Input        | Condition |Reference|  |
    |------------|-------------------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`scrollInIOS`](#)   | @value       |  | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`scrollInIOS`](#)   | Sheet:Column |  | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`scrollInIOS`](#)   | %dynamicVar% |  | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc ="Scroll to Element in iOS", input = InputType.YES, condition = InputType.YES)
    public void scrollInIOS() {
        try {
            HashMap<String, Object> scrollObject = new HashMap<>();
            scrollObject.put("direction", Condition.toLowerCase());
            String attribute = Data.split("=")[0];
            String value = Data.split("=")[1];
            scrollObject.put(attribute,value);
            IOSDriver driver = (IOSDriver) mDriver;
            driver.executeScript("mobile:scroll",scrollObject);
            Report.updateTestLog(Action, "Scrolled to '" + Data + "'", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog("Could not perfom [" + Action + "] action", "Error: " + e.getMessage(), Status.FAIL);
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

