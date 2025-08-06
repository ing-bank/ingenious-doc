# Store Actions

## **storeResponseBodyInDataSheet**

**Description**: This function is used to store the response body of SOAP/REST request, into a respective column of a given datasheet.

**Input Format** : @Expected **DatasheetName:ColumnName**

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`storeResponseBodyInDataSheet`](#)  | Sheet:Column      |      | |<span style="color:#559BD1">:arrow_left:   *Datasheet where value is supposed to be stored*</span>

    Note: Ensure that your data sheet doesn't contain column names with spaces. 

=== "Corresponding Code"

    ```java 
    @Action(object = ObjectType.WEBSERVICE, desc = "Store Response Message In DataSheet ", input = InputType.YES)
        public void storeResponseBodyInDataSheet() {
            try {
                String strObj = Input;
                if (strObj.matches(".*:.*")) {
                    try {
                        System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                        String sheetName = strObj.split(":", 2)[0];
                        String columnName = strObj.split(":", 2)[1];
                        userData.putData(sheetName, columnName, responsebodies.get(key));
                        Report.updateTestLog(Action, "Response body is stored in " + strObj, Status.DONE);
                    } catch (Exception ex) {
                        Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
                        Report.updateTestLog(Action, "Error Storing text in datasheet :" + ex.getMessage(), Status.DEBUG);
                    }
                } else {
                    Report.updateTestLog(Action,
                            "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",Status.DEBUG);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error Storing response body in datasheet :" + "\n" + ex.getMessage(),Status.DEBUG);
            }
        }
    ```

----------------------

## **storeXMLelement**

**Description**: This function is used to store a certain XML tag value inside the response body of SOAP request, into a variable.

**Input Format** : @`XPath` of the tag

**Condition Format**: %variable%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`storeXMLelement`](#)  | @`XPath`       |  %var%     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`storeXMLelement`](#)  | **Sheet:Column** containing `XPath`  |%var%| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`storeXMLelement`](#)   | %Var% containing `XPath` |%var%| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Store XML Element", input = InputType.YES, condition = InputType.YES)
        public void storeXMLelement() {
            try {
                String variableName = Condition;
                String expression = Data;
                if (variableName.matches("%.*%")) {
                    DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                    DocumentBuilder dBuilder;
                    InputSource inputSource = new InputSource();
                    inputSource.setCharacterStream(new StringReader(responsebodies.get(key)));
                    dBuilder = dbFactory.newDocumentBuilder();
                    Document doc = dBuilder.parse(inputSource);
                    doc.getDocumentElement().normalize();
                    XPath xPath = XPathFactory.newInstance().newXPath();
                    NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
                    Node nNode = nodeList.item(0);
                    String value = nNode.getNodeValue();
                    addVar(variableName, value);
                    Report.updateTestLog(Action, "XML element value stored", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
                }
            } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                    | SAXException ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error Storing XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }

    ```
-------------------------------

## **storeXMLelementInDataSheet**

**Description**: This function is used to store a certain XML tag value inside the response body of SOAP request, into a respective column of a given datasheet.

**Input Format** : @Expected datasheet name:column name

**Condition Format**: XPath of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`storeXMLelementInDataSheet'](#)  | Sheet:Column      |  XPath     | |<span style="color:Blue"><< *Datasheet to where value is supposed br stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces. 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Store XML Element In DataSheet ", input = InputType.YES, condition = InputType.YES)
        public void storeXMLelementInDataSheet() {

            try {
                String strObj = Input;
                if (strObj.matches(".*:.*")) {
                    try {
                        String expression = "";
                        System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                        String sheetName = strObj.split(":", 2)[0];
                        String columnName = strObj.split(":", 2)[1];
                        String xmlText = responsebodies.get(key);
                        DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                        DocumentBuilder dBuilder;
                        InputSource inputSource = new InputSource();
                        inputSource.setCharacterStream(new StringReader(xmlText));
                        dBuilder = dbFactory.newDocumentBuilder();
                        Document doc = dBuilder.parse(inputSource);
                        doc.getDocumentElement().normalize();
                        XPath xPath = XPathFactory.newInstance().newXPath();
                        if (Condition.matches("%.*%"))
                            expression = getVar(Condition);
                        else
                            expression = Condition;
                        NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
                        Node nNode = nodeList.item(0);
                        String value = nNode.getNodeValue();
                        userData.putData(sheetName, columnName, value);
                        Report.updateTestLog(Action, "Element text [" + value + "] is stored in " + strObj, Status.DONE);
                    } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException| SAXException ex) {
                        Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
                        Report.updateTestLog(Action, "Error Storing XML element in datasheet :" + "\n" + ex.getMessage(),Status.DEBUG);
                    }
                } else {
                    Report.updateTestLog(Action,
                            "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",Status.DEBUG);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error Storing XML element in datasheet :" + "\n" + ex.getMessage(),Status.DEBUG);
            }

        }
    ```

---------------------------------

## **storeJSONelement**

**Description**: This function is used to store a certain JSON tag value from the response body of REST request, into a variable.

**Input Format** : @`JSONPath` of the tag

**Condition Format**: %variable%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`storeJSONelement`](#)   | @`JSONPath`       |  %var%     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`storeJSONelement`](#)   | **Sheet:Column** containing `JSONPath`  |%var%| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`storeJSONelement`](#)   | %Var% containing `JSONPath` |%var%| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Store JSON Element", input = InputType.YES, condition = InputType.YES)
        public void storeJSONelement() {
            try {
                String variableName = Condition;
                String jsonpath = Data;
                if (variableName.matches("%.*%")) {
                    addVar(variableName, JsonPath.read(responsebodies.get(key), jsonpath).toString());
                    Report.updateTestLog(Action, "JSON element value stored", Status.DONE);
                } else {
                    Report.updateTestLog(Action, "Variable format is not correct", Status.DEBUG);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error Storing JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }

    ```
------------------------------------------

## **storeJSONelementInDataSheet**

**Description**: This function is used to store a certain JSON tag value inside the response body of REST request, into a respective column of a given datasheet.

**Input Format** : @Expected datasheet name:column name

**Condition Format**: JSONPath of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`storeJSONelementInDataSheet`](#)  | Sheet:Column      |  JSONPath     | |<span style="color:Blue"><< *Datasheet to where value is supposed br stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces. 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Store JSON Element In DataSheet ", input = InputType.YES, condition = InputType.YES)
        public void storeJSONelementInDataSheet() {

            try {
                String strObj = Input;
                if (strObj.matches(".*:.*")) {
                    try {
                        System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                        String sheetName = strObj.split(":", 2)[0];
                        String columnName = strObj.split(":", 2)[1];
                        String response = responsebodies.get(key);
                        String jsonpath = Condition;
                        String value = JsonPath.read(response, jsonpath).toString();
                        userData.putData(sheetName, columnName, value);
                        Report.updateTestLog(Action, "Element text [" + value + "] is stored in " + strObj, Status.DONE);
                    } catch (Exception ex) {
                        Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
                        Report.updateTestLog(Action, "Error Storing JSON element in datasheet :" + "\n" + ex.getMessage(),
                                Status.DEBUG);
                    }
                } else {
                    Report.updateTestLog(Action,
                            "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
                            Status.DEBUG);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error Storing JSON element in datasheet :" + "\n" + ex.getMessage(),
                        Status.DEBUG);
            }
        }
    ```

----------------------

## **storeJsonElementCount**

**Description**: This function is used to store the count of JSON elements for a given JSON Path of REST request, into a variable.

**Input Format** : @`JSONPath` of the tag

**Condition Format**: %variable%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`storeJsonElementCount`](#)   | @`JSONPath`       |  %var%     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`storeJsonElementCount`](#)   | **Sheet:Column** containing `JSONPath`  |%var%| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`storeJsonElementCount`](#)   | %Var% containing `JSONPath` |%var%| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Store JSON Element count in variable ", input = InputType.YES, condition = InputType.YES)
        public void storeJsonElementCount() {

            try {
                String variableName = Condition;
                Condition = Data;

                if (variableName.matches("%.*%")) {
                    try {
                        System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                        int actualObjectCountInteger = 1;                                                       //getJsonElementCount();
                        String actualObjectCount = Integer.toString(actualObjectCountInteger);
                        addVar(variableName, actualObjectCount);
                        Report.updateTestLog(Action, "Element count [" + actualObjectCount + "] is stored in " + variableName,
                                Status.DONE);
                    } catch (Exception ex) {
                        Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
                        Report.updateTestLog(Action, "Error Storing JSON element in Variable :" + "\n" + ex.getMessage(),
                                Status.DEBUG);
                    }
                } else {
                    Report.updateTestLog(Action,
                            "Given condition [" + Condition + "] format is invalid. It should be [%Var%]",
                            Status.DEBUG);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error Storing JSON element in Variable :" + "\n" + ex.getMessage(),
                        Status.DEBUG);
            }

        }
    ```
---------------------------------

## **storeJsonElementCountInDataSheet**

**Description**:  This function is used to store in a datasheet the count of JSON elements for a given JSON Path of REST request.

**Input Format** : @Expected datasheet name:column name

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`storeJsonElementCountInDataSheet`](#)   | Sheet:Column      |  JSONPath     | |<span style="color:#559BD1">:arrow_left:   *Datasheet where value is to be stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces. 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Store JSON Element count in Datasheet ", input = InputType.YES, condition = InputType.YES)
        public void storeJsonElementCountInDataSheet() {

            try {
                String strObj = Input;
                if (strObj.matches(".*:.*")) {
                    try {
                        System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                        String sheetName = strObj.split(":", 2)[0];
                        String columnName = strObj.split(":", 2)[1];
                        int actualObjectCountInteger = 1;                                                                         //getJsonElementCount();
                        String actualObjectCount = Integer.toString(actualObjectCountInteger);
                        userData.putData(sheetName, columnName, actualObjectCount);
                        Report.updateTestLog(Action, "Element count [" + actualObjectCount + "] is stored in " + strObj,
                                Status.DONE);
                    } catch (Exception ex) {
                        Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
                        Report.updateTestLog(Action, "Error Storing JSON element in datasheet :" + "\n" + ex.getMessage(),
                                Status.DEBUG);
                    }
                } else {
                    Report.updateTestLog(Action,
                            "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
                            Status.DEBUG);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error Storing JSON element in datasheet :" + "\n" + ex.getMessage(),
                        Status.DEBUG);
            }

        }
    ```
---------------------------------