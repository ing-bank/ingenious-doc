---
icon: material/keyboard-variant
---

# KeyBoard Actions
------------------------

## **KeyPressOnElement**

**Description**: This function is used to **press a key or combination of keys** on an element.

**Input Format** : @Expected Keys or combination. Examples :

`F1` - `F12`, `Digit0` - `Digit9`, `KeyA` - `KeyZ`, `Backquote`, `Minus`, `Equal`, `Backslash`, `Backspace`, `Tab`, `Delete`, `Escape`, `ArrowDown`, `End`, `Enter`, `Home`, `Insert`, `PageDown`, `PageUp`, `ArrowRight`, `ArrowUp`, etc.

Following modification shortcuts are also supported: `Shift`, `Control`, `Alt`, `Meta`, `ShiftLeft`.

Holding down `Shift` will type the text that corresponds to the `key` in the upper case.

If key is a single character, it is case-sensitive, so the values a and A will generate different respective texts.

Shortcuts such as `key: "Control+o"` or `key: "Control+Shift+T"` are supported as well. When specified with the modifier, modifier is pressed and being held while the subsequent key is being pressed.


A full list of keys can be found [here](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events/Keyboard_event_key_values)

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Object     |:green_circle: [`KeyPressOnElement`](#)   | @value       |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span> 
    | Object     |:green_circle: [`KeyPressOnElement`](#)   | Sheet:Column |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Object     |:green_circle: [`KeyPressOnElement`](#)   | %dynamicVar% |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Press the [<Object>] ",input = InputType.YES)
        public void KeyPressOnElement() {
        try {
                Locator.press(Data);
                Report.updateTestLog(Action, "Pressed key ["+ Data + "] on " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **KeyPress**

**Description**: This function is used to **press a key or combination of keys** .

**Input Format** : @Expected Keys or combination. Examples :

`F1` - `F12`, `Digit0` - `Digit9`, `KeyA` - `KeyZ`, `Backquote`, `Minus`, `Equal`, `Backslash`, `Backspace`, `Tab`, `Delete`, `Escape`, `ArrowDown`, `End`, `Enter`, `Home`, `Insert`, `PageDown`, `PageUp`, `ArrowRight`, `ArrowUp`, etc.

Following modification shortcuts are also supported: `Shift`, `Control`, `Alt`, `Meta`, `ShiftLeft`.

Holding down `Shift` will type the text that corresponds to the `key` in the upper case.

If key is a single character, it is case-sensitive, so the values a and A will generate different respective texts.

Shortcuts such as `key: "Control+o"` or `key: "Control+Shift+T"` are supported as well. When specified with the modifier, modifier is pressed and being held while the subsequent key is being pressed.


A full list of keys can be found [here](https://developer.mozilla.org/en-US/docs/Web/API/UI_Events/Keyboard_event_key_values)

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`KeyPress`](#)   | @value       |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span> 
    | Browser     |:green_circle: [`KeyPress`](#)   | Sheet:Column |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Browser     |:green_circle: [`KeyPress`](#)   | %dynamicVar% |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Press the [<Object>] ",input = InputType.YES)
        public void KeyPressOnElement() {
        try {
                Locator.press(Data);
                Report.updateTestLog(Action, "Pressed key ["+ Data + "] on " + "["+ObjectName+"]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **KeyUp**

**Description**: This function is used to **press up a key or combination of keys** .

**Input Format** : @Expected Keys or combination. Examples : as stated above.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`KeyUp`](#)   | @value       |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span> 
    | Browser     |:green_circle: [`KeyUp`](#)   | Sheet:Column |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Browser     |:green_circle: [`KeyUp`](#)   | %dynamicVar% |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Press Key Up ",input = InputType.YES)
        public void KeyUp() {
        try {
                Page.keyboard().up(Data);
                Report.updateTestLog(Action, "Pressed key ["+ Data + "] Up", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **KeyDown**

**Description**: This function is used to **press down a key or combination of keys** .

**Input Format** : @Expected Keys or combination. Examples : as stated above.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`KeyDown`](#)   | @value       |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span> 
    | Browser     |:green_circle: [`KeyDown`](#)   | Sheet:Column |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Browser     |:green_circle: [`KeyDown`](#)   | %dynamicVar% |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Press Key Down ",input = InputType.YES)
        public void KeyDown() {
        try {
                Page.keyboard().down(Data);
                Report.updateTestLog(Action, "Pressed key ["+ Data + "] Down", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```

----------------------

## **KeyInsertText**

**Description**: This function is used to **insert a text via key press** .

**Input Format** : @Expected Keys or combination. Examples : as stated above.

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Browser     |:green_circle: [`KeyInsertText`](#)   | @value       |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span> 
    | Browser     |:green_circle: [`KeyInsertText`](#)   | Sheet:Column |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Browser     |:green_circle: [`KeyInsertText`](#)   | %dynamicVar% |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Insert Text via Keyboard",input = InputType.YES)
        public void KeyInsertText() {
        try {
                Page.keyboard().insertText(Data);
                Report.updateTestLog(Action, "Inserted Text ["+ Data + "]", Status.DONE);
            } catch(Exception e) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, e);
                Report.updateTestLog("Could not perfom ["+Action+"] action", "Error: " + e.getMessage(),Status.FAIL);
            }
        }
    ```