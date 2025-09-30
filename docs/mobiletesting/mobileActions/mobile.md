---
icon: material/cellphone
---

# Mobile Actions
------------------------

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

