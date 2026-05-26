---
icon: octicons/browser-16
---

# Structured Data Object Actions

## **assertJsonPathResultContains**

**Description**: This function is used to validate that the value extracted from the JSON response contains the specified text.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertJsonPathResultContains`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertJsonPathResultContains`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertJsonPathResultContains`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert JsonPath Result Contains ", input = InputType.YES)
    public void assertJsonPathResultContains() {
        try {
            String response = responsebodies.get(key);
            String jsonpath = Data;
            String value = JsonPath.read(response, jsonpath).toString();
            String strObj = getInputValue(Input);
            if (value.contains(strObj)) {
                Report.updateTestLog(Action, "Element text contains [" + strObj + "] is as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text [" + value + "] does not contain [" + strObj + "]",
                        Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **assertJsonPathResultNotContains**

**Description**: This function is used to validate that the value extracted from the JSON does not contain the specified text.

**Input Format** : @Text that should NOT be present

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertJsonPathResultNotContains`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertJsonPathResultNotContains`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertJsonPathResultNotContains`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert JsonPath Result Not Contains ", input = InputType.YES)
    public void assertJsonPathResultNotContains() {
        try {
            String response = responsebodies.get(key);
            String jsonpath = Data;
            String value = JsonPath.read(response, jsonpath).toString();
            String strObj = getInputValue(Input);
            if (!value.contains(strObj)) {
                Report.updateTestLog(Action, "Element text [" + value + "] does not contain [" + strObj + "] as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text [" + value + "] contains [" + strObj + "] but should not",
                        Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **assertJsonPathResultEquals**

**Description**: This function is used to validate that the value extracted from the JSON response exactly matches the expected text.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertJsonPathResultEquals`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertJsonPathResultEquals`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertJsonPathResultEquals`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert JsonPath Result Equals ", input = InputType.YES)
    public void assertJsonPathResultEquals() {
        try {
            String response = responsebodies.get(key);
            String jsonpath = Data;
            String value = JsonPath.read(response, jsonpath).toString();
            String strObj = getInputValue(Input);
            if (value.equals(strObj)) {
                Report.updateTestLog(Action, "Element text [" + value + "] is as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text is [" + value + "] but is expected to be [" + strObj + "]",
                        Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **assertJsonPathResultNotEquals**

**Description**: This function is used to validate that the value extracted from the JSON response does not exactly match the specified expected text.

**Input Format** : @Text that should NOT be present

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertJsonPathResultNotEquals`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertJsonPathResultNotEquals`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertJsonPathResultNotEquals`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert JsonPath Result Not Equals ", input = InputType.YES)
    public void assertJsonPathResultNotEquals() {
        try {
            String response = responsebodies.get(key);
            String jsonpath = Data;
            String value = JsonPath.read(response, jsonpath).toString();
            String strObj = getInputValue(Input);
            if (!value.equals(strObj)) {
                Report.updateTestLog(Action, "Element text [" + value + "] is not equal to [" + strObj + "] as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text is [" + value + "] but should not be equal to [" + strObj + "]",
                        Status.FAILNS);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **assertJsonPathResultCount**

**Description**: This function is used to validate that the number of elements selected from JSON response matches the expected count. Supports both arrays and objects.

**Input Format** : @Expected Count

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertJsonPathResultCount`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertJsonPathResultCount`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertJsonPathResultCount`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert JsonPath Result Count ", input = InputType.YES)
    public void assertJsonPathResultCount() {
        try {
            String response = responsebodies.get(key);
            int actualObjectCount = 0;
            JSONParser parser = new JSONParser();
            JSONObject json = (JSONObject) parser.parse(response);
            String strObj = getInputValue(Input);
            try {
                Map<String, String> objectMap = JsonPath.read(json, Data);
                actualObjectCount = objectMap.keySet().size();
            } catch (Exception ex) {
                try {
                    JSONArray objectMap = JsonPath.read(json, Data);
                    actualObjectCount = objectMap.size();
                } catch (Exception ex1) {
                    try {
                        net.minidev.json.JSONArray objectMap = JsonPath.read(json, Data);
                        actualObjectCount = objectMap.size();
                    } catch (Exception ex2) {
                        String objectMap = JsonPath.read(json, Data);
                        actualObjectCount = 1;
                    }
                }
            }

            int expectedObjectCount = Integer.parseInt(strObj);
            if (actualObjectCount == expectedObjectCount) {
                Report.updateTestLog(Action, "Element count [" + expectedObjectCount + "] is as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element count is [" + actualObjectCount + "] but is expected to be [" + expectedObjectCount + "]", Status.FAILNS);
            }

        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **storeJsonPathResultInVariable**

**Description**: This function is used to extract a value from the JSON response and store it in a variable.

**Input Format** : %variableName%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`storeJsonPathResultInVariable`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Store JsonPath Result", input = InputType.YES)
    public void storeJsonPathResultInVariable() {
        try {
            String variableName = Input;
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

## **storeJsonPathResultInDataSheet**

**Description**: This function is used to extract a value from the JSON response and store it in a datasheet.

**Input Format** : Sheet:Column

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`storeJsonPathResultInDataSheet`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Store JsonPath Result In DataSheet ", input = InputType.YES)
    public void storeJsonPathResultInDataSheet() {
        try {
            String dataSheetReference = Input;
            if (dataSheetReference.matches(".*:.*")) {
                try {
                    System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                    String sheetName = dataSheetReference.split(":", 2)[0];
                    String columnName = dataSheetReference.split(":", 2)[1];
                    String response = responsebodies.get(key);
                    String jsonpath = Data;
                    String value = JsonPath.read(response, jsonpath).toString();
                    userData.putData(sheetName, columnName, value);
                    Report.updateTestLog(Action, "Element text [" + value + "] is stored in " + dataSheetReference, Status.DONE);
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
------------------------------------------

## **storeJsonPathResultCountInVariable**

**Description**: This function is used to select elements from the JSON response, count them, and store the resulting count in a variable.

**Input Format** : %variableName%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`storeJsonPathResultCountInVariable`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Store JsonPath Result count in variable ", input = InputType.YES)
    public void storeJsonPathResultCountInVariable() {
        try {
            String varName = Input;
            if (varName.matches("%.*%")) {
                try {
                    System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                    String actualObjectCount = Integer.toString(getJsonElementCount());
                    addVar(varName, actualObjectCount);
                    Report.updateTestLog(Action, "Element count [" + actualObjectCount + "] is stored in " + varName,
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
------------------------------------------

## **storeJsonPathResultCountInDataSheet**

**Description**: This function is used to select elements from the JSON response, count them, and store the resulting count in a datasheet.

**Input Format** : Sheet:Column

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`storeJsonPathResultCountInDataSheet`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Store JsonPath Result count in Datasheet ", input = InputType.YES)
    public void storeJsonPathResultCountInDataSheet() {
        try {
            String dataSheetReference = Input;
            if (dataSheetReference.matches(".*:.*")) {
                try {
                    System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                    String sheetName = dataSheetReference.split(":", 2)[0];
                    String columnName = dataSheetReference.split(":", 2)[1];
                    String actualObjectCount = Integer.toString(getJsonElementCount());
                    userData.putData(sheetName, columnName, actualObjectCount);
                    Report.updateTestLog(Action, "Element count [" + actualObjectCount + "] is stored in " + dataSheetReference,
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
------------------------------------------

## **assertXmlPathResultContains**

**Description**: This function is used to validate that the value extracted from the XML response contains the specified text.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertXmlPathResultContains`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertXmlPathResultContains`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertXmlPathResultContains`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert XmlPath Result Contains ", input = InputType.YES)
    public void assertXmlPathResultContains() {
        try {
            DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
            DocumentBuilder dBuilder;
            InputSource inputSource = new InputSource();
            inputSource.setCharacterStream(new StringReader(responsebodies.get(key)));
            dBuilder = dbFactory.newDocumentBuilder();
            Document doc = dBuilder.parse(inputSource);
            doc.getDocumentElement().normalize();
            XPath xPath = XPathFactory.newInstance().newXPath();
            String expression = Data;
            NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
            Node nNode = nodeList.item(0);
            String value = nNode.getNodeValue();
            String inputValue = getInputValue(Input);
            if (value.contains(inputValue)) {
                Report.updateTestLog(Action, "Element text contains [" + inputValue + "] is as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text [" + value + "] does not contain [" + inputValue + "]",
                        Status.FAILNS);
            }
        } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                | SAXException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error validating XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **assertXmlPathResultNotContains**

**Description**: This function is used to validate that the value extracted from the XML does not contain the specified text.

**Input Format** : @Text that should NOT be present

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertXmlPathResultNotContains`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertXmlPathResultNotContains`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertXmlPathResultNotContains`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert XmlPath Result Not Contains ", input = InputType.YES)
    public void assertXmlPathResultNotContains() {
        try {
            DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
            DocumentBuilder dBuilder;
            InputSource inputSource = new InputSource();
            inputSource.setCharacterStream(new StringReader(responsebodies.get(key)));
            dBuilder = dbFactory.newDocumentBuilder();
            Document doc = dBuilder.parse(inputSource);
            doc.getDocumentElement().normalize();
            XPath xPath = XPathFactory.newInstance().newXPath();
            String expression = Data;
            NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
            Node nNode = nodeList.item(0);
            String value = nNode.getNodeValue();
            if (!value.contains(Input)) {
                Report.updateTestLog(Action, "Element text [" + value + "] does not contain [" + Input + "] as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text [" + value + "] contains [" + Input + "] but should not",
                        Status.FAILNS);
            }
        } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                | SAXException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error validating XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **assertXmlPathResultEquals**

**Description**: This function is used to validate that the value extracted from the XML response exactly matches the expected text.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertXmlPathResultEquals`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertXmlPathResultEquals`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertXmlPathResultEquals`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert XmlPath Result Equals ", input = InputType.YES)
    public void assertXmlPathResultEquals() {
        try {
            DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
            DocumentBuilder dBuilder;
            InputSource inputSource = new InputSource();
            inputSource.setCharacterStream(new StringReader(responsebodies.get(key)));
            dBuilder = dbFactory.newDocumentBuilder();
            Document doc = dBuilder.parse(inputSource);
            doc.getDocumentElement().normalize();
            XPath xPath = XPathFactory.newInstance().newXPath();
            String expression = Data;
            NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
            Node nNode = nodeList.item(0);
            String value = nNode.getNodeValue();
            String inputValue = getInputValue(Input);
            if (value.equals(inputValue)) {
                Report.updateTestLog(Action, "Element text [" + value + "] is as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text [" + value + "] is not as expected. " + Data, Status.FAILNS);
            }
        } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                | SAXException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error validating XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **assertXmlPathResultNotEquals**

**Description**: This function is used to validate that the value extracted from the XML response does not exactly match the specified expected text.

**Input Format** : @Text that should NOT be present

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`assertXmlPathResultNotEquals`](#)   | @value       | | PageName |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | structuredData Object |:green_circle: [`assertXmlPathResultNotEquals`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | structuredData Object |:green_circle: [`assertXmlPathResultNotEquals`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Assert XmlPath Result Not Equals ", input = InputType.YES)
    public void assertXmlPathResultNotEquals() {
        try {
            DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
            DocumentBuilder dBuilder;
            InputSource inputSource = new InputSource();
            inputSource.setCharacterStream(new StringReader(responsebodies.get(key)));
            dBuilder = dbFactory.newDocumentBuilder();
            Document doc = dBuilder.parse(inputSource);
            doc.getDocumentElement().normalize();
            XPath xPath = XPathFactory.newInstance().newXPath();
            String expression = Data;
            NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
            Node nNode = nodeList.item(0);
            String value = nNode.getNodeValue();
            String inputValue = getInputValue(Input);
            if (!value.equals(inputValue)) {
                Report.updateTestLog(Action, "Element text [" + value + "] is not equal to [" + inputValue + "] as expected", Status.PASSNS);
            } else {
                Report.updateTestLog(Action, "Element text [" + value + "] should not be equal to [" + inputValue + "]", Status.FAILNS);
            }
        } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                | SAXException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error validating XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **storeXmlPathResultInVariable**

**Description**: This function is used to extract a value from the XML response and store it in a variable.

**Input Format** : %variableName%

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`storeXmlPathResultInVariable`](#)   | %dynamicVar% | | PageName |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Store XmlPath Result", input = InputType.YES)
    public void storeXmlPathResultInVariable() {
        try {
            String variableName = Input;
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
------------------------------------------

## **storeXmlPathResultInDataSheet**

**Description**: This function is used to extract a value from the XML response and store it in a datasheet.

**Input Format** : Sheet:Column

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | structuredData Object |:green_circle: [`storeXmlPathResultInDataSheet`](#)   | Sheet:Column | | PageName |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.STRUCTUREDDATA, desc = "Store XmlPath Result In DataSheet ", input = InputType.YES)
    public void storeXmlPathResultInDataSheet() {
        try {
            String strObj = Input;
            if (strObj.matches(".*:.*")) {
                try {
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
                    String expression = Data;
                    NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
                    Node nNode = nodeList.item(0);
                    String value = nNode.getNodeValue();
                    userData.putData(sheetName, columnName, value);
                    Report.updateTestLog(Action, "Element text [" + value + "] is stored in " + strObj, Status.DONE);
                } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                        | SAXException ex) {
                    Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
                    Report.updateTestLog(Action, "Error Storing XML element in datasheet :" + "\n" + ex.getMessage(),
                            Status.DEBUG);
                }
            } else {
                Report.updateTestLog(Action,
                        "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
                        Status.DEBUG);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error Storing XML element in datasheet :" + "\n" + ex.getMessage(),
                    Status.DEBUG);
        }
    }
    ```
------------------------------------------