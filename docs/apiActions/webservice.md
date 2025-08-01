# API Testing Actions

## **addHeader**

**Description**:  This function is used to add a header for a Rest/SOAP API request.

**Input Format** : @`HeaderName`=`HeaderValue`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`addHeader`](#)   | @`HeaderName`=`HeaderValue`      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`addHeader`](#)    | Sheet:Column containing `HeaderName`=`HeaderValue`|       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`addHeader`](#)    | %dynamicVar% containing `HeaderName`=`HeaderValue` |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Webservice     |:green_circle: [`addHeader`](#)    | @`HeaderName`=`{SheetName:ColumnName}` |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Webservice     |:green_circle: [`addHeader`](#)    | @`HeaderName`=`%dynamicVar%` |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    This function adds all the **Headers** into a HashMap `headerlist`. Then those are applied to the request as :

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Add Header ", input = InputType.YES)
        public void addHeader() {
            try {

                List<String> sheetlist = Control.getCurrentProject().getTestData().getTestDataFor(Control.exe.runEnv())
                        .getTestDataNames();
                for (int sheet = 0; sheet < sheetlist.size(); sheet++) {
                    if (Data.contains("{" + sheetlist.get(sheet) + ":")) {
                        com.ing.datalib.testdata.model.TestDataModel tdModel = Control.getCurrentProject().getTestData()
                                .getTestDataByName(sheetlist.get(sheet));
                        List<String> columns = tdModel.getColumns();
                        for (int col = 0; col < columns.size(); col++) {
                            if (Data.contains("{" + sheetlist.get(sheet) + ":" + columns.get(col) + "}")) {
                                Data = Data.replace("{" + sheetlist.get(sheet) + ":" + columns.get(col) + "}",
                                        userData.getData(sheetlist.get(sheet), columns.get(col)));
                            }
                        }
                    }
                }

                Collection<Object> valuelist = Control.getCurrentProject().getProjectSettings().getUserDefinedSettings()
                        .values();
                for (Object prop : valuelist) {
                    if (Data.contains("{" + prop + "}")) {
                        Data = Data.replace("{" + prop + "}", prop.toString());
                    }
                }

                                                            

                if (headers.containsKey(key)) {
                    headers.get(key).add(Data);
                } else {
                    ArrayList<String> toBeAdded = new ArrayList<String>();
                    toBeAdded.add(Data);
                    headers.put(key, toBeAdded);
                }

                Report.updateTestLog(Action, "Header added " + Data, Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error adding Header :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }

    ```
-----------------------------

## **addURLParam**

**Description**: This function is used to add the parameters in your URL in a key value pair (as query strings or URL query parameters)

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Webservice | :green_circle: [`addURLParam`](#) |@key=value                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Add Parameters ", input = InputType.YES)
        public void addURLParam() {

            try {
                if (urlParams.containsKey(key)) {
                    urlParams.get(key).add(Data);
                } else {
                    ArrayList<String> toBeAdded = new ArrayList<String>();
                    toBeAdded.add(Data);
                    urlParams.put(key, toBeAdded);
                }
                Report.updateTestLog(Action, "URl Param added " + Data, Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error adding Header :" + "\n" + ex.getMessage(), Status.DEBUG);
            }

        }
    ```
-----------------------------

## **setEndPoint**

**Description**: This function is used to set the End Point for a Rest/SOAP API. 

**Input Format** : @EndPoint

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`setEndPoint`](#)  | @Endpoint (from Editor)      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`setEndPoint`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`setEndPoint`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded`, passed inside the **Endpoint editor** which is capable of parameterising the Endpoint (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    Performs opening of URL Connection

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Set End Point ", input = InputType.YES, condition = InputType.OPTIONAL)
        public void setEndPoint() {
            try {
                String resource = handlePayloadorEndpoint(Data);
                endPoints.put(key, resource);
                httpAgentCheck();
                OpenURLconnection();
                Report.updateTestLog(Action, "End point set : " + resource, Status.DONE);
            } catch (FileNotFoundException ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error setting the end point :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }

    ```
-----------------------------

## **closeConnection**

**Description**: This function is used to close a connection for a Rest/SOAP API request.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Webservice |:green_circle: [`closeConnection`](#) |                             |           |         |

=== "Corresponding Code"

    Performs disconnection of the URL connection
    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Close the connection ", input = InputType.NO)
        public void closeConnection() {
            try {
                // httpConnections.get(key).disconnect();
                headers.remove(key);
                responsebodies.remove(key);
                basicAuthorization = "";
                responsecodes.remove(key);
                responsemessages.remove(key);
                endPoints.remove(key);
                Report.updateTestLog(Action, "Connection is closed", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error closing connection :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

-----------------------------------

## **postSoapRequest**

**Description**: This function is used to perform POST action on a SOAP API.

**Input Format** : @Expected Payload

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`postSoapRequest`](#)  | @Payload (from Editor)      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`postSoapRequest`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`postSoapRequest`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded`, passed inside the **XML editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "POST SOAP Request ", input = InputType.YES, condition = InputType.OPTIONAL)
        public void postSoapRequest() {
            try {
                createhttpRequest(RequestMethod.POST);
            } catch (InterruptedException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        }
    ```
----------------------------------------

## **postRestRequest**

**Description**: This function is used to perform POST action on a Rest API.

**Input Format** : @Expected Payload

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`postRestRequest`](#)   | @Payload (from Editor)      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`postRestRequest`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`postRestRequest`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded`, passed inside the **JSON editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "POST Rest Request ", input = InputType.YES, condition = InputType.OPTIONAL)
        public void postRestRequest() {
            try {
                createhttpRequest(RequestMethod.POST);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    ```

----------------------

## **putRestRequest**

**Description**: This function is used to perform PUT action on a Rest API.

**Input Format** : @Expected Payload

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`putRestRequest`](#)   | @Payload (from Editor)      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`putRestRequest`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`putRestRequest`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded`, passed inside the **JSON editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "PUT Rest Request ", input = InputType.YES, condition = InputType.OPTIONAL)
        public void putRestRequest() {
            try {
                createhttpRequest(RequestMethod.PUT);
            } catch (InterruptedException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        }
    ```

----------------------
## **patchRestRequest**

**Description**: This function is used to perform PATCH action on a Rest API.

**Input Format** : @Expected Payload

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`patchRestRequest`](#)   | @Payload (from Editor)      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`patchRestRequest`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`patchRestRequest`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded`, passed inside the **XML editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "PATCH Rest Request ", input = InputType.YES, condition = InputType.OPTIONAL)
        public void patchRestRequest() {
            try {
                createhttpRequest(RequestMethod.PATCH);
            } catch (InterruptedException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        }
    ```
----------------------

## **getRestRequest**

**Description**: This function is used to perform GET action on a Rest API.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Webservice |:green_circle: [`getRestRequest`](#)  |                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "GET Rest Request ", input = InputType.NO, condition = InputType.OPTIONAL)
        public void getRestRequest() {
            try {
                createhttpRequest(RequestMethod.GET);
            } catch (InterruptedException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        }
    ```

----------------------

## **deleteRestRequest**

**Description**:  This function is used to perform DELETE action on a Rest API.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Webservice |:green_circle: [`deleteRestRequest`](#) |                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "DELETE Rest Request ", input = InputType.NO)
        public void deleteRestRequest() {
            try {
                createhttpRequest(RequestMethod.DELETE);
            } catch (InterruptedException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        }
    ```
-----------------------------

## **deleteWithPayload**

**Description**:  This function is used to perform DELETE action on a Rest API with payload.

| ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`deleteWithPayload`](#)   | @Payload (from Editor)      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`deleteWithPayload`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`deleteWithPayload`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded`, passed inside the **XML editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.      |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "DELETE with Payload ", input = InputType.YES)
    public void deleteWithPayload() {
        try {
            createhttpRequest(RequestMethod.DELETEWITHPAYLOAD);
        } catch (InterruptedException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
    ```
-----------------------------