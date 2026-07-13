# **API Workbench**

!!! info 
    The API Workbench is an integrated tool within INGenious that allows users to design, test, and validate APIs in a streamlined and user-friendly interface—similar to tools like Postman. It enables teams to easily create API requests (GET, POST, PUT, DELETE, etc.), manage headers and parameters, and inspect responses in real time.

## How to use the API Workbench:

The API Workbench can be accessed via the Menu Ribbon:

![APIWorkbenchMenuRibbon](../img/api/APIWorkbenchMenuRibbon.png "APIWorkbenchMenuRibbon"){ width="60%" }

Once selected, you will be navigated to API Workbench window. See example below:

![APIWorkbenchExample](../img/api/APIWorkbenchExample.png "APIWorkbenchExample")

=== ":one: Collection/Requests Pane"
      This is where the Collections and Requests are created and organized. Every `Collection` in the INGenious IDE , is a JSON file in the backend.

      To see this, you can navigate to the location of your tool, then `Projects` :material-arrow-right: `Your Project` :material-arrow-right: `api` :material-arrow-right: `collections`

      ![APIWorkbenchBackend](../img/api/APIWorkbenchBackend.png "APIWorkbenchBackend")

      If you click on the `+`, this will allow you to create a new collection.

      ![APIWorkbenchCollection](../img/api/APIWorkbenchCollection.png "APIWorkbenchCollection"){ width="30%" }

      If you select a Collection or Request and **Right Click**, you will have some interesting and handy options to work with:

      **Collection level**
      
      ![CollectionLevelOptions](../img/api/CollectionLevelOptions.png "CollectionLevelOptions"){ width="75%" }

      **Request level**
      
      ![RequestLevelOptions](../img/api/RequestLevelOptions.png "RequestLevelOptions"){ width="75%" }
  
=== ":two: Workbench Pane"
       This section allows you to select and configure the API request you want to execute.
       
       ![WorkbenchPane](../img/api/WorkbenchPane.png "WorkbenchPane")

       It supports multiple HTTP methods commonly used for interacting with web services:

       * **GET** – Retrieve data from a server
       * **POST** – Create new resources
       * **PUT** – Update or replace existing resources
       * **PATCH** – Partially update existing resources
       * **DELETE** – Remove resources
       * **HEAD** – Retrieve response headers without the body
       * **OPTIONS** – Discover supported operations and communication options for an endpoint
       
       Several tabs are provided for configuration:

       * **Params** – Define query parameters that are appended to the request URL. Useful for filtering, searching, or passing dynamic values to the API.
       * **Headers** – Add key-value pairs to the request header, such as content type, authorization tokens, or custom metadata required by the API.
       * **Body** – Specify the request payload sent to the server, typically used with POST, PUT, or PATCH requests to create or update data.
       * **Auth** – Configure authentication details (e.g., API keys, tokens, or basic auth) required to securely access the API.
       * **Settings** – Customize request behavior, such as timeouts, redirects, or other advanced configuration options.

       You may also **convert the configured API request into a test case**, capturing all request details for quick integration into your test suite.

       ![ExampleConvertoTC](../img/api/ExampleConvertoTC.gif "ExampleConvertoTC")

=== ":three: Response Body Pane"

      This section displays the API response content in a formatted (Pretty) or raw view, allowing you to easily inspect, copy, and analyze returned data for validation and troubleshooting.

=== ":four: API Environments"

      API Environments allow you to store reusable variables for different testing contexts such as Development, QA, Staging, or Production. This enables the same API request to be reused across multiple environments without manually changing values such as URLs, tokens, usernames, passwords, proxy settings, or certificate paths.

      The **Environment Dropdown** allows you to switch between environments. To open the **Environment Configuration Window** click **Configure**.

      ![APIEnvironmentDropdown](../img/api/APIEnvironmentDropdown.png "APIEnvironmentDropdown")

      The Environment Configuration Window displays all available environments and provides several actions:

      * **+ New** – Create a new environment.
      * **Rename** – Change the name of the selected environment.
      * **Duplicate** – Create a copy of the selected environment, including all configured variables.
      * **Delete** – Remove the selected environment.

      ![APIEnvironmentActions](../img/api/APIEnvironmentActions.png "APIEnvironmentActions")

      **Environment Variable Configuration**

      Variables are configured by entering a **Name** and **Value**. The **Secret** option can be enabled for sensitive information such as passwords, tokens, and API keys. Secret values are masked in the UI and are not displayed in plain text. After adding or updating variables, click **Save** to persist the environment configuration.

      ![APIEnvironmentVariables](../img/api/APIEnvironmentVariables.png "APIEnvironmentVariables")

      Variables can be referenced throughout API requests using double curly braces:

      ```text
      {{variableName}}
      ```

      For example:

      ```text
      {{baseUrl}}/users
      ```

      ![APIEnvironmentRequestExample](../img/api/APIEnvironmentRequestExample.png "APIEnvironmentRequestExample")

      When a request is executed, all referenced variables are automatically resolved using the currently selected environment. Switching to a different environment allows the same request to be executed against a different set of values without modifying the request itself. If a referenced variable does not exist in the active environment, the request execution may fail or use the unresolved placeholder value

=== ":five: Convert API Request to Test Case"

      API requests can be converted directly into INGenious test cases, allowing API validations to be incorporated into automated test suites with minimal effort.

      During conversion, all configured request details are preserved, including:

      * Endpoint URL and query parameters
      * Request headers
      * Authentication settings (Basic Auth, Bearer Token, and API Keys)
      * Request body
      * Assertions

      If the request contains environment variables (for example `{{baseUrl}}` or `{{token}}`), the values are resolved using the **currently active environment** during conversion. Literal values that do not reference environment variables are copied directly into the generated test case.

      The original API request is not modified. Variable placeholders are retained in the collection, while the generated test case receives the resolved values.

      **Converted Test Case Example (Basic Authentication)**

      ![APIRequestToTestCase](../img/api/APIRequestToTestCase.png "APIRequestToTestCase")

      The generated test case performs the same API call as the API Workbench request and can be executed within INGenious to validate the expected response and assertions.