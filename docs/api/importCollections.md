# Import Postman and Bruno Collections

!!! info
    INGenious can import Postman and Bruno collections and automatically convert them into Test Cases or User Intents. This allows existing API requests to be migrated into INGenious without manually recreating each request.

!!! tip ""
    During import, you can choose to convert each request into a **Test Case** or a **User Intent**. Choosing **User Intent** creates a [User Intent](../home/userIntent.md) that can be executed from any number of test cases via the `Execute` action, instead of a standalone test case. See [User Intent](../home/userIntent.md) for details.

## Supported Formats

The importer supports:

* Postman Collections (`.postman_collection.json`)
* Postman Environments (.postman_environment.json)
* Bruno Collections and Environments (`.bru`)

## Importing a Collection

From the menu bar, select:

```text
Tools → Import Collection → Postman
```

or

```text
Tools → Import Collection → Bruno
```

The Import Wizard guides you through the import process:

1. Select a collection file or folder.
2. Configure the import options.
3. Click **Import**.

INGenious automatically converts the imported requests into Test Cases or User Intents.

## Converted Content

The importer automatically converts commonly used request settings, including:

* Request URLs
* Query Parameters
* Headers
* Authentication Settings
* Request Bodies
* Collection and Environment Variables
* Common Assertions

Where possible, request validations are preserved and converted into INGenious-compatible assertions.

## Environment and Test Data Conversion

* Convert Postman and Bruno environment variables into INGenious Test Data.
* Auto-parameterize supported variable references.
* Generate datasheets from request data and supported test configurations.
* Create datasheet rows for parameterized test execution.

## Import Results

After the import completes:

* Test Cases or User Intents are created within the project.
* An import report is generated containing import details, warnings, and items that may require manual review.

Import reports are stored under:

```text
<project>/api/import-reports/
```

## Best Practice

Always review the generated import report after an import completes. While most requests, variables, and environments are converted automatically, some custom scripts or advanced collection features may require manual adjustment.

## Next Steps

After importing a collection:

1. Review the generated Test Cases or User Intents.
2. Verify environment variables and authentication settings.
3. Execute the imported requests.
4. Update any items flagged in the import report.

This helps ensure the imported collection behaves as expected in your target environment.