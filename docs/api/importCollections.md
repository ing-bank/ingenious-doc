# Import Postman and Bruno Collections

!!! info
    INGenious can import Postman and Bruno collections and automatically convert them into reusable API components. This allows existing API requests to be migrated into INGenious without manually recreating each request.

## Supported Formats

The importer supports:

* Postman Collections (`.postman_collection.json`)
* Bruno Collections (`.bru`)

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

INGenious automatically converts the imported requests into reusable API components.

## Converted Content

The importer automatically converts common request settings, including:

* Request URLs
* Query Parameters
* Headers
* Authentication Settings
* Request Bodies
* Collection Variables
* Common Assertions

Where possible, request validations are preserved and converted into INGenious-compatible assertions.

## Import Results

After the import completes:

* Reusable API components are created within the project.
* An import report is generated containing import details, warnings, and items that may require manual review.

Import reports are stored under:

```text
<project>/api/import-reports/
```

## Best Practice

Review the generated import report after each import. While most requests are converted automatically, some custom scripts or advanced collection features may require manual adjustment.

## Next Steps

After importing a collection:

1. Review the generated reusable components.
2. Verify environment variables and authentication settings.
3. Execute the imported requests.
4. Update any items flagged in the import report.

This helps ensure the imported collection behaves as expected in your target environment.