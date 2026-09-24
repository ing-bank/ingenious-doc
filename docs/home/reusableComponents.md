# **Reusable Components**

!!! info
    A **Reusable** is a self-contained, named group of test steps that represents a single **User Intent** — one discrete action a user performs in the application under test, such as `Login`, `Add to Cart`, or `Submit Form`. Instead of duplicating the same steps in every test case that needs them, you build the action once as a Reusable and **`Execute`** it from any number of other test cases.

!!! abstract "Key Benefits:"
    * **Eliminate duplication** – Author a user intent once and call it from as many test cases as needed.
    * **Centralized maintenance** – Update the Reusable once and every test case that executes it picks up the change automatically.
    * **Faster authoring** – Compose new test cases largely out of existing Reusables instead of raw steps.
    * **Cross-project reuse** – Promote a Reusable to **Shared** so it can be executed from any project opened in the same INGenious installation.

## What is a User Intent?

**User Intent** is the name INGenious gives to a Reusable that is scoped to a single project. It is simply the label used for the **Reusable Components** panel in the Test Design pane — see [Know the Framework](knowyourframework.md#test-design-pane) for where this fits among the other Test Design panels.

Reusable Scenarios and Test Cases follow the same structure as the Test Plan:

* Every Reusable **Scenario** is a `Directory` on disk and typically groups a related set of intents (for example, a `Common` scenario for `Login`/`Logout`, or a `Purchase` scenario for `Add to Cart`/`Checkout`).
* Every Reusable **Test Case** inside that scenario is a `.csv` file, and represents **one User Intent**.

You'll also see the "User Intent" terminology surface outside of Test Design, in places where a set of steps can be generated automatically and you get to choose the kind of artifact to create:

* **API Workbench / Convert to Test Case** – when converting an API request, you can choose to generate a **Test Case** or a **User Intent (Reusable)**.
* **Import Postman/Bruno Collections** – when importing a collection, each request can be converted into a **Test Case** or a **Reusable (User Intent)**.

Choosing the User Intent option in either flow creates the result directly as a Reusable Test Case, ready to be executed from other test cases, instead of a standalone Test Plan test case.

## Project and Shared Reusable Components

There are two scopes of Reusable Components:

* **Project Reusables (User Intent)**

    Contains reusables that **can be used within the project** and are managed from the **`User Intent`** tab in the Test Design pane.

    They live under `<ProjectName>\ReusableComponents\` in the project directory.

    **For projects created before version 3.0**, the tool uses a `ReusableComponent.xml` file located at the project root to organize Reusable Scenarios and Test Cases:

    ``` xml
    <Root ref="Example" type="RC">
       <Folder ref="UI">
          <Scenario ref="Common">
             <TestCase exeType="Executable" ref="Login"/>
          </Scenario>
          <Scenario ref="Purchase">
             <TestCase exeType="Executable" ref="Add to Cart"/>
             <TestCase exeType="Executable" ref="Checkout"/>
             <TestCase exeType="Executable" ref="Logout"/>
          </Scenario>
       </Folder>
    </Root>
    ```

    **For projects loaded in version 3.0**, the legacy `ReusableComponent.xml` is automatically migrated and reorganized into the `ReusableComponents` folder structure. The original file is preserved as a `.bak` file under `<ProjectName>`.

    When a Project Reusable is used in a test step, it is referenced as **`[Project] Scenario:TestCase`**.

* **Shared Reusables**

    Contains reusables that **can be used across different projects** opened in the same INGenious installation, and are managed from the **`Shared Reusables`** tab in the Test Design pane.

    They live outside any single project, under `Shared\SharedReusableComponents\` at the application level — so any project can reference the same Shared Reusable without copying it.

    A manifest file tracks which projects currently reference each Shared Reusable. INGenious uses this list to warn you before a rename or delete affects other projects (see [Renaming and Deleting Shared Reusables](#renaming-and-deleting-shared-reusables)).

    When a Shared Reusable is used in a test step, it is referenced as **`[Shared] Scenario:TestCase`**.

* Reusable Scenarios and Test Cases may share the same names across the Project and Shared scopes. However, names must remain unique within each individual scope.

## Creating a Reusable

There are a few ways to create a Reusable:

* **Create Reusable** – Right-click a Test Case (or selection of steps) in the Test Plan and choose **Create Reusable**. In the dialog, choose the target scope (**Project Reusable** or **Shared Reusable**), pick or create the target Reusable Scenario, and give it a **Reusable Name**.
* **Make As Project Reusable / Make As Shared Reusable** – Right-click an existing Test Plan test case and promote it directly into either scope.
* **Convert to Automation (API Workbench)** – When converting an API request into an automated artifact, choose **User Intent (Reusable)** instead of **Test Case** as the target type.
* **Import Collections** – When importing a Postman or Bruno collection, choose **Reusable (User Intent)** instead of **Test Case** as the target type for the imported requests. See [Import Postman and Bruno Collections](../api/importCollections.md).

## Using (Executing) a Reusable

A Reusable is invoked from any other test case using the **`Execute`** action:

| **Field** | **Value** |
|-----------|-----------|
| **ObjectName** | `Execute` |
| **Action** | `<ReusableScenario>:<ReusableTestCase>` |
| **Reference** | `[Project]` for a Project Reusable, `[Shared]` for a Shared Reusable |

As a best practice, compose your test cases **only from Reusables** rather than mixing in loose, one-off steps — this keeps maintenance centralized and makes larger flows easier to read.

To jump to the definition of a Reusable that's called from a test step, right-click the step and choose **Go To Reusable**.

## Moving and Promoting Reusables

A Reusable is not locked to the scope it was created in. Right-click a Reusable (or a Shared Reusable) to move it between scopes:

* **Make As Shared Reusable** – Promotes a Project Reusable to Shared, making it available to other projects.
* **Move to Project Reusable** – Demotes a Shared Reusable back to a single project's scope.
* Copy variants of both operations are also available when you want to keep the original in place.

Whenever a Reusable is moved or renamed, INGenious automatically rewrites every `Execute` reference to it elsewhere in the project, and confirms with a message such as:

> *"Moved to Shared Reusable completed. All impacted test cases have been updated (N)."*

## Renaming and Deleting Shared Reusables

Because a Shared Reusable may be referenced by test cases in several different projects, INGenious checks the shared manifest before a destructive change and warns you if other projects depend on it, for example:

* **Delete Shared Reusable Components** – lists every project on disk that currently references the Shared Reusable before you confirm the deletion.
* **Rename Shared Reusable - References Found** – lists every project on disk that would be affected by the rename.

Review the listed projects before proceeding — test cases in other projects that reference the Shared Reusable by its old name will not resolve until they are updated.

## Reusables in Loops and With Specific Data

Reusables can also be executed repeatedly or against a specific row of data using loop and parameter blocks. See the following sections in [Additional Features](../hiddengems/additionalfeatures.md):

* [Looping Reusable Components](../hiddengems/additionalfeatures.md#looping-reusable-components)
* [Execute a Reusable for a Specific Set of Data](../hiddengems/additionalfeatures.md#execute-a-reusable-for-a-specific-set-of-data)

[Know the Framework](knowyourframework.md){ .md-button } [Additional Features](../hiddengems/additionalfeatures.md){ .md-button }
