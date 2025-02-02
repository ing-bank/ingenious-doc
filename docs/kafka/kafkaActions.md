# **Kafka Operations**
------------------------

## **setBootstrapServers**

**Description**: This function is used to set the bootstrap servers for establishing the kafka connection.

**Input Format** : @Expected server details

=== "Usage"

    | ObjectName | Action   | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setBootstrapServers`](#)   | @value       |        | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setBootstrapServers`](#)   | Sheet:Column |        | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setBootstrapServers`](#)   | %dynamicVar% |        | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Bootstrap Servers", input = InputType.YES, condition = InputType.NO)
    public void setBootstrapServers() {
        try {
            kafkaServers.put(key, Data);
            Report.updateTestLog(Action, "Bootstrap Servers have been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Bootstrap Servers setup", ex);
            Report.updateTestLog(Action, "Error in setting Bootstrap Servers: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```

----------------------


## **setProducerTopic**

**Description**: This function is used to set the Producer Topic name

**Input Format** : @Expected Producer Topic Name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setProducerTopic`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setProducerTopic`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setProducerTopic`](#) | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Producer Topic", input = InputType.YES, condition = InputType.NO)
    public void setProducerTopic() {
        try {
            kafkaProducerTopic.put(key, Data);
            Report.updateTestLog(Action, "Topic has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Topic setup", ex);
            Report.updateTestLog(Action, "Error in setting Topic: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```

----------------------



## **setKey**

**Description**: This function is used to set the key for the Kafka connection.

**Input Format** : @Expected Key

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setKey`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setKey`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setKey`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Key", input = InputType.YES, condition = InputType.NO)
    public void setKey() {
        try {
            kafkaKey.put(key, Data);
            Report.updateTestLog(Action, "Key has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Key setup", ex);
            Report.updateTestLog(Action, "Error in setting Key: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
----------------------------------------

## **setKeySerializer**

**Description**: This function is used to set the Key Serializer for the Kafka Producer.

**Input Format** : @Expected Key Serializer. Expected values are : `string` / `bytearray` / `avro`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setKeySerializer`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setKeySerializer`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setKeySerializer`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Key Serializer", input = InputType.YES, condition = InputType.NO)
    public void setKeySerializer() {
        try {
            kafkaKeySerializer.put(key, Data);
            Report.updateTestLog(Action, "Key Serializer has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Key Serializer setup", ex);
            Report.updateTestLog(Action, "Error in setting Key Serializer: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
----------------------------------------

## **setValueSerializer**

**Description**: This function is used to set the Value Serializer for the Kafka Producer.

**Input Format** : @Expected Value Serializer. Expected values are : `string` / `bytearray` / `avro`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setValueSerializer`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setValueSerializer`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setValueSerializer`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Value Serializer", input = InputType.YES, condition = InputType.NO)
    public void setValueSerializer() {
        try {
            kafkaValueSerializer.put(key, Data);
            Report.updateTestLog(Action, "Value Serializer has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Value Serializer setup", ex);
            Report.updateTestLog(Action, "Error in setting Value Serializer: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
----------------------------------------

## **setSchemaRegistryURL**

**Description**: This function is used to set the Schema Registry URL (mostly used when firing `Avro` serialized value).

**Input Format** : @Expected Schema Registry URL

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setSchemaRegistryURL`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setSchemaRegistryURL`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setSchemaRegistryURL`](#)   | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Schema Registry URL", input = InputType.YES, condition = InputType.NO)
    public void setSchemaRegistryURL() {
        try {
            kafkaSchemaRegistryURL.put(key, Data);
            Report.updateTestLog(Action, "Schema Registry URL has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Schema Registry URL setup", ex);
            Report.updateTestLog(Action, "Error in setting Schema Registry URL: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
-------------------------------

## **setPartition**

**Description**: This function is used to set the Partition for the Kafka Producer.

**Input Format** : @Expected Partition value. Either set an `Integer` or just set `null`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setPartition`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setPartition`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setPartition`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Partition", input = InputType.YES, condition = InputType.NO)
    public void setPartition() {
        try {
            if (Data.toLowerCase().equals("null")) {
                kafkaPartition.put(key, null);
            } else {
                kafkaPartition.put(key, Integer.valueOf(Data));
            }
            Report.updateTestLog(Action, "Partition has been set successfully", Status.DONE);
        } catch (NumberFormatException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Partition setup", ex);
            Report.updateTestLog(Action, "Error in setting Partition: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }   
    ```

---------------------------------

## **setTimeStamp**

**Description**: This function is used to set the Time Stamp for the Kafka Producer. This sets the `System.currentTimeMillis()` to the producer record.


=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setTimeStamp`](#)   |        |       | |


=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set TimeStamp", input = InputType.NO, condition = InputType.NO)
    public void setTimeStamp() {
        try {
            kafkaTimeStamp.put(key, System.currentTimeMillis());
            Report.updateTestLog(Action, "Time Stamp has been set successfully", Status.DONE);
        } catch (NumberFormatException ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Time Stamp setup", ex);
            Report.updateTestLog(Action, "Error in setting Time Stamp: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
------------------------------------------

## **addKafkaHeader**

**Description**: This function is used to add a header to the Kafka Producer Record.

**Input Format** : @`HeaderName`=`HeaderValue`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`addHeader`](#)   | @`HeaderName`=`HeaderValue`      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`addHeader`](#)    | `Sheet:Column` containing `HeaderName`=`HeaderValue`|       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`addHeader`](#)    | %dynamicVar% containing `HeaderName`=`HeaderValue` |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Kafka     |:green_circle: [`addHeader`](#)    | @`HeaderName`=`{SheetName:ColumnName}` |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>
    | Kafka     |:green_circle: [`addHeader`](#)    | @`HeaderName`=`%dynamicVar%` |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    This function adds all the **Headers** into a HashMap `headerlist`. Then those are applied to the request as :

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Add Kafka Header", input = InputType.YES)
    public void addKafkaHeader() {
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
            String headerKey = Data.split("=", 2)[0];
            String headerValue = Data.split("=", 2)[1];

            if (kafkaHeaders.containsKey(key)) {
                kafkaHeaders.get(key).add(new RecordHeader(headerKey, headerValue.getBytes()));
            } else {
                ArrayList<Header> toBeAdded = new ArrayList<Header>();
                toBeAdded.add(new RecordHeader(headerKey, headerValue.getBytes()));
                kafkaHeaders.put(key, toBeAdded);
            }

            Report.updateTestLog(Action, "Header added " + Data, Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error adding Header :" + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }

    ```
----------------------





## **produceMessage**

**Description**: This function is used to Produce the Kafka Producer Record.

**Input Format** : @Expected Payload

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`produceMessage`](#)   | @Payload (from Editor)      |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`produceMessage`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`produceMessage`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

    Inputs in the Input column can be either `hardcoded`, passed inside the **Payload editor** which is capable of parameterising the Payload (Press ctrl+space to see the list of variables available ), passed from the data sheet (`datasheet name : column name`) or passed from a variable value (`%variable name%`), as given in the above example.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Produce Kafka Message", input = InputType.YES, condition = InputType.NO)
    public void produceMessage() {
        try {
            String value = Data;
            value = handleDataSheetVariables(value);
            value = handleuserDefinedVariables(value);
            kafkaValue.put(key, value);

            if (kafkaHeaders.get(key) != null && kafkaTimeStamp.get(key) != null) {
                produceMessage(kafkaProducerTopic.get(key), kafkaPartition.get(key), kafkaTimeStamp.get(key), kafkaKey.get(key), kafkaValue.get(key), kafkaHeaders.get(key));
            } else if (kafkaHeaders.get(key) != null) {
                produceMessage(kafkaProducerTopic.get(key), kafkaPartition.get(key), kafkaKey.get(key), kafkaValue.get(key), kafkaHeaders.get(key));
            } else if (kafkaTimeStamp.get(key) != null) {
                produceMessage(kafkaProducerTopic.get(key), kafkaPartition.get(key), kafkaTimeStamp.get(key), kafkaKey.get(key), kafkaValue.get(key));
            } else if (kafkaPartition.containsKey(key)) {
                produceMessage(kafkaProducerTopic.get(key), kafkaPartition.get(key), kafkaKey.get(key), kafkaValue.get(key));
            } else if (kafkaKey.get(key) != null) {
                produceMessage(kafkaProducerTopic.get(key), kafkaKey.get(key), kafkaValue.get(key));
            } else {
                produceMessage(kafkaProducerTopic.get(key), kafkaValue.get(key));
            }

            Report.updateTestLog(Action, "Message has been produced. ", Status.DONE);

        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Something went wrong in producing the message" + "\n" + ex.getMessage(),
                    Status.FAILNS);
            ex.printStackTrace();
        }
    }
    ```


-----------------------------

## **sendKafkaMessage**

**Description**: This function is used to send the Kafka Record to the Producer Topic.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Queue |:green_circle: [`sendKafkaMessage`](#) |                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Send Message", input = InputType.NO, condition = InputType.NO)
    public void sendKafkaMessage() {
        try {
            createProducer(kafkaValueSerializer.get(key));
            //before.put(key, Instant.now());
            kafkaProducer.get(key).send(kafkaProducerRecord.get(key));
            Report.updateTestLog(Action, "Record sent", Status.DONE);
            kafkaProducer.get(key).close();
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception while sending record", ex);
            Report.updateTestLog(Action, "Error in sending record: " + "\n" + ex.getMessage(), Status.DEBUG);
        } finally {
            clearProducerDetails();
        }
    }
    ```
------------------------------------------

## **setConsumerTopic**

**Description**: This function is used to set the Consumer Topic name

**Input Format** : @Expected Consumer Topic Name

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setConsumerTopic`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setConsumerTopic`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setConsumerTopic`](#) | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Consumer Topic", input = InputType.YES, condition = InputType.NO)
    public void setConsumerTopic() {
        try {
            kafkaConsumerTopic.put(key, Data);
            Report.updateTestLog(Action, "Topic has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Topic setup", ex);
            Report.updateTestLog(Action, "Error in setting Topic: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```

----------------------

## **setConsumerPollRetries**

**Description**: This function is used to set the the number of times the Kafka Consumer will retry the polling of the target record.

**Input Format** : @Expected number of retries

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setConsumerPollRetries`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setConsumerPollRetries`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setConsumerPollRetries`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Consumer Retries", input = InputType.YES, condition = InputType.NO)
    public void setConsumerPollRetries() {
        try {
            kafkaConsumerPollRetries.put(key, Integer.parseInt(Data));
            Report.updateTestLog(Action, "Poll Retries has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Poll Retries setup", ex);
            Report.updateTestLog(Action, "Error in setting Poll Retries: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```

----------------------

## **setConsumerPollInterval**

**Description**: This function is used to set the interval (in milliseconds) in which the Kafka Consumer will retry the polling of the target record.

**Input Format** : @Expected interval value (in milliseconds)

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     | :green_circle: [`setConsumerPollInterval`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setConsumerPollInterval`](#)   | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     | :green_circle: [`setConsumerPollInterval`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Consumer Retries", input = InputType.YES, condition = InputType.NO)
    public void setConsumerPollInterval() {
        try {
            kafkaConsumerPollDuration.put(key, Long.valueOf(Data));
            Report.updateTestLog(Action, "Poll interval has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Poll interval setup", ex);
            Report.updateTestLog(Action, "Error in setting Poll interval: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
----------------------

## **setConsumerGroupId**

**Description**: This function is used to set the Group Id for the Kafka Consumer.

**Input Format** : @Expected Group Id

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setConsumerGroupId`](#)   | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     | :green_circle: [`setConsumerGroupId`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     | :green_circle: [`setConsumerGroupId`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Consumer GroupId", input = InputType.YES, condition = InputType.NO)
    public void setConsumerGroupId() {
        try {
            kafkaConsumerGroupId.put(key, Data);
            Report.updateTestLog(Action, "Consumer GroupId has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Consumer GroupId setup", ex);
            Report.updateTestLog(Action, "Error in setting Consumer GroupId: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```
----------------------

## **setValueDeserializer**

**Description**: This function is used to set the Value Deserializer for the Kafka Consumer.

**Input Format** : @Expected Value Deserializer. Expected values are : `string` / `bytearray` / `avro`

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`setValueDeserializer`](#)  | @value       |       | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`setValueDeserializer`](#)  | Sheet:Column |       | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`setValueDeserializer`](#)  | %dynamicVar% |       | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Set Value Deserializer", input = InputType.YES, condition = InputType.NO)
    public void setValueDeserializer() {
        try {
            kafkaValueDeserializer.put(key, Data);
            Report.updateTestLog(Action, "Value Deserializer has been set successfully", Status.DONE);
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.SEVERE, "Exception during Value Deserializer setup", ex);
            Report.updateTestLog(Action, "Error in setting Value Deserializer: " + "\n" + ex.getMessage(), Status.DEBUG);
        }
    }
    ```

----------------------

## **consumeKafkaMessage**

**Description**: This function is used to consume the Kafka Consumer Record.

=== "Usage"

    | ObjectName | Action          | Input                       | Condition |Reference|
    |------------|-----------------|-----------------------------|-----------|---------|
    | Queue |:green_circle: [`consumeKafkaMessage`](#)|                             |           |         |

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Consume Kafka Message", input = InputType.NO)
    public void consumeKafkaMessage() {

        createConsumer(kafkaValueDeserializer.get(key));
        kafkaConsumer.get(key).subscribe(Arrays.asList(kafkaConsumerTopic.get(key)));
        try {
            ConsumerRecord record = pollKafkaConsumer();
            if (record != null) {
                Report.updateTestLog(Action, "Kafka message consumed successfully. ", Status.DONE);
            } else {
                Report.updateTestLog(Action, "Kafka message not received. ", Status.FAIL);
            }
        } catch (Exception e) {
            e.printStackTrace();
            Report.updateTestLog(Action, "Error while consuming Kafka message: " + e.getMessage(), Status.FAIL);
        } finally {
            kafkaConsumer.get(key).close();
        }
    }
    ```

---------------------------------

## **storeKafkaXMLtagInDataSheet**

**Description**: This function is used to store a certain XML tag value into a respective column of a given datasheet.

**Input Format** : @Expected datasheet name:column name

**Condition Format**: XPath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`storeKafkaXMLtagInDataSheet`](#)   | Sheet:Column      |  XPath     | |<span style="color:Blue">:arrow_left: *Datasheet to where value is supposed br stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces. 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Store XML tag In DataSheet ", input = InputType.YES, condition = InputType.NO)
    public void storeKafkaXMLtagInDataSheet() {

        try {
            String strObj = Input;
            if (strObj.matches(".*:.*")) {
                try {
                    System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                    String sheetName = strObj.split(":", 2)[0];
                    String columnName = strObj.split(":", 2)[1];
                    String xmlText = kafkaConsumerRecord.get(key).value().toString();
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

## **assertKafkaXMLtagEquals**

**Description**:  This function is used to validate whether a certain XML tag equals an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : XPath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`assertKafkaXMLtagEquals`](#)   | @value       |  XPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`assertKafkaXMLtagEquals`](#)  | Sheet:Column |XPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`assertKafkaXMLtagEquals`](#)  | %dynamicVar% |XPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Assert XML Tag Equals ", input = InputType.YES, condition = InputType.YES)
    public void assertKafkaXMLtagEquals() {

        try {
            DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
            DocumentBuilder dBuilder;
            InputSource inputSource = new InputSource();
            inputSource.setCharacterStream(new StringReader(kafkaConsumerRecord.get(key).value().toString()));
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

## **assertKafkaXMLtagContains**

**Description**:  This function is used to validate whether a certain XML tag contains an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : XPath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`assertKafkaXMLtagContains`](#)   | @value       |  XPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`assertKafkaXMLtagContains`](#)  | Sheet:Column |XPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`assertKafkaXMLtagContains`](#)  | %dynamicVar% |XPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Assert XML Tag Contains ", input = InputType.YES, condition = InputType.YES)
    public void assertKafkaXMLtagContains() {

        try {
            DocumentBuilderFactory dbFactory = DocumentBuilderFactory.newInstance();
            DocumentBuilder dBuilder;
            InputSource inputSource = new InputSource();
            inputSource.setCharacterStream(new StringReader(kafkaConsumerRecord.get(key).value().toString()));
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

## **storeKafkaResponseInDataSheet**

**Description**: This function is used to store the Kafka message into a respective column of a given datasheet.

**Input Format** : @Expected datasheet name:column name

**Condition Format**: XPath

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`storeKafkaResponseInDataSheet`](#)   | Sheet:Column      |  XPath     | |<span style="color:Blue">:arrow_left: *Datasheet to where value is supposed br stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces. 

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Store Response In DataSheet ", input = InputType.YES, condition = InputType.NO)
    public void storeKafkaResponseInDataSheet() {

        try {
            String strObj = Input;
            if (strObj.matches(".*:.*")) {
                try {
                    System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                    String sheetName = strObj.split(":", 2)[0];
                    String columnName = strObj.split(":", 2)[1];
                    String response = kafkaConsumerRecord.get(key).value().toString();
                    userData.putData(sheetName, columnName, response);
                    Report.updateTestLog(Action, "Response is stored in " + strObj, Status.DONE);
                } catch (Exception ex) {
                    Logger.getLogger(this.getClass().getName()).log(Level.OFF, ex.getMessage(), ex);
                    Report.updateTestLog(Action, "Error storing Response in datasheet :" + "\n" + ex.getMessage(),
                            Status.DEBUG);
                }
            } else {
                Report.updateTestLog(Action,
                        "Given input [" + Input + "] format is invalid. It should be [sheetName:ColumnName]",
                        Status.DEBUG);
            }
        } catch (Exception ex) {
            Logger.getLogger(this.getClass().getName()).log(Level.OFF, null, ex);
            Report.updateTestLog(Action, "Error storing Response in datasheet :" + "\n" + ex.getMessage(),
                    Status.DEBUG);
        }
    }
    ```
----------------------



## **assertKafkaResponseMessageContains**

**Description**:  This function is used to validate whether Kafka message contains an expected text or not.

**Input Format** : @Expected Text

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`assertKafkaResponseMessageContains`](#)  | @value       |  | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`assertKafkaResponseMessageContains`](#)  | Sheet:Column |  | |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     | :green_circle: [`assertKafkaResponseMessageContains`](#)  | %dynamicVar% |  | |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Assert Response Message contains ", input = InputType.YES)
    public void assertKafkaResponseMessageContains() {
        try {
            if (kafkaConsumerRecord.get(key).value().toString().contains(Data)) {
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

## **assertKafkaJSONtagEquals**

**Description**:  This function is used to validate whether a certain JSON tag equals an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`assertKafkaJSONtagEquals`](#)  | @value       |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`assertKafkaJSONtagEquals`](#)  | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`assertKafkaJSONtagEquals`](#) | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Assert JSON Tag Equals ", input = InputType.YES, condition = InputType.YES)
    public void assertKafkaJSONtagEquals() {
        try {
            String response = kafkaConsumerRecord.get(key).value().toString();
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

## **assertKafkaJSONtagContains**

**Description**:  This function is used to validate whether a certain JSON tag contains an expected text or not.

**Input Format** : @Expected Text

**Condition Format** : JSON Path of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`assertKafkaJSONtagContains`](#)   | @value      |  JSONPath     | |<span style="color:#349651">:arrow_left:   *Hardcoded Input*</span> 
    | Kafka     |:green_circle: [`assertKafkaJSONtagContains`](#)  | Sheet:Column |JSONPath| |<span style="color:#559BD1">:arrow_left:   *Input from Datasheet*</span>
    | Kafka     |:green_circle: [`assertKafkaJSONtagContains`](#)  | %dynamicVar% |JSONPath| |<span style="color:#AB0066">:arrow_left:   *Input from variable*</span>

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Assert JSON Tag Contains ", input = InputType.YES, condition = InputType.YES)
    public void assertKafkaJSONtagContains() {
        try {
            String response = kafkaConsumerRecord.get(key).value().toString();
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

---------------------------------

## **storeKafkaJSONtagInDataSheet**

**Description**: This function is used to store a certain JSON tag value into a respective column of a given datasheet.

**Input Format** : @Expected datasheet name:column name

**Condition Format**: JSONPath of the tag

=== "Usage"

    | ObjectName | Action | Input        | Condition |Reference|  |
    |------------|--------|--------------|-----------|---------|--|
    | Kafka     |:green_circle: [`storeKafkaJSONtagInDataSheet`](#)   | Sheet:Column      |  JSONPath     | |<span style="color:Blue">:arrow_left: *Datasheet to where value is supposed br stored*</span> 

    Note: Ensure that your data sheet doesn't contain column names with spaces.

=== "Corresponding Code"

    ```java
    @Action(object = ObjectType.KAFKA, desc = "Store JSON Tag In DataSheet ", input = InputType.YES, condition = InputType.YES)
    public void storeKafkaJSONtagInDataSheet() {

        try {
            String strObj = Input;
            if (strObj.matches(".*:.*")) {
                try {
                    System.out.println("Updating value in SubIteration " + userData.getSubIteration());
                    String sheetName = strObj.split(":", 2)[0];
                    String columnName = strObj.split(":", 2)[1];
                    String response = kafkaConsumerRecord.get(key).value().toString();
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
