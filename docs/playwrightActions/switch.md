---
icon: octicons/arrow-switch-16
---

# Switch

----------------------------------

## **clickAndSwitchToNewPage**

**Description**:  This function will click on the Locator and wait till switch to new page is successful.

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Object     |:green_circle: [`clickAndSwitchToNewPage`](#)           |               |           |         | |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.PLAYWRIGHT, desc = "Switch to new Page", input = InputType.NO)
        public void clickAndSwitchToNewPage() {
            try {
                Page popup = Page.waitForPopup(() -> {
                    Locator.click();
                });
                BrowserContext = popup.context();
                List<Page> pages = popup.context().pages();

                AObject.setPage(pages.get(1));
                Page = pages.get(1);
                Page.bringToFront();
                Driver.setPage(pages.get(1));
                Report.updateTestLog(Action, "Successfully switched to new Page", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong" + e.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------

## **createAndSwitchToNewPage**

**Description**:  This function will create a new empty page and switch the control to it.

**Input Format** :   @Expected Text should be a Page URL

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`createAndSwitchToNewPage`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`createAndSwitchToNewPage`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`createAndSwitchToNewPage`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Switch to new Page", input = InputType.YES)
        public void createAndSwitchToNewPage() {
            try {
                Page page = BrowserContext.newPage();
                page.navigate(Data);
                AObject.setPage(page);
                Page = page;
                Page.bringToFront();
                Driver.setPage(page);

                Report.updateTestLog(Action, "Successfully switched to new Page with URL: " + Data, Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong" + e.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------

## **createAndSwitchToNewContext**

**Description**:  This function will create a new empty browser context and switch the control to it.

**Input Format** :   @Expected Text should be URL

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`createAndSwitchToNewContext`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`createAndSwitchToNewContext`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`createAndSwitchToNewContext`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Switch to new Browser Context", input = InputType.YES)
        public void createAndSwitchToNewContext() {
            try {
                Browser browser = BrowserContext.browser();
                BrowserContext = browser.newContext();
                Page = BrowserContext.newPage();
                Page.navigate(Data);
                AObject.setPage(Page);
                Page.bringToFront();
                Driver.setPage(Page);

                Report.updateTestLog(Action, "Successfully switched to new Context with URL: " + Data, Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong" + e.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------

## **switchToPageByIndex**

**Description**:  This function will switch the control to a page by its index.

**Input Format** :   The index of the target page. Example `@0` or `@1` 

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`switchToPageByIndex`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`switchToPageByIndex`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`switchToPageByIndex`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Switch to Page by index", input = InputType.YES)
        public void switchToPageByIndex() {
            try {
                int index = Integer.parseInt(Data);
                List<Page> pages = BrowserContext.pages();
                AObject.setPage(pages.get(index));
                Page = pages.get(index);
                Page.bringToFront();
                Driver.setPage(pages.get(index));

                Report.updateTestLog(Action, "Successfully switched to Page [" + index + "]", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong" + e.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------

## **switchToContextByIndex**

**Description**:  This function will switch the control to a browser context by its index.

**Input Format** :   The index of the target browser context. Example `@0` or `@1` 

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`switchToContextByIndex`](#)   | @value       | `optional` page timeout in milliseconds      | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`switchToContextByIndex`](#)   | Sheet:Column | `optional` page timeout in milliseconds      | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`switchToContextByIndex`](#)   | %dynamicVar% | `optional` page timeout in milliseconds      | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Switch to Context by index", input = InputType.YES, condition = InputType.OPTIONAL)
        public void switchToContextByIndex() throws InterruptedException {
            try {
                int index = Integer.parseInt(Data);
                List<com.microsoft.playwright.BrowserContext> contexts = BrowserContext.browser().contexts();
                BrowserContext = contexts.get(index);
                Thread.sleep(500);
                int pageIndex = 0;
                if (!Condition.isEmpty()) {
                    pageIndex = Integer.parseInt(Condition);
                }

                Page = BrowserContext.pages().get(pageIndex);
                AObject.setPage(Page);
                Page.bringToFront();
                Driver.setPage(Page);

                Report.updateTestLog(Action, "Successfully switched to Context [" + index + "]", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong" + e.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------

## **switchToContextByPageTitle**

**Description**:  This function will switch the control to a page by its title.

**Input Format** :   @Expected Text should be a Page Title

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`switchToContextByPageTitle`](#)   | @value       | `optional` page timeout in milliseconds      | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`switchToContextByPageTitle`](#)   | Sheet:Column |  `optional` page timeout in milliseconds     | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`switchToContextByPageTitle`](#)   | %dynamicVar% | `optional` page timeout in milliseconds      | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Switch to Context by Page Title", input = InputType.YES, condition = InputType.OPTIONAL)
        public void switchToContextByPageTitle() {
            try {
                List<com.microsoft.playwright.BrowserContext> contexts = BrowserContext.browser().contexts();
                int pageIndex = 0;
                boolean found = false;
                if (!Condition.isEmpty()) {
                    pageIndex = Integer.parseInt(Condition);
                }
                for (com.microsoft.playwright.BrowserContext context : contexts) {
                    if (context.pages().get(pageIndex).title().contains(Data)) {
                        BrowserContext = context;
                        Page = BrowserContext.pages().get(pageIndex);
                        AObject.setPage(Page);
                        Page.bringToFront();
                        Driver.setPage(Page);
                        found = true;
                        Report.updateTestLog(Action, "Successfully switched to Context with Page title matching [" + Data + "]", Status.DONE);
                        break;
                    }
                }
                if (!found) {
                    Report.updateTestLog(Action, "Context with Page title matching [" + Data + "] could not be found", Status.FAIL);
                }
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong" + e.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------

## **switchToContextByPageURL**

**Description**:  This function will switch the control to a page by its current url (or part of it)

**Input Format** :   @Expected Text should be a Page URL

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`switchToContextByPageURL`](#)   | @value       | `optional` page timeout in milliseconds      | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`switchToContextByPageURL`](#)   | Sheet:Column |  `optional` page timeout in milliseconds     | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`switchToContextByPageURL`](#)   | %dynamicVar% |  `optional` page timeout in milliseconds     | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Switch to Context by Page URL", input = InputType.YES, condition = InputType.OPTIONAL)
        public void switchToContextByPageURL() {
            try {
                List<com.microsoft.playwright.BrowserContext> contexts = BrowserContext.browser().contexts();
                int pageIndex = 0;
                boolean found = false;
                if (!Condition.isEmpty()) {
                    pageIndex = Integer.parseInt(Condition);
                }
                for (com.microsoft.playwright.BrowserContext context : contexts) {
                    if (context.pages().get(pageIndex).url().contains(Data)) {
                        BrowserContext = context;
                        Page = BrowserContext.pages().get(pageIndex);
                        AObject.setPage(Page);
                        Page.bringToFront();
                        Driver.setPage(Page);
                        found = true;
                        Report.updateTestLog(Action, "Successfully switched to Context with Page URL matching [" + Data + "]", Status.DONE);
                        break;
                    }
                }
                if (!found) {
                    Report.updateTestLog(Action, "Context with Page URL matching [" + Data + "] could not be found", Status.FAIL);
                }
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong" + e.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------

## **switchToMainPage**

**Description**:  This function will switch the control to the main page (Index = 0).

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`switchToMainPage`](#)   |       |       | | 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Switch to main Page", input = InputType.NO)
        public void switchToMainPage() {
            try {
                List<Page> pages = BrowserContext.pages();

                AObject.setPage(pages.get(0));
                Page = pages.get(0);
                Page.bringToFront();
                Driver.setPage(pages.get(0));

                Report.updateTestLog(Action, "Successfully switched to main Page", Status.DONE);
            } catch (Exception e) {
                Report.updateTestLog(Action, "Something went wrong" + e.getMessage(), Status.DEBUG);
            }
        }
    ```