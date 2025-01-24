# Queue Operations
------------------------

## **setHost**

**Description**: This function is used to set the host for establishing the queue connection.

**Input Format** : @Expected host name

=== "Usage"

    | ObjectName | Action   | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setHost`](#)   | @value       |        | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setHost`](#)   | Sheet:Column |        | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setHost`](#)   | %dynamicVar% |        | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Host", input = InputType.YES, condition = InputType.NO)
        public void setHost() {
            try {
                jmsHost.put(key, Data);
                Report.updateTestLog(Action, "Queue Host has been set successfully", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting Host: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

----------------------


## **setPort**

**Description**: This function is used to set the port for establishing the queue connection.

**Input Format** : @Expected port name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setPort`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setPort`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setPort`](#) | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Port", input = InputType.YES, condition = InputType.NO)
        public void setPort() {
            try {
                jmsPort.put(key, Integer.valueOf(Data));
                Report.updateTestLog(Action, "Queue Port has been set successfully", Status.DONE);
            } catch (NumberFormatException ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting Port: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

----------------------

## **setChannel**

**Description**: This function is used to set the channel for establishing the queue connection.

**Input Format** : @Expected channel name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setChannel`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setChannel`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setChannel`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Channel", input = InputType.YES, condition = InputType.NO)
        public void setChannel() {
            try {
                jmsChannel.put(key, Data);
                Report.updateTestLog(Action, "Queue Channel has been set successfully", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting Channel: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------------------------

## **setQueueManager**

**Description**: This function is used to set the Queue Manager for the connection.

**Input Format** : @Expected Queue manager name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setQueueManager`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setQueueManager`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setQueueManager`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Queue Manager", input = InputType.YES, condition = InputType.NO)
        public void setQueueManager() {
            try {
                jmsQmgr.put(key, Data);
                Report.updateTestLog(Action, "Queue manager has been set successfully", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting Queue manager: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
-------------------------------

## **setUserName**

**Description**: This function is used to set the username for the queue connection.

**Input Format** : @Expected Username

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setUserName`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setUserName`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setUserName`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Username", input = InputType.YES, condition = InputType.NO)
        public void setUserName() {
            try {
                jmsUsername.put(key, Data);
                Report.updateTestLog(Action, "Username has been set successfully", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting Username: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

---------------------------------

## **setPassword**

**Description**: This function is used to set the password for the queue connection.

**Input Format** : @Expected Password value

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setPassword`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setPassword`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setPassword`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Password", input = InputType.YES, condition = InputType.NO)
        public void setPassword() {
            try {
                jmsPassword.put(key, Data);
                Report.updateTestLog(Action, "Password has been set successfully", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting Password: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
------------------------------------------

## **setSSLCipherSuite**

**Description**: This function is used to set the SSL Cipher Suite for the queue connection.

**Input Format** : @Expected SSL Cipher Suite

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setSSLCipherSuite`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     | :green_circle: [`setSSLCipherSuite`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setSSLCipherSuite`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set SSL Cipher Suite", input = InputType.YES, condition = InputType.NO)
        public void setSSLCipherSuite() {
            try {
                WMQ_SSL_CIPHER_SUITE.put(key, Data);
                Report.updateTestLog(Action, "SSL Cipher Suite has been set successfully", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting SSL Cipher Suite: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------

## **setRequestQueue**

**Description**: This function is used to set the Request Queue for the connection.

**Input Format** : @Expected Request Queue

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setRequestQueue`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setRequestQueue`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setRequestQueue`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Request Queue", input = InputType.YES, condition = InputType.NO)
        public void setRequestQueue() {
            try {
                if (Data.startsWith("queue:///"))
                    jmsReqQueueName.put(key, Data);
                else {
                    Data = "queue:///" + Data;
                    jmsReqQueueName.put(key, Data);
                }
                Report.updateTestLog(Action, "Request Queue has been set successfully", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting Request Queue: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

----------------------

## **setResponseQueue**

**Description**: This function is used to set Response Queue for the connection.

**Input Format** : @Expected ResponseQueue

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     | :green_circle: [`setResponseQueue`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setResponseQueue`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     | :green_circle: [`setResponseQueue`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Response Queue", input = InputType.YES, condition = InputType.NO)
        public void setResponseQueue() {
            try {
                if (Data.startsWith("queue:///"))
                    jmsRespQueueName.put(key, Data);
                else {
                    Data = "queue:///" + Data;
                    jmsRespQueueName.put(key, Data);
                }
                Report.updateTestLog(Action, "Response Queue has been set successfully", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during queue connection setup", ex);
                Report.updateTestLog(Action, "Error in setting Response Queue: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------
## **setCorrelationID**

**Description**: This function is used to set Correlation ID for the queue connection.

**Input Format** : @Expected CorrelationID

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setCorrelationID`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     | :green_circle: [`setCorrelationID`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     | :green_circle: [`setCorrelationID`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Correlation ID", input = InputType.YES, condition = InputType.NO)
        public void setCorrelationID() {
            try {
                jmsMessage.get(key).setJMSCorrelationID(Data);
                Report.updateTestLog(Action, "Correlation ID set", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during setting of Correlation ID", ex);
                Report.updateTestLog(Action, "Error in setting Correlation ID: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
----------------------

## **setMesssageID**

**Description**: This function is used to set the message ID for the queue connection.

**Input Format** : @Expected MessageID

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setMesssageID`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setMesssageID`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setMesssageID`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Message ID", input = InputType.YES, condition = InputType.NO)
        public void setMesssageID() {
            try {
                jmsMessage.get(key).setJMSMessageID(Data);
                Report.updateTestLog(Action, "Message ID set", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during setting of Message ID", ex);
                Report.updateTestLog(Action, "Error in setting Message ID: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

----------------------

## **setText**

**Description**: This function is used to set the text.

**Input Format** : @Expected Payload

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`setText`](#)   | @Payload (from Editor)      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`setText`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`setText`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded`, passed inside the **Payload editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Set Text", input = InputType.YES, condition = InputType.NO)
        public void setText() {
            try {
                createConnectionFactory();
                jmsDestination.put(key, jmsContext.get(key).createQueue(jmsReqQueueName.get(key)));
                jmsMessage.get(key).setText(handlePayloadorEndpoint(Data));
                Report.updateTestLog(Action, "Text set", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during setting of Text", ex);
                Report.updateTestLog(Action, "Error in setting Text: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```


-----------------------------

## **sendMessage**

**Description**: This function is used to send message.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Queue |:green_circle: [`sendMessage`](#) |                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Send Message", input = InputType.NO, condition = InputType.NO)
        public void sendMessage() {
            try {
                jmsProducer.put(key, jmsContext.get(key).createProducer());
                before.put(key, Instant.now());
                jmsProducer.get(key).send(jmsDestination.get(key), jmsMessage.get(key));
                Report.updateTestLog(Action, "Message sent", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception while sending message", ex);
                Report.updateTestLog(Action, "Error in sending message: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```
------------------------------------------

## **receiveMessageWithFilter**

**Description**: This function is used to receive message based on filter.

**Input Format** : @Expected filter

**Condition Format**: `timeout` in ms

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`receiveMessageWithFilter`](#)  | @value       |  `timeout` in ms     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`receiveMessageWithFilter`](#)   | Sheet:Column  |`timeout` in ms| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`receiveMessageWithFilter`](#)  | %dynamicVar%|`timeout` in ms| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Receive Message based on Filter", input = InputType.YES, condition = InputType.YES)
        public void receiveMessageWithFilter() {
            try {
                long timeout = Long.valueOf(Condition);
                jmsDestination.put(key, jmsContext.get(key).createQueue(jmsRespQueueName.get(key)));
                jmsConsumer.put(key, jmsContext.get(key).createConsumer(jmsDestination.get(key), Data));
                receivedMessage.put(key, jmsConsumer.get(key).receiveBody(String.class, timeout));
                after.put(key, Instant.now());
                duration.put(key, Duration.between(before.get(key), after.get(key)).toMillis());
                if (receivedMessage.get(key) != null) {
                    Report.updateTestLog(Action, "Message received in : [" + duration.get(key) + "ms]. Message body is : \n" + receivedMessage, Status.DONE);
                } else {
                    Report.updateTestLog(Action, "No Message received with filter " + Data, Status.DONE);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during receiving message", ex);
                Report.updateTestLog(Action, "Error in receiving message: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

----------------------

## **closeContext**

**Description**: This function is used to close the queue connection.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Queue |:green_circle: [`closeContext`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Close the connection", input = InputType.NO, condition = InputType.NO)
        public void closeContext() {
            try {
                jmsContext.get(key).close();
                Report.updateTestLog(Action, "Context closed", Status.DONE);
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during context closure", ex);
                Report.updateTestLog(Action, "Error while closing context: " + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

---------------------------------

## **storeXMLtagInDataSheet**

**Description**: This function is used to store a certain XML tag value into a respective column of a given datasheet.

**Input Format** : @Expected datasheet name:column name

**Condition Format**: XPath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`storeXMLtagInDataSheet`](#)   | Sheet:Column      |  XPath     | |<span style="color:Blue">:arrow_left: *Datasheet to where value is supposed br stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces. 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Store XML tag In DataSheet ", input = InputType.YES, condition = InputType.YES)
        public void storeXMLtagInDataSheet() {

            try {
                String strObj = Input;
                if (strObj.matches(".*:.*")) {
                    try {
                        System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                        String sheetName = strObj.split(":", 2)[0];
                        String columnName = strObj.split(":", 2)[1];
                        String xmlText = receivedMessage.get(key);
                        DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                        DocumentBuilder dBuilder;
                        InputSource inputSource = new InputSource();
                        inputSource.setCharacterStream(new StringReader(xmlText));
                        dBuilder = dbFactory.newDocumentBuilder();
                        Document doc = dBuilder.parse(inputSource);
                        doc.getDocumentElement().normalize();
                        XPath xPath = XPathFactory.newInstance().newXPath();
                        String expression = Condition;
                        String value = (String) xPath.compile(expression).evaluate(doc);
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
----------------------
## **assertXMLtagEquals**

**Description**:  This function is used to validate whether a certain XML tag equals an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : XPath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`assertXMLtagEquals`](#)   | @value       |  XPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`assertXMLtagEquals`](#)  | Sheet:Column |XPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`assertXMLtagEquals`](#)  | %dynamicVar% |XPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Assert XML Tag Equals ", input = InputType.YES, condition = InputType.YES)
        public void assertXMLtagEquals() {

            try {
                DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                DocumentBuilder dBuilder;
                InputSource inputSource = new InputSource();
                inputSource.setCharacterStream(new StringReader(receivedMessage.get(key)));
                dBuilder = dbFactory.newDocumentBuilder();
                Document doc = dBuilder.parse(inputSource);
                doc.getDocumentElement().normalize();
                XPath xPath = XPathFactory.newInstance().newXPath();
                String expression = Condition;
                String value = (String) xPath.compile(expression).evaluate(doc);
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

---------------------------------
## **assertXMLtagContains**

**Description**:  This function is used to validate whether a certain XML tag contains an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : XPath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`assertXMLtagContains`](#)   | @value       |  XPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`assertXMLtagContains`](#)  | Sheet:Column |XPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`assertXMLtagContains`](#)  | %dynamicVar% |XPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Assert XML Tag Contains ", input = InputType.YES, condition = InputType.YES)
        public void assertXMLtagContains() {

            try {
                DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
                DocumentBuilder dBuilder;
                InputSource inputSource = new InputSource();
                inputSource.setCharacterStream(new StringReader(receivedMessage.get(key)));
                dBuilder = dbFactory.newDocumentBuilder();
                Document doc = dBuilder.parse(inputSource);
                doc.getDocumentElement().normalize();
                XPath xPath = XPathFactory.newInstance().newXPath();
                String expression = Condition;
                String value = (String) xPath.compile(expression).evaluate(doc);
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

---------------------------------

## **assertResponseMessageContains**

**Description**:  This function is used to validate whether response message contains an expected text or not.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`assertResponseMessageContains`](#)  | @value       |  | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`assertResponseMessageContains`](#)  | Sheet:Column |  | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     | :green_circle: [`assertResponseMessageContains`](#)  | %dynamicVar% |  | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Assert Response Message contains ", input = InputType.YES)
        public void assertResponseMessageContains() {
            try {
                if (receivedMessage.get(key).contains(Data)) {
                    Report.updateTestLog(Action, "Response Message contains : " + Data, Status.PASSNS);
                } else {
                    Report.updateTestLog(Action, "Response Message does not contain : " + Data, Status.FAILNS);
                }
            } catch (Exception ex) {
                Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
                Report.updateTestLog(Action, "Error in validating response body :" + "\n" + ex.getMessage(), Status.DEBUG);
            }
        }
    ```

---------------------------------

## **assertJSONtagEquals**

**Description**:  This function is used to validate whether a certain JSON tag equals an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`assertJSONtagEquals`](#)  | @value       |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`assertJSONtagEquals`](#)  | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`assertJSONtagEquals`](#) | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Assert JSON Tag Equals ", input = InputType.YES, condition = InputType.YES)
        public void assertJSONtagEquals() {
            try {
                String response = receivedMessage.get(key);
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
## **assertJSONtagContains**

**Description**:  This function is used to validate whether a certain JSON tag contains an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`assertJSONtagContains`](#)   | @value       |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Queue     |:green_circle: [`assertJSONtagContains`](#)  | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Queue     |:green_circle: [`assertJSONtagContains`](#)  | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Assert JSON Tag Contains ", input = InputType.YES, condition = InputType.YES)
        public void assertJSONtagContains() {
            try {
                String response = receivedMessage.get(key);
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
        } }
        }
    ```

---------------------------------
## **storeJSONtagInDataSheet**

**Description**: This function is used to store a certain JSON tag value into a respective column of a given datasheet.

**Input Format** : @Expected datasheet name:column name

**Condition Format**: JSONPath of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Queue     |:green_circle: [`storeJSONtagInDataSheet`](#)   | Sheet:Column      |  JSONPath     | |<span style="color:Blue">:arrow_left: *Datasheet to where value is supposed br stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.QUEUE, desc = "Store JSON Tag In DataSheet ", input = InputType.YES, condition = InputType.YES)
        public void storeJSONtagInDataSheet() {

            try {
                String strObj = Input;
                if (strObj.matches(".*:.*")) {
                    try {
                        System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                        String sheetName = strObj.split(":", 2)[0];
                        String columnName = strObj.split(":", 2)[1];
                        String response = receivedMessage.get(key);
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

---------------------------------
