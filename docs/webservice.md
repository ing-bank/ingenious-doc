# API Testing Actions

## **setEndPoint**

**Description**: This function is used to set the End Point for a Rest/SOAP API. 

**Input Format** : @EndPoint

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*setEndPoint*   | @Endpoint (from Editor)      |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*setEndPoint*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*setEndPoint*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded`, passed inside the **Endpoint editor** which is capable of parameterising the Endpoint (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

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

## **addHeader**

**Description**:  This function is used to add a header for a Rest/SOAP API request.

**Input Format** : @`HeaderName`=`HeaderValue`

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*addHeader*   | @`HeaderName`=`HeaderValue`      |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*addHeader*   | Sheet:Column containing `HeaderName`=`HeaderValue`|       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*addHeader*   | %dynamicVar% containing `HeaderName`=`HeaderValue` |       | |<span style="color:Brown"><<*Input from variable*</span>
| Webservice     |*addHeader*   | @`HeaderName`=`{SheetName:ColumnName}` |       | |<span style="color:Brown"><<*Input from variable*</span>
| Webservice     |*addHeader*   | @`HeaderName`=`%dynamicVar%` |       | |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action          | Input                       | Condition |Reference|
|------------|-----------------|-----------------------------|-----------|---------|
| Webservice | addURLParam|@key=value                             |           |         |

**Corresponding Code:**

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

## **closeConnection**

**Description**: This function is used to close a connection for a Rest/SOAP API request.

**Usage:**

| ObjectName | Action          | Input                       | Condition |Reference|
|------------|-----------------|-----------------------------|-----------|---------|
| Webservice |*closeConnection* |                             |           |         |

**Corresponding Code:**

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

## **storeResponseBodyInDataSheet**

**Description**: This function is used to store the response body of SOAP/REST request, into a respective column of a given datasheet.

**Input Format** : @Expected **DatasheetName:ColumnName**

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*storeResponseBodyInDataSheet*   | Sheet:Column      |      | |<span style="color:Blue"><< *Datasheet to where value is supposed br stored*</span> 

Note: Ensure that your data sheet doesn't contain column names with spaces. 

**Corresponding Code:**

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


## **assertResponseCode**

**Description**: This function is used to validate the response code of SOAP/REST response.

**Input Format** : @Expected code

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*assertResponseCode*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*assertResponseCode*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*assertResponseCode*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*assertResponsebodycontains*   | @value       |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*assertResponsebodycontains*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*assertResponsebodycontains*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

## **postSoapRequest**

**Description**: This function is used to perform POST action on a SOAP API.

**Input Format** : @Expected Payload

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*postRestRequest*   | @Payload (from Editor)      |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*postRestRequest*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*postRestRequest*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded`, passed inside the **XML editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

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

## **storeXMLelement**

**Description**: This function is used to store a certain XML tag value inside the response body of SOAP request, into a variable.

**Input Format** : @`XPath` of the tag

**Condition Format**: %variable%

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*storeXMLelement*   | @`XPath`       |  %var%     | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*storeXMLelement*   | **Sheet:Column** containing `XPath`  |%var%| |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*storeXMLelement*   | %Var% containing `XPath` |%var%| |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*storeXMLelementInDataSheet*   | Sheet:Column      |  XPath     | |<span style="color:Blue"><< *Datasheet to where value is supposed br stored*</span> 

Note: Ensure that your data sheet doesn't contain column names with spaces. 

**Corresponding Code:**

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

## **assertXMLelementEquals**

**Description**: This function is used to validate whether a certain XML tag of the response body of SOAP request equals an expected text or not.

**Input Format** : @Expected Text

**Condition Format**: XPath of the tag

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*assertXMLelementEquals*   | @value       |  XPath     | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*assertXMLelementEquals*   | Sheet:Column |XPath| |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*assertXMLelementEquals*   | %dynamicVar% |XPath| |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*assertXMLelementContains*   | @value       |  XPath     | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*assertXMLelementContains*   | Sheet:Column |XPath| |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*assertXMLelementContains*   | %dynamicVar% |XPath| |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

## **postRestRequest**

**Description**: This function is used to perform POST action on a Rest API.

**Input Format** : @Expected Payload

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*postRestRequest*   | @Payload (from Editor)      |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*postRestRequest*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*postRestRequest*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded`, passed inside the **JSON editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*putRestRequest*   | @Payload (from Editor)      |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*putRestRequest*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*putRestRequest*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded`, passed inside the **JSON editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*patchRestRequest*   | @Payload (from Editor)      |       | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*patchRestRequest*   | Sheet:Column |       | |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*patchRestRequest*   | %dynamicVar% |       | |<span style="color:Brown"><<*Input from variable*</span>

Inputs in the Input column can be either `hardcoded`, passed inside the **XML editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action          | Input                       | Condition |Reference|
|------------|-----------------|-----------------------------|-----------|---------|
| Webservice |*getRestRequest* |                             |           |         |

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action          | Input                       | Condition |Reference|
|------------|-----------------|-----------------------------|-----------|---------|
| Webservice |*deleteRestRequest* |                             |           |         |

**Corresponding Code:**

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

## **storeJSONelement**

**Description**: This function is used to store a certain JSON tag value from the response body of REST request, into a variable.

**Input Format** : @`JSONPath` of the tag

**Condition Format**: %variable%

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*storeJSONelement*   | @`JSONPath`       |  %var%     | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*storeJSONelement*   | **Sheet:Column** containing `JSONPath`  |%var%| |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*storeJSONelement*   | %Var% containing `JSONPath` |%var%| |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*storeJSONelementInDataSheet*   | Sheet:Column      |  JSONPath     | |<span style="color:Blue"><< *Datasheet to where value is supposed br stored*</span> 

Note: Ensure that your data sheet doesn't contain column names with spaces. 

**Corresponding Code:**

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

## **assertJSONelementEquals**

**Description**:  This function is used to validate whether a certain JSON tag of the response body of REST request equals an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : JSON Path of the tag

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*assertJSONelementEquals*   | @value       |  JSONPath     | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*assertJSONelementEquals*   | Sheet:Column |JSONPath| |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*assertJSONelementEquals*   | %dynamicVar% |JSONPath| |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*assertJSONelementContains*   | @value       |  JSONPath     | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*assertJSONelementContains*   | Sheet:Column |JSONPath| |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*assertJSONelementContains*   | %dynamicVar% |JSONPath| |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

## **storeJsonElementCount**

**Description**: This function is used to store the count of JSON elements for a given JSON Path of REST request, into a variable.

**Input Format** : @`JSONPath` of the tag

**Condition Format**: %variable%

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*storeJsonElementCount*   | @`JSONPath`       |  %var%     | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*storeJsonElementCount*   | **Sheet:Column** containing `JSONPath`  |%var%| |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*storeJsonElementCount*   | %Var% containing `JSONPath` |%var%| |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*storeJsonElementCountInDataSheet*   | Sheet:Column      |  JSONPath     | |<span style="color:Blue"><< *Datasheet to where value is supposed br stored*</span> 

Note: Ensure that your data sheet doesn't contain column names with spaces. 

**Corresponding Code:**

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

## **assertJSONelementCount**

**Description**:  This function is used to validate whether the count of JSON elements for a given JSON Path of REST request contains an expected value or not.

**Input Format** : @Expected Value

**Condition Format** : JSON Path of the tag

**Usage:**

| ObjectName | Action | Input        | Condition |Reference|  |
|------------|--------|--------------|-----------|---------|--|
| Webservice     |*assertJSONelementCount*   | @value       |  JSONPath     | |<span style="color:Green"><< *Hardcoded Input*</span> 
| Webservice     |*assertJSONelementCount*   | Sheet:Column |JSONPath| |<span style="color:Blue"><< *Input from Datasheet*</span>
| Webservice     |*assertJSONelementCount*   | %dynamicVar% |JSONPath| |<span style="color:Brown"><<*Input from variable*</span>

**Corresponding Code:**

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





