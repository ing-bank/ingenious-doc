---
icon: material/api-off
---

# RequestFulfill

----------------------------------
## **RouteFulfillEndpoint**

**Description**:  This function will set the endpoint for the request which is required to be mocked.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`RouteFulfillEndpoint`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`RouteFulfillEndpoint`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`RouteFulfillEndpoint`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Set Endpoint for mocking request", input = InputType.YES)
        public void RouteFulfillEndpoint() {
            try {
                String resource = handlePayloadorEndpoint(Data);
                mockEndPoints.put(key, resource);
                Report.updateTestLog(Action, "End point set : " + resource, Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error setting the end point :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------

## **RouteFulfillSetBody**

**Description**:  This function will set the body for the request which is required to be mocked.

**Input Format** :   @Expected Text

=== "Usage"

    | ObjectName | Action                     | Input         | Condition |Reference|  |
    |------------|----------------------------|---------------|-----------|---------|--|
    | Browser     |:green_circle: [`RouteFulfillSetBody`](#)   | @value       |       | PageName|<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Browser     |:green_circle: [`RouteFulfillSetBody`](#)   | Sheet:Column |       | PageName|<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Browser     |:green_circle: [`RouteFulfillSetBody`](#)   | %dynamicVar% |       | PageName|<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.BROWSER, desc = "Set body for mocking request", input = InputType.YES)
        public void RouteFulfillSetBody() {
            try {
                Route.FulfillOptions fulfillOptions = new Route.FulfillOptions();
                Page.route(mockEndPoints.get(key), route -> {
                    try {
                        route.fulfill(fulfillOptions.setBody(handlePayloadorEndpoint(Data)));
                    } catch (FileNotFoundException ex) {
                        Logger.getLogger(RequestFulfill.class.getName()).log(Level.SEVERE, null, ex);
                    }
                });
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error setting the body :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------