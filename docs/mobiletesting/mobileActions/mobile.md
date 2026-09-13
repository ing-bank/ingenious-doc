---
icon: material/cellphone
---

# Mobile Actions
------------------------

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

## **dragToAndDropElement**

**Description**: This function is used to perform drag and drop operation on an element.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`dragToAndDropElement`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`dragToAndDropElement`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`dragToAndDropElement`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "drag and drop operation of ", input = InputType.YES)
	public void dragToAndDropElement() {
		try {
			String Page = Data.split(":", 2)[0];
			String Object = Data.split(":", 2)[1];
			if (elementPresent()) {
				WebElement DropElement = mObject.findElement(Object, Page);
				if (DropElement != null) {
					new Actions(mDriver).dragAndDrop(Element, DropElement).build().perform();
					Report.updateTestLog(Action,
							"'" + ObjectName + "' has been dragged and dropped to '" + Object + "'", Status.PASS);
				} else {
					throw new ElementException(ElementException.ExceptionType.Element_Not_Found, Object);
				}
			} else {
				throw new ElementException(ElementException.ExceptionType.Element_Not_Found, ObjectName);
			}
		} catch (Exception e) {
			Report.updateTestLog(Action, e.getMessage(), Status.FAIL);
			Logger.getLogger(CommonMethods.class.getName()).log(Level.SEVERE, e.getMessage(), e);
		}
	}
    ```
----------------------

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

## **getDeviceTime**

**Description**: This function is used to get device time in variable.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`getDeviceTime`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Get device time in variable", input = InputType.NO, condition = InputType.YES)
    public void getDeviceTime() {
        try {
            String deviceTime = "";
            if (mDriver instanceof AndroidDriver) {
                deviceTime = ((AndroidDriver) mDriver).getDeviceTime();
                addVar(Condition, deviceTime);
            } else if (mDriver instanceof IOSDriver) {
                deviceTime = ((IOSDriver) mDriver).getDeviceTime();
                addVar(Condition, deviceTime);
            }
            Report.updateTestLog(Action, "Device time is " + deviceTime, Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to get device time, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
----------------------

## **goToHomescreen**

**Description**: This function navigates the user to the homescreen.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`goToHomescreen`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Go to homescreen", input = InputType.NO, condition = InputType.NO)
    public void goToHomescreen() {
        try {
            if (mDriver instanceof AndroidDriver) {
                ((AndroidDriver) mDriver).executeScript("mobile: pressKey", Map.of("keycode", 3));
            } else if (mDriver instanceof IOSDriver) {
                ((IOSDriver) mDriver).executeScript("mobile: pressButton", Map.of("name", "home"));
            }
            Report.updateTestLog(Action, "Performed go to Homescreen operation", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to perform homescreen operation, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
----------------------

## **hideKeyboard**

**Description**: This function is used to hide the keyboard.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`hideKeyboard`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Hide Keyboard", input = InputType.NO, condition = InputType.NO)
    public void hideKeyboard() {
        try {
            if (((AndroidDriver) mDriver).isKeyboardShown()) {
                if (mDriver instanceof AndroidDriver) {
                    ((AndroidDriver) mDriver).hideKeyboard();
                } else if (mDriver instanceof IOSDriver) {
                    ((IOSDriver) mDriver).hideKeyboard();
                }
                Report.updateTestLog(Action, "Keyboard hidden successfully ", Status.DONE);
            } else {
                Report.updateTestLog(Action, "Keyboard is hidden already ", Status.DEBUG);
            }
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to hide keyboard, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
---------------------------------

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

## **lockMobileDevice**

**Description**: This function is used to lock mobile device.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`lockMobileDevice`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Lock Mobile Device", input = InputType.NO, condition = InputType.NO)
    public void lockMobileDevice() {
        try {
            if (mDriver instanceof AndroidDriver) {
                boolean lockAndroid = ((AndroidDriver) mDriver).isDeviceLocked();
                if (!lockAndroid) {
                    ((AndroidDriver) mDriver).lockDevice();
                    Report.updateTestLog(Action, "Device is locked successfully ", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Device is locked already ", Status.DONE);
                }
            } else if (mDriver instanceof IOSDriver) {
                boolean lockIOS = ((AndroidDriver) mDriver).isDeviceLocked();
                if (!lockIOS) {
                    ((AndroidDriver) mDriver).lockDevice();
                    Report.updateTestLog(Action, "Device is locked successfully ", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Device is locked already ", Status.DONE);
                }
            }
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to Lock device, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
----------------------

## **longPress**

**Description**: This function is used to do long press.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`longPress`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`longPress`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`longPress`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Long press the [<Object>]", input = InputType.YES, condition = InputType.NO)
    public void longPress() {
        try {
            int holdDuration = Integer.parseInt(Data);
            Rectangle rectangle = Element.getRect();
            Point point = new Point(rectangle.x + (rectangle.width / 2), rectangle.y + (rectangle.height / 2));
            PointerInput finger = new PointerInput(PointerInput.Kind.TOUCH, "finger");
            Sequence seq = new Sequence(finger, 1);
            seq.addAction(finger.createPointerMove(Duration.ofMillis(0), PointerInput.Origin.viewport(), point.x, point.y));
            seq.addAction(finger.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
            seq.addAction(finger.createPointerMove(Duration.ofMillis(50), PointerInput.Origin.viewport(), point.x, point.y));
            seq.addAction(new Pause(finger, Duration.ofMillis(holdDuration)));
            seq.addAction(finger.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
            ((RemoteWebDriver) mDriver).perform(Arrays.asList(seq));
            Report.updateTestLog(Action, "Long press on " + "[" + ObjectName + "]", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to perform Long Press action, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
----------------------

## **openNotifications**

**Description**: This function is used to open notifications.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`openNotifications`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Open Notifications", input = InputType.NO, condition = InputType.NO)
    public void openNotifications() {
        try {
            if (mDriver instanceof AndroidDriver) {
                ((AndroidDriver) mDriver).openNotifications();
            } else if (mDriver instanceof IOSDriver) {

            }
            Report.updateTestLog(Action, "Notification opened ", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to open Notifications, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```

---------------------------------

## **pinchAndZoomElement**

**Description**: This function is used to pinch and zoom element.

**Input Format** : @Expected data in integer

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`pinchAndZoomElement`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`pinchAndZoomElement`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`pinchAndZoomElement`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Pinch and Zoom", input = InputType.YES, condition = InputType.NO)
    public void pinchAndZoomElement() throws InterruptedException {
        try {
            Dimension size = mDriver.manage().window().getSize();
            Point SreenSource = new Point(size.getWidth(), size.getHeight());
            Rectangle rectangle = Element.getRect();
            Point elementCentre = new Point(rectangle.x + (rectangle.width / 2), rectangle.y + (rectangle.height / 2));
            int rightSideWidth = SreenSource.x - elementCentre.x;
            int leftSideWidth = elementCentre.x;
            int longestDigonal = 0;
            int angle = 0;
            float percentageZoom = Float.parseFloat(Data) / 100;
            int xExtension = 0;
            int yExtension = 0;
            int startXFingure1 = elementCentre.x;
            int startXFingure2 = elementCentre.x;
            int startYFingure1 = elementCentre.y;
            int startYFingure2 = elementCentre.y;
            int endXFingure1 = 0;
            int endYFingure1 = 0;
            int endYFingure2 = 0;
            int endXFingure2 = 0;
            if (rightSideWidth > leftSideWidth) {
                longestDigonal = (int) Math.sqrt((Math.pow(rightSideWidth, 2) + (Math.pow(elementCentre.y, 2))));
                angle = (int) Math.toDegrees(Math.atan(elementCentre.y / rightSideWidth));
                xExtension = (int) (Math.cos(angle) * longestDigonal * percentageZoom);
                yExtension = (int) (Math.sin(angle) * longestDigonal * percentageZoom);
                endXFingure1 = (int) (elementCentre.x + xExtension);
                endXFingure2 = (int) (elementCentre.x - xExtension);
            } else {
                longestDigonal = (int) Math.sqrt((Math.pow(leftSideWidth, 2) + (Math.pow(elementCentre.y, 2))));
                angle = (int) Math.toDegrees(Math.atan(elementCentre.y / leftSideWidth));
                xExtension = (int) (Math.cos(angle) * longestDigonal * percentageZoom);
                yExtension = (int) (Math.sin(angle) * longestDigonal * percentageZoom);
                endXFingure1 = (int) (elementCentre.x - xExtension);
                endXFingure2 = (int) (elementCentre.x + xExtension);
            }
            endYFingure1 = (int) (elementCentre.y - yExtension);
            endYFingure2 = (int) (elementCentre.y + yExtension);
            PointerInput finger1 = new PointerInput(PointerInput.Kind.TOUCH, "finger1");
            PointerInput finger2 = new PointerInput(PointerInput.Kind.TOUCH, "finger2");
            Sequence pinchAndZoom1 = new Sequence(finger1, 1);
            pinchAndZoom1.addAction(finger1.createPointerMove(Duration.ZERO, PointerInput.Origin.viewport(), startXFingure1, startYFingure1));
            pinchAndZoom1.addAction(finger1.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
            pinchAndZoom1.addAction(new Pause(finger1, Duration.ofMillis(200)));
            pinchAndZoom1.addAction(finger1.createPointerMove(Duration.ofMillis(200), PointerInput.Origin.viewport(), endXFingure1, endYFingure1));
            pinchAndZoom1.addAction(finger1.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
            Sequence pinchAndZoom2 = new Sequence(finger2, 1);
            pinchAndZoom2.addAction(finger2.createPointerMove(Duration.ZERO,
                    PointerInput.Origin.viewport(), startXFingure2, startYFingure2));
            pinchAndZoom2.addAction(finger2.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
            pinchAndZoom2.addAction(new Pause(finger2, Duration.ofMillis(200)));
            pinchAndZoom2.addAction(finger2.createPointerMove(Duration.ofMillis(200),
                    PointerInput.Origin.viewport(), endXFingure2, endYFingure2));
            pinchAndZoom2.addAction(finger2.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));

            ((RemoteWebDriver) mDriver).perform(Arrays.asList(pinchAndZoom1, pinchAndZoom2));

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    ```
---------------------------------

## **pinchAndZoomScreen**

**Description**: This function is used to pinch and zoom screen.

**Input Format** : @Expected data in integer

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`pinchAndZoomScreen`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`pinchAndZoomScreen`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`pinchAndZoomScreen`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Pinch and Zoom", input = InputType.YES, condition = InputType.NO)
    public void pinchAndZoomScreen() throws InterruptedException {
        try {
            Dimension size = mDriver.manage().window().getSize();
            Point source = new Point(size.getWidth(), size.getHeight());
            float halfY = source.y / 2;
            float halfX = source.x / 2;
            int angle = (int) Math.toDegrees(Math.atan(halfY / halfX));
            int halfDigonal = (int) Math.sqrt((Math.pow(halfX, 2) + (Math.pow(halfY, 2))));
            float percentageZoom = Float.parseFloat(Data) / 100;
            int xExtension = (int) (Math.cos(angle) * halfDigonal * percentageZoom);
            int yExtension = (int) (Math.sin(angle) * halfDigonal * percentageZoom);
            int startXFingure1 = source.x / 2;
            int endXFingure1 = (int) (source.x / 2 + xExtension);
            int startXFingure2 = source.x / 2;
            int endXFingure2 = (int) (source.x / 2 - xExtension);
            int startYFingure1 = source.y / 2;
            int endYFingure1 = (int) (source.y / 2 - yExtension);
            int startYFingure2 = source.y / 2;
            int endYFingure2 = (int) (source.y / 2 + yExtension);
            PointerInput finger1 = new PointerInput(PointerInput.Kind.TOUCH, "finger1");
            PointerInput finger2 = new PointerInput(PointerInput.Kind.TOUCH, "finger2");
            Sequence pinchAndZoom1 = new Sequence(finger1, 1);
            pinchAndZoom1.addAction(finger1.createPointerMove(Duration.ZERO, PointerInput.Origin.viewport(), startXFingure1, startYFingure1));
            pinchAndZoom1.addAction(finger1.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
            pinchAndZoom1.addAction(new Pause(finger1, Duration.ofMillis(200)));
            pinchAndZoom1.addAction(finger1.createPointerMove(Duration.ofMillis(200), PointerInput.Origin.viewport(), endXFingure1, endYFingure1));
            pinchAndZoom1.addAction(finger1.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
            Sequence pinchAndZoom2 = new Sequence(finger2, 1);
            pinchAndZoom2.addAction(finger2.createPointerMove(Duration.ZERO,
                    PointerInput.Origin.viewport(), startXFingure2, startYFingure2));
            pinchAndZoom2.addAction(finger2.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
            pinchAndZoom2.addAction(new Pause(finger2, Duration.ofMillis(200)));
            pinchAndZoom2.addAction(finger2.createPointerMove(Duration.ofMillis(200),
                    PointerInput.Origin.viewport(), endXFingure2, endYFingure2));
            pinchAndZoom2.addAction(finger2.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));

            ((RemoteWebDriver) mDriver).perform(Arrays.asList(pinchAndZoom1, pinchAndZoom2));

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    ```
---------------------------------

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

## **rotatePortrait**

**Description**: This function is used to roate screen orientation to portrait.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`rotatePortrait`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Rotate Screen orientation to Portrait", input = InputType.NO, condition = InputType.NO)
    public void rotatePortrait() {
        try {
            ((SupportsRotation) mDriver).rotate(org.openqa.selenium.ScreenOrientation.PORTRAIT);
            Report.updateTestLog(Action, "Screen orientation changed to Portrait ", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to change the Screen orientation to Portrait, Error: " + e.getMessage(), Status.FAIL);
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

## **shake**

**Description**: This function is used to shake the device.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`shake`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Shake Device")
    public void shake() {
        try {
            if (mDriver instanceof AndroidDriver) {
                ((AndroidDriver) mDriver).executeScript("mobile: shake");
            } else if (mDriver instanceof IOSDriver) {
                ((IOSDriver) mDriver).executeScript("mobile: shake");

            }
            Report.updateTestLog(Action, "Performed Shake Operation", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to perform Shake operation, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```

---------------------------------

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

## **swipeElement**

**Description**: This function is used to swipe the element to specific position.

**Input Format** : @Expected data in integer

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | mobileObject     |:green_circle: [`swipeElement`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | mobileObject     |:green_circle: [`swipeElement`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | mobileObject     |:green_circle: [`swipeElement`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.APP, desc = "Swipe Element to <Input> position", input = InputType.YES, condition = InputType.OPTIONAL)
    public void swipeElement() {
        try {
            int duration = 2000;
            Dimension size = mDriver.manage().window().getSize();
            Rectangle rectangle = Element.getRect();
            Point point = new Point(rectangle.x + (rectangle.width / 2), rectangle.y + (rectangle.height / 2));
            int startX = point.x;
            int startY = point.y;
            int endX = 0;
            int endY = 0;

            switch (Data) {
                case "Left":
                    endY = startY;
                    break;

                case "Right":
                    endX = (int) (0.9 * size.getWidth());
                    endY = startY;
                    break;

                case "Up":
                    endX = startX;
                    break;

                case "Down":
                    endX = startX;
                    endY = size.getHeight();
            }
            if (!Condition.equals("")) {
                duration = Integer.parseInt(Condition);
            }
            PointerInput finger = new PointerInput(PointerInput.Kind.TOUCH, "finger");
            Sequence seq = new Sequence(finger, 1);
            seq.addAction(finger.createPointerMove(Duration.ofMillis(0), PointerInput.Origin.viewport(), startX, startY));
            seq.addAction(finger.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
            seq.addAction(finger.createPointerMove(Duration.ofMillis(duration), PointerInput.Origin.viewport(), endX, endY));
            seq.addAction(finger.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
            ((RemoteWebDriver) mDriver).perform(Arrays.asList(seq));
            Report.updateTestLog(Action, "Element Swiped to " + Data, Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to Swipe the Element to" + Data + ", Error: " + e.getMessage(), Status.FAIL);
        }
    }    
    ```

----------------------

## **swipeMobileScreen**

**Description**: This function is used to swipe the mobile screen to specific position.

**Input Format** : @Expected data in integer

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Mobile     |:green_circle: [`swipeMobileScreen`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Mobile     |:green_circle: [`swipeMobileScreen`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Mobile     |:green_circle: [`swipeMobileScreen`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Swipe Screen to <Input> position", input = InputType.YES, condition = InputType.OPTIONAL)
    public void swipeMobileScreen() {
        try {
            int duration = 2000;
            Dimension size = mDriver.manage().window().getSize();
            int startX = 0;
            int startY = 0;
            int endX = 0;
            int endY = 0;

            switch (Data) {
                case "Left":
                    startX = (int) (0.8 * size.getWidth());
                    startY = (int) size.getHeight() / 2;
                    endX = (int) (0.2 * size.getWidth());
                    endY = startY;
                    break;

                case "Right":
                    startX = (int) (0.2 * size.getWidth());
                    startY = (int) size.getHeight() / 2;
                    endX = (int) (0.8 * size.getWidth());
                    endY = startY;
                    break;

                case "Up":
                    startX = (int) (size.getWidth() / 2);
                    startY = (int) (0.8 * size.getHeight());
                    endX = startX;
                    endY = (int) (0.2 * size.getHeight());
                    break;

                case "Down":
                    startX = (int) (size.getWidth() / 2);
                    startY = (int) (0.2 * size.getHeight());
                    endX = startX;
                    endY = (int) (0.8 * size.getHeight());
                    break;
            }
            if (!Condition.equals("")) {
                duration = Integer.parseInt(Condition);
            }
            PointerInput finger = new PointerInput(PointerInput.Kind.TOUCH, "finger");
            Sequence seq = new Sequence(finger, 1);
            seq.addAction(finger.createPointerMove(Duration.ofMillis(0), PointerInput.Origin.viewport(), startX, startY));
            seq.addAction(finger.createPointerDown(PointerInput.MouseButton.LEFT.asArg()));
            seq.addAction(finger.createPointerMove(Duration.ofMillis(duration), PointerInput.Origin.viewport(), endX, endY));
            seq.addAction(finger.createPointerUp(PointerInput.MouseButton.LEFT.asArg()));
            ((RemoteWebDriver) mDriver).perform(Arrays.asList(seq));
            Report.updateTestLog(Action, "Screen swiped to " + Data, Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to Swipe the Screen to" + Data + ", Error: " + e.getMessage(), Status.FAIL);
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

## **toggleInternetData**

**Description**: This function is used to toggle internet data.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`toggleInternetData`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Toggle Internet Data ", input = InputType.NO, condition = InputType.NO)
    public void toggleInternetData() {
        try {
            if (mDriver instanceof AndroidDriver) {
                ((AndroidDriver) mDriver).toggleData();
            } else if (mDriver instanceof IOSDriver) {

            }
            Report.updateTestLog(Action, "Toggle Data is done ", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to toggle Data, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
----------------------------------------

## **toggleLocationServices**

**Description**: This function is used to toggle location services.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`toggleLocationServices`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Toggle Location Services", input = InputType.NO, condition = InputType.NO)
    public void toggleLocationServices() {
        try {
            if (mDriver instanceof AndroidDriver) {
                ((AndroidDriver) mDriver).toggleLocationServices();
            } else if (mDriver instanceof IOSDriver) {

            }
            Report.updateTestLog(Action, "Toggle Location Services is done ", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to toggle Location Services, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
-------------------------------

## **toggleWifi**

**Description**: This function is used to toggle Wifi.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`toggleWifi`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Toggle Wifi", input = InputType.NO, condition = InputType.NO)
    public void toggleWifi() {
        try {
            if (mDriver instanceof AndroidDriver) {
                ((AndroidDriver) mDriver).toggleWifi();
            } else if (mDriver instanceof IOSDriver) {

            }
            Report.updateTestLog(Action, "Toggle Wifi is done ", Status.DONE);
        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to toggle Wifi, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```
----------------------------------------

## **unlockMobileDevice**

**Description**: This function is used to unlock mobile device.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Mobile |:green_circle: [`unlockMobileDevice`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.MOBILE, desc = "Unlock Mobile Device", input = InputType.NO, condition = InputType.NO)
    public void unlockMobileDevice() {
        try {
            if (mDriver instanceof AndroidDriver) {
                boolean lockAndroid = ((AndroidDriver) mDriver).isDeviceLocked();
                if (lockAndroid) {
                    ((AndroidDriver) mDriver).unlockDevice();
                    Report.updateTestLog(Action, "Device is unlocked successfully ", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Device is unlocked already ", Status.DONE);
                }
            } else if (mDriver instanceof IOSDriver) {
                boolean lockIOS = ((AndroidDriver) mDriver).isDeviceLocked();
                if (lockIOS) {
                    ((AndroidDriver) mDriver).unlockDevice();
                    Report.updateTestLog(Action, "Device is unlocked successfully ", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Device is unlocked already ", Status.DONE);
                }

            }

        } catch (Exception e) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
            Report.updateTestLog(Action, "Unable to Unlock device, Error: " + e.getMessage(), Status.FAIL);
        }
    }
    ```

---------------------------------

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

