# **Test Data**

!!! info
    **Test Data** is how INGenious drives data-driven testing: instead of hardcoding values into test steps, you store them in datasheets and reference them from your test cases. Every project gets its own Test Data, and a datasheet (or an entire environment) can be promoted to **Shared Test Data** so it can be reused by any other project opened in the same INGenious installation — the same **Project** / **Shared** scoping already used for [Reusable Components](knowyourframework.md#test-design-pane) and the Object Repositories.

!!! abstract "Key Benefits:"
    * **Data-driven test cases** – Keep values out of your steps and drive the same test case with different rows of data.
    * **Multiple environments** – Maintain separate values per environment (`Default`, `QA`, `UAT`, …) without duplicating test cases.
    * **Cross-project reuse** – Promote a datasheet to **Shared** so it can be referenced from any project, instead of copy-pasting the same CSV into every project that needs it.
    * **Centralized maintenance** – Update a Shared datasheet once and every project referencing it picks up the change.

## Test Data Structure

Test Data is organized as follows:

    ```
    ├── TestData
    │   ├── Default (Environment)
    │   │   ├── Sheet1.csv
    │   │   └── Sheet2.csv
    │   └── QA (Environment)
    │       ├── Sheet1.csv
    │       └── Sheet2.csv
    ```

* A project can define **multiple Environments** (see [Know the Framework](knowyourframework.md#test-design-pane) for how to set these up). Every Environment has its own set of datasheets and its own **Global Datasheet** (see [Global Datasheets](../hiddengems/globalDataSheet.md)).
* Each datasheet is a `.csv` file made up of rows, one row per data set. Every row carries these built-in columns, followed by any custom columns you add:

    | **Column** | **Description** |
    |------------|------------------|
    | **Scenario** | The Scenario the row's data belongs to. |
    | **Flow** | The Test Case the row's data belongs to. |
    | **Scope** | Read-only. Auto-populated as `[Project]`, `[Shared]`, or empty (Test Plan) based on where the selected Scenario/Test Case lives. |
    | **Iteration** | The iteration number the row belongs to. |
    | **SubIteration** | The sub-iteration number the row belongs to. |

* Sheet names must be unique within the scope (Project or Shared) they belong to.

## Project and Shared Test Data

There are two scopes of Test Data:

* **Project Test Data**

    Contains datasheets that **can be used within the project** and are managed from the **`Project`** tab in the Test Data pane.

    They live under `<ProjectName>\TestData\<Environment>\` in the project directory.

    When a Project datasheet is used in a test step, it can be referenced as **`Sheet:Column`** (the default, unchanged behavior) or explicitly as **`[Project] Sheet:Column`**.

* **Shared Test Data**

    Contains datasheets that **can be used across different projects** opened in the same INGenious installation, and are managed from the **`Shared`** tab in the Test Data pane.

    They live outside any single project, under `Shared\SharedTestData\<Environment>\` at the application level — so any project can reference the same Shared datasheet without copying it.

    A `projects.items` manifest tracks which projects currently reference Shared Test Data. INGenious uses this list to warn you before a rename or delete affects other projects (see [Renaming and Deleting Shared Test Data](#renaming-and-deleting-shared-test-data)) — the same convention used by Shared Reusable Components and the Shared Object Repository.

    When a Shared datasheet is used in a test step, it is referenced as **`[Shared] Sheet:Column`**.

* Datasheets may share the same names across the Project and Shared scopes. However, names must remain unique within each individual scope.

## Referencing Test Data in Test Steps

| **Reference form** | **Resolves against** |
|---------------------|-----------------------|
| `Sheet:Column` | The project's own Test Data (unchanged, canonical form). |
| `[Project] Sheet:Column` | The project's own Test Data — tag explicit. |
| `[Shared] Sheet:Column` | The app-root Shared Test Data store. |

* The easiest way to add a reference is to **drag and drop** a column header from either the `Project` or `Shared` Test Data tab onto a step's Input/Condition field — INGenious inserts the correctly tagged reference (`[Project] Sheet:Column` or `[Shared] Sheet:Column`) automatically.
* Inside a larger value — a webservice payload, SQL text, a URL, a file template — a Test Data reference must be wrapped in curly braces to tell it apart from the surrounding text, for example `{Sheet:Column}` or `{[Shared] Sheet:Column}`.
* An **untagged** or `[Project]`-tagged reference only ever resolves against the project's own Test Data — it will never silently fall back to Shared Test Data. Only an explicit `[Shared]` tag resolves against the Shared store.

## Making Test Data Shared

A Project datasheet is promoted to Shared Test Data using **`Make As Shared TestData`**:

* Right-click a **datasheet tab** (on the `Project` Test Data tab) and choose **`Make As Shared TestData`** to move just that sheet.
* Right-click an **environment tab** and choose **`Make As Shared TestData`** to move the entire environment — every datasheet in it, plus its Global Data. The `Default` environment is kept but emptied; any other environment is removed from the project once its data has moved.
* `Make As Shared TestData` is only offered from the `Project` tab, never from `Shared`. Global Data cannot be moved on its own from a datasheet's menu — use the environment's `Make As Shared TestData` instead.

When you confirm the move:

1. If Test Plan or Project Reusable test cases use the data being moved, INGenious lists them and asks whether to **also convert them to Shared Reusables** so other projects can actually run them, not just read their data.
    * **Yes** converts the listed test cases to Shared Reusables and rewrites their references to `[Shared]` as well.
    * **No** moves only the Test Data — INGenious then warns that other consumers of the shared data may not be able to run those test cases.
    * Dismissing the dialog cancels the whole operation.
2. The datasheet (or environment) is moved to `Shared\SharedTestData\`, and every existing reference to it — in the Test Plan, Project Reusables, and Shared Reusables — is rewritten from `Sheet:Column` to `[Shared] Sheet:Column`.
3. If the same sheet name still exists in another environment of the project, its references are **left untouched** (retagging them would break that other environment) — INGenious warns you which sheets were only partially moved so you can move those environments too.
4. A summary notification reports how many sheets moved, how many references were updated, and how many test cases were converted to Shared Reusables.

## Importing Test Data

Use **Test Data → Import TestData** from the menu bar to import one or more CSV datasheets:

1. **Browse** for one or more `.csv` files.
2. Choose **Import into**: **Project Test Data** or **Shared Test Data** (a warning reminds you that Shared Test Data is shared across every project that uses it).
3. Tick one or more target **Environments** (or **Select all**).
4. Click **Import**. The file is imported into every checked environment; an environment that already has a sheet with the same name is skipped, and the outcome is reported in a notification.

## Shared Environment (Execution Setting)

Because Project and Shared Test Data are independent stores, a test run resolves them against **two separate environment settings** in Run Settings / Quick Settings:

* **Environment** – which Project Test Data environment to use (as before).
* **Shared Environment** – which Shared Test Data environment `[Shared]` references resolve against.

This lets a run use, for example, Project environment `QA` while resolving all `[Shared]` references against Shared environment `Default`.

## Renaming and Deleting Shared Test Data

Because a Shared datasheet or environment may be referenced by several different projects, INGenious checks the `projects.items` manifest before a destructive change and warns you if other projects depend on it, listing every project on disk that currently references it before you confirm the rename or delete.

Review the listed projects before proceeding — test steps in other projects that reference the Shared datasheet by its old name will not resolve until they are updated.

[Know the Framework](knowyourframework.md){ .md-button } [Global Datasheets](../hiddengems/globalDataSheet.md){ .md-button }
