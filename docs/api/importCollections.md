# Import Postman and Bruno Collections

!!! info
    INGenious can import Postman and Bruno collections and automatically convert them into reusable API components. Postman imports can also migrate associated environments, variables, and test data, reducing the effort required to onboard existing API assets into INGenious.

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

INGenious automatically converts the imported assets into reusable API components and Test Data.

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

* Reusable API components are created within the project.
* Imported environments are created and populated with converted variables.
* Datasheets may be generated automatically based on imported assets.
* An import audit trail and HTML report are generated containing import details, warnings, and items that may require manual review.

Import reports are stored under:

```text
<project>/api/import-reports/
```

## Best Practice

Always review the generated import report after an import completes. While most requests, variables, and environments are converted automatically, some custom scripts or advanced collection features may require manual adjustment.

## Next Steps

After importing a collection:

1. Review the generated reusable components.
2. Verify imported environment variables and authentication settings.
3. Review generated datasheets and parameterized values.
4. Execute the imported requests.
5. Address any warnings or recommendations identified in the import report.

This helps ensure the imported collection behaves as expected in your target environment.