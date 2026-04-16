---
icon: material/flask-empty-minus-outline
---

# Negative Assertions

## **assertResponsebodyNotContains**

**Description**: This function is used to validate that the response body of SOAP/REST response does NOT contain a specified text.

**Input Format** : @Text that should NOT be present

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertResponsebodyNotContains`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertResponsebodyNotContains`](#)    | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertResponsebodyNotContains`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert Response Body Not Contains ", input = InputType.YES)
        public void assertResponsebodyNotContains() {
            try {
                if (!responsebodies.get(key).contains(Data)) {
                    Report.updateTestLog(Action, "Response body does not contain : " + Data + " as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Response body contains : " + Data + " but should not", Status.FAILNS);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error in validating response body :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------

## **assertXMLelementNotEquals**

**Description**: This function is used to validate that a certain XML tag of the response body of SOAP response does NOT equal a specified text.

**Input Format** : @Text that should NOT match

**Condition Format**: XPath of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertXMLelementNotEquals`](#)   | @value       |  XPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertXMLelementNotEquals`](#)   | Sheet:Column |XPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertXMLelementNotEquals`](#)   | %dynamicVar% |XPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert XML Element Not Equals ", input = InputType.YES, condition = InputType.YES)
        public void assertXMLelementNotEquals() {

            try {
                DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                DocumentBuilder dBuilder;
                InputSource inputSource = new InputSource();
                inputSource.setCharacterStream(new StringReader(responsebodies.get(key)));
                dBuilder = dbFactory.newDocumentBuilder();
                Document doc = dBuilder.parse(inputSource);
                doc.getDocumentElement().normalize();
                XPath xPath = XPathFactory.newInstance().newXPath();
                String expression = Condition;
                NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
                Node nNode = nodeList.item(0);
                String value = nNode.getNodeValue();
                if (!value.equals(Data)) {
                    Report.updateTestLog(Action, "Element text [" + value + "] is not equal to [" + Data + "] as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Element text [" + value + "] should not be equal to [" + Data + "]", Status.FAILNS);
                }
            } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                    | SAXException ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error validating XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
------------------------------------------

## **assertXMLelementNotContains**

**Description**: This function is used to validate that a certain XML tag of the response body of SOAP request does NOT contain a specified text.

**Input Format** : @Text that should NOT be present

**Condition Format**: XPath of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertXMLelementNotContains`](#)   | @value       |  XPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertXMLelementNotContains`](#)    | Sheet:Column |XPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertXMLelementNotContains`](#)    | %dynamicVar% |XPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert XML Element Not Contains ", input = InputType.YES, condition = InputType.YES)
        public void assertXMLelementNotContains() {

            try {
                DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                DocumentBuilder dBuilder;
                InputSource inputSource = new InputSource();
                inputSource.setCharacterStream(new StringReader(responsebodies.get(key)));
                dBuilder = dbFactory.newDocumentBuilder();
                Document doc = dBuilder.parse(inputSource);
                doc.getDocumentElement().normalize();
                XPath xPath = XPathFactory.newInstance().newXPath();
                String expression = Condition;
                NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(doc, XPathConstants.NODESET);
                Node nNode = nodeList.item(0);
                String value = nNode.getNodeValue();
                if (!value.contains(Data)) {
                    Report.updateTestLog(Action, "Element text [" + value + "] does not contain [" + Data + "] as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Element text [" + value + "] contains [" + Data + "] but should not",
                            Status.FAILNS);
                }
            } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                    | SAXException ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error validating XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------

## **assertJSONelementNotEquals**

**Description**:  This function is used to validate that a certain JSON tag of the response body of REST request does NOT equal a specified text.

**Input Format** : @Text that should NOT match

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertJSONelementNotEquals`](#)  | @value       |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertJSONelementNotEquals`](#)  | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertJSONelementNotEquals`](#)  | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert JSON Element Not Equals ", input = InputType.YES, condition = InputType.YES)
        public void assertJSONelementNotEquals() {
            try {
                String response = responsebodies.get(key);
                String jsonpath = Condition;
                String value = JsonPath.read(response, jsonpath).toString();
                if (!value.equals(Data)) {
                    Report.updateTestLog(Action, "Element text [" + value + "] is not equal to [" + Data + "] as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Element text is [" + value + "] but should not be equal to [" + Data + "]",
                            Status.FAILNS);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

---------------------------------

## **assertJSONelementNotContains**

**Description**:  This function is used to validate that a certain JSON tag of the response body of REST request does NOT contain a specified text.

**Input Format** : @Text that should NOT be present

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertJSONelementNotContains`](#)   | @value       |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertJSONelementNotContains`](#)   | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertJSONelementNotContains`](#)   | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded` (in this case the data is preceded by a "**@**"), passed from the datasheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert JSON Element Not Contains ", input = InputType.YES, condition = InputType.YES)
        public void assertJSONelementNotContains() {
            try {
                String response = responsebodies.get(key);
                String jsonpath = Condition;
                String value = JsonPath.read(response, jsonpath).toString();
                if (!value.contains(Data)) {
                    Report.updateTestLog(Action, "Element text [" + value + "] does not contain [" + Data + "] as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Element text [" + value + "] contains [" + Data + "] but should not",
                            Status.FAILNS);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

-----------------------------
