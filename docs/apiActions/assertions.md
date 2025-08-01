# Assertion Actions

## **assertResponseCode**

**Description**: This function is used to validate the response code of SOAP/REST response.

**Input Format** : @Expected code

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertResponseCode`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertResponseCode`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertResponseCode`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert Response Code ", input = InputType.YES)
        public void assertResponseCode() {
            try {
                if (responsecodes.get(key).equals(Data)) {
                    Report.updateTestLog(Action, "Status code is : " + Data, Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Status code is : " + responsecodes.get(key) + " but should be " + Data,
                            Status.FAILNS);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error in validating response code :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

----------------------


## **assertResponsebodycontains**

**Description**: This function is used to validate whether the response body of SOAP/REST request contains an expected text or not.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertResponsebodycontains`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertResponsebodycontains`](#)    | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertResponsebodycontains`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert Response Body contains ", input = InputType.YES)
        public void assertResponsebodycontains() {
            try {
                if (responsebodies.get(key).contains(Data)) {
                    Report.updateTestLog(Action, "Response body contains : " + Data, Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Response body does not contain : " + Data, Status.FAILNS);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error in validating response body :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------

## **assertXMLelementEquals**

**Description**: This function is used to validate whether a certain XML tag of the response body of SOAP request equals an expected text or not.

**Input Format** : @Expected Text

**Condition Format**: XPath of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertXMLelementEquals`](#)   | @value       |  XPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertXMLelementEquals`](#)   | Sheet:Column |XPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertXMLelementEquals`](#)   | %dynamicVar% |XPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert XML Element Equals ", input = InputType.YES, condition = InputType.YES)
        public void assertXMLelementEquals() {

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
                if (value.equals(Data)) {
                    Report.updateTestLog(Action, "Element text [" + value + "] is as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Element text [" + value + "] is not as expected", Status.FAILNS);
                }
            } catch (IOException | ParserConfigurationException | XPathExpressionException | DOMException
                    | SAXException ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error validating XML element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
------------------------------------------

## **assertXMLelementContains**

**Description**: This function is used to validate whether a certain XML tag of the response body of SOAP request contains an expected text or not.

**Input Format** : @Expected Text

**Condition Format**: XPath of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertXMLelementContains`](#)   | @value       |  XPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertXMLelementContains`](#)    | Sheet:Column |XPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertXMLelementContains`](#)    | %dynamicVar% |XPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert XML Element Contains ", input = InputType.YES, condition = InputType.YES)
        public void assertXMLelementContains() {

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
                if (value.contains(Data)) {
                    Report.updateTestLog(Action, "Element text contains [" + Data + "] is as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Element text [" + value + "] does not contain [" + Data + "]",
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

## **assertJSONelementEquals**

**Description**:  This function is used to validate whether a certain JSON tag of the response body of REST request equals an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertJSONelementEquals`](#)  | @value       |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertJSONelementEquals`](#)  | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertJSONelementEquals`](#)  | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert JSON Element Equals ", input = InputType.YES, condition = InputType.YES)
        public void assertJSONelementEquals() {
            try {
                String response = responsebodies.get(key);
                String jsonpath = Condition;
                String value = JsonPath.read(response, jsonpath).toString();
                if (value.equals(Data)) {
                    Report.updateTestLog(Action, "Element text [" + value + "] is as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Element text is [" + value + "] but is expected to be [" + Data + "]",
                            Status.FAILNS);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

---------------------------------

## **assertJSONelementContains**

**Description**:  This function is used to validate whether a certain JSON tag of the response body of REST request contains an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertJSONelementContains`](#)   | @value       |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertJSONelementContains`](#)   | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertJSONelementContains`](#)   | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert JSON Element Contains ", input = InputType.YES, condition = InputType.YES)
        public void assertJSONelementContains() {
            try {
                String response = responsebodies.get(key);
                String jsonpath = Condition;
                String value = JsonPath.read(response, jsonpath).toString();
                if (value.contains(Data)) {
                    Report.updateTestLog(Action, "Element text contains [" + Data + "] is as expected", Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Element text [" + value + "] does not contain [" + Data + "]",
                            Status.FAILNS);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error in validating JSON element :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

-----------------------------

## **assertJSONelementCount**

**Description**:  This function is used to validate whether the count of JSON elements for a given JSON Path of REST request contains an expected value or not.

**Input Format** : @Expected Value

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Webservice     |:green_circle: [`assertJSONelementCount`](#)   | @value       |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Webservice     |:green_circle: [`assertJSONelementCount`](#)    | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Webservice     |:green_circle: [`assertJSONelementCount`](#)    | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.WEBSERVICE, desc = "Assert JSON Element Count ", input = InputType.YES, condition = InputType.YES)
        public void assertJSONelementCount() {

            try {
                String response = responsebodies.get(key);
                int actualObjectCount = 0;
                JSONParser parser = new JSONParser();
                JSONObject json = (JSONObject) parser.parse(response);
                try {
                    Map<String, String> objectMap = JsonPath.read(json, Condition);
                    actualObjectCount = objectMap.keySet().size();
                } catch (Exception ex) {
                    try {
                        JSONArray objectMap = JsonPath.read(json, Condition);
                        actualObjectCount = objectMap.size();
                    } catch (Exception ex1) {
                        try {
                            net.minidev.json.JSONArray objectMap = JsonPath.read(json, Condition);
                            actualObjectCount = objectMap.size();
                        } catch (Exception ex2) {
                            String objectMap = JsonPath.read(json, Condition);
                            actualObjectCount = 1;
                        }
                    }
                }

                int expectedObjectCount = Integer.parseInt(Data);
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
----------------------