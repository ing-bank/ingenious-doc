# **Working with Kafka**

## How to create a Kafka - based Test Case?

=== "v4.0.0 and up"

    <span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">4.0.0</span></span>
    Kafka connectivity is defined once per **named configuration** — not per test step — and referenced
    from a step using the `#alias` syntax. See [Kafka Configurations](#kafka-configurations) below.

    * Create a **Producer** and a **Consumer** alias under **Settings** :material-arrow-right: **Kafka Configurations**.

    * Then there should be steps to create the **`message`**. You can leverage built-in capabilities in INGenious like `Synthetic Data Generation` to create `UUID`s and other data to be fed into the message.

    * The **`produceMessage`** action comes with an editor which makes parameterization of data in the payload very easy. This action is always marked in <span style="color:Green">**Green.**</span> [See the section below]. Put the producer alias (e.g. `#OrdersProducer`) in the **Condition** column.

    * Then there should be the **`sendKafkaMessage`** action to push the message to the producer topic.

    * To consume a specific target message, use the **`identifyTargetMessage`** action and provide a unique value along with its corresponding JSON Path or X-Path.

    * Then use **`consumeKafkaMessage`** with the consumer alias (e.g. `#OrdersConsumer`) in the **Condition** column, and validate/store message **details**, **specific tags** or even the **entire message body.**

    * Always finish with **`closeConsumer`** to release consumer state and resources, even on assertion failure paths.

    **Minimal produce flow**

    | ObjectName | Action | Input | Condition |
    |---|---|---|---|
    | Kafka | :green_circle: [`produceMessage`](kafkaActions.md#producemessage) | `{Sheet:Column}` or literal payload | `#OrdersProducer` |
    | Kafka | :green_circle: [`sendKafkaMessage`](kafkaActions.md#sendkafkamessage) | — | `#OrdersProducer` |

    **Minimal consume flow**

    | ObjectName | Action | Input | Condition |
    |---|---|---|---|
    | Kafka | :green_circle: [`identifyTargetMessage`](kafkaActions.md#identifytargetmessage) | expected value, e.g. `12345` | `$.orderId` (repeatable) |
    | Kafka | :green_circle: [`consumeKafkaMessage`](kafkaActions.md#consumekafkamessage) | — | `#OrdersConsumer` |
    | Kafka | :green_circle: [`closeConsumer`](kafkaActions.md#closeconsumer) | — | — |

    !!! note "Per-step overrides"
        The legacy `setXxx` actions still work and take precedence over the named config for that
        key/step — use them only when you need a one-off override (for example `setPartition`,
        `setKey`, `setTimeStamp`, `addKafkaHeader`, `addSchema`, `setConsumerGroupId`).

    !!! warning "Legacy actions"
        These legacy `setXxx` actions are highlighted in <span style="color:Orange">**Orange**</span> in the grid.
        It is advisable to move to **Kafka Configurations** going forward instead of relying on these
        per-step overrides.

    !!! tip
        If the alias in the **Condition** column doesn't exist, the `default` configuration is used instead.

    === "String Serializer Example"

        For String Serializer, the following are required: **`bootstrap.servers`, `producer.topic`, `value.serializer`, `key.serializer`**

        ![kafka string configuration](/img/kafka/string_serializer_config_v4.png "kafka string configuration"){ width="50%" }

        ![kafka string sample](/img/kafka/string_serializer_sample_v4.png "kafka string sample")

    === "Avro Serializer Example"

        For Avro Serializer, the following are required: **`bootstrap.servers`, `producer.topic`, `value.serializer`, `key.serializer`, `schema.registry.url`, `addSchema`**

        ![kafka avro configuration](/img/kafka/avro_serializer_config_v4.png "kafka avro configuration"){ width="50%" }

        ![kafka avro sample](/img/kafka/avro_serializer_sample_v4.png "kafka avro sample")

=== "Prior to v4.0.0"

    * At the beginning, there should be steps to set up the configurations for the **`Kafka Producer`**.
      For instance setting the **`server`, `producerTopic`, `keySerializer`, `valueSerializer`, `partition`, `headers`** etc. are required.

    * Then there should be steps to create the **`message`**. You can leverage built-in capabilities in INGenious like `Synthetic Data Generation` to create `UUID`s and other data to be fed into the message.

    * The **`produceMessage`** action comes with an editor which makes parameterization of data in the paylod very easy. This action is always marked in <span style="color:Green">**Green.**</span>. [See the section below]

    * Then there should be the **`sendKafkaMessage`** action to push the message to the producer topic.

    * Then there should be steps to configure the **`Kafka Consumer`**.
      For instance setting the **`consumerGroupId`, `consumerTopic`, `valueDeserializer`, `pollIntervals`** etc. are required.

    * To consume a specific target message, use the **`identifyTargetMessage`** action and provide a unique value along with its corresponding JSON Path or X-Path.

    * Eventually there should be steps to consume the message and validate/store message **details**, **specific tags** or even the **entire message body.**

    === "String Serializer Example"

        For String Serializer, the following are required: **`server`, `producerTopic`, `valueSerializer`, `keySerializer`**

        ![kafka string serializer](/img/kafka/string_serializer.png "kafka string serializer")

    === "Avro Serializer Example"

        For Avro Serializer, the following are required: **`server`, `producerTopic`, `valueSerializer`, `keySerializer`, `setSchemaRegistryURL`, `addSchema`**

        ![kafka avro serializer](/img/kafka/avro_serializer.png "kafka avro serializer")


-------------------------------------

## Kafka Configurations

=== "v4.0.0 and up"

    <span class="version-badge"><span class="badge-icon">:octicons-tag-16:</span><span class="badge-version">4.0.0</span></span>
    Open the **gear icon** :gear: :material-arrow-right: **Settings** :material-arrow-right: **Kafka Configurations**.
    This single tab replaces the legacy **Kafka SSL Configurations** tab and hosts two sides:

    * **Producers** — one config per producer alias (e.g. `OrdersProducer`)
    * **Consumers** — one config per consumer alias (e.g. `OrdersConsumer`)

    Each side has a dropdown to select an existing alias, plus **New**, **Delete** and **Test Connection**
    buttons. A `default` alias is created automatically the first time the project is opened.

    Configuration fields are grouped into collapsible sections:

    | Group | Producer fields | Consumer fields |
    |---|---|---|
    | General | `producer.alias` | `consumer.alias` |
    | Connection | `bootstrap.servers`, `producer.topic`, `partition` | `bootstrap.servers`, `consumer.topic`, `group.id` |
    | Serialization | `key.serializer`, `value.serializer` | `value.deserializer` |
    | Polling | — | `poll.retries`, `poll.interval.ms`, `max.poll.records` |
    | Schema Registry | `schema.registry.url`, `auto.register.schemas`, `shared.secret` | `schema.registry.url`, `shared.secret` |
    | SSL | `ssl.enabled`, truststore/keystore location, password, type, `ssl.key.password` | same |

    `key.serializer` / `value.serializer` (and `value.deserializer`) accept short aliases which are
    resolved to the underlying class:

    | Alias | Resolves to |
    |---|---|
    | `string` | `StringSerializer` / `StringDeserializer` |
    | `bytearray` | `ByteArraySerializer` / `ByteArrayDeserializer` |
    | `avro` | Confluent `KafkaAvroSerializer` / `KafkaAvroDeserializer` (requires `schema.registry.url`) |
    | *(anything else)* | Treated as a fully-qualified class name |

    **SSL and Schema Registry**

    * Set `ssl.enabled=true` on the alias to enable one-way or mutual TLS; keystore/truststore fields
      are only required for the auth mode you use.
    * Set `schema.registry.url` when using `avro`
    * `auto.register.schemas` (producer only) controls whether new Avro schemas are auto-registered
      with the schema registry.

    !!! tip "Test Connection"
        Use **Test Connection** to validate `bootstrap.servers` (and, if set, that the configured
        topic exists) without producing or consuming a real message.

=== "Prior to v4.0.0"

    If Key Store Certificates are required, you may set it up by clicking on the **gear icon** :gear: to open up the **Run Settings** :material-arrow-right: **Kakfa ssl Configurations**

    === "With SSL certificate configuration example"

        For this example, **`Producer_ssl_Enabled` is set to `true`** then the following are required: **`Producer_Keystore_Location`, `Producer_Key_Password`, `Producer_Keystore_Password`**

        ![With SSL configuration](/img/kafka/with_ssl.png "With SSL configuration"){ width="50%" }

    === "Without SSL certificate configuration example"

        For this example, **`Producer_ssl_Enabled` is set to `false`**

        ![Without SSL configuration](/img/kafka/without_ssl.png "Without SSL configuration"){ width="50%" }

-------------------------------------

## Payload Data Parameterization


 Data Parameterization can be done using the built-in **editor.** If you mouse-hover on the **Input** column, corresponding to the **`produceMessage`** step, an option to open up the Editor comes up.

 Inside this editor, we can paste the entire Payload and then parameterize the specific JSON/XML tags based on our needs.

 If we press ++ctrl+space++ the list of all available **DataSheets : ColumnNames** along with all **user-defined variables** show up. We can then select the appropriate item from where we want to parameterize.

 We need to press ++escape++ to close the editor

 ![editor](/img/kafka/editor.gif "editor")
 
 -------------------------------------

## Assert/Store Response Tags

 We can access the Response Tags using **`xpath`** for XMLs and **`jsonPath`** for JSONs.

 The corresponding **`xpath`** or **`jsonPath`** for the tag, should be entered in the **Condition** column like as shown below :

 ![assertions](/img/kafka/assertions.png "assertions")

??? note "Example for writing Xpath"

    ```xml
    <root xmlns:foo="http://www.foo.org/" xmlns:bar="http://www.bar.org">
        <actors>
            <actor id="1">Christian Bale</actor>
            <actor id="2">Liam Neeson</actor>
            <actor id="3">Michael Caine</actor>
        </actors>
    </root>
    ```

    XPath for retrieving **Liam Neeson** is `/root/actors/actor[2]/text()` or simply `//actor[2]/text()`

??? note "Example for writing JSONPath"

    **Example 1 :**

    ```json
    { 
    "name":"TestName",
    "salary":"12300",
    "age":"29"
    }
    ```

    JSON Path for retrieving **TestName** is `$.name` 

    **Example 2 :**

    ```json
    {
        "page": 2,
        "per_page": 6,
        "total": 12,
        "total_pages": 2,
        "data": [
            {
                "id": 7,
                "email": "michael.lawson@xyz.com",
                "first_name": "Michael",
                "last_name": "Lawson"
            },
            {
                "id": 8,
                "email": "lindsay.ferguson@xyz.com",
                "first_name": "Lindsay",
                "last_name": "Ferguson"
            },
            {
                "id": 9,
                "email": "tobias.funke@xyz.com",
                "first_name": "Tobias",
                "last_name": "Funke"
            },
            {
                "id": 10,
                "email": "byron.fields@xyz.com",
                "first_name": "Byron",
                "last_name": "Fields"
            },
            {
                "id": 11,
                "email": "george.edwards@xyz.com",
                "first_name": "George",
                "last_name": "Edwards"
            },
            {
                "id": 12,
                "email": "rachel.howell@xyz.com",
                "first_name": "Rachel",
                "last_name": "Howell"
            }
        ],
        "additional": {
            "url": "https://xyz.com",
            "text": "Happy Testing!"
        }
    }
    ```

    JSON Path for retrieving **byron.fields@ing.com** is `$.data[3].email` [Index starts with 0]

>To learn more about JSONPath, visit this [GitHub](https://github.com/json-path/JsonPath) page.

>To learn more about XPath, visit the [XPath Syntax](https://www.w3schools.com/xml/xpath_syntax.asp) page.

-------------------------------------

[Actions](kafkaActions.md){ .md-button }