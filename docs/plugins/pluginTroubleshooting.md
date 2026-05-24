# Troubleshooting

- **Duplicate Action Error**

    If you define multiple actions with the same name and object type, INGenious will report a duplicate action error during plugin loading and the application will exit. Ensure that each action method within an object type has a unique name to avoid this issue.

    Below is an example of the error you might encounter:

    ```
    Duplicate action 'assertOddNumberDataSheet' for object type 'Numeric Assert' detected:
    - Original found in: text-assertion-plugin (class: com.ing.plugin2.Plugin2)
    - Duplicate found in: sample-plugin (class: com.ing.plugin.cloader.PluginCloader)
    Duplicate action 'GetOccurence' for object type 'String Operations' detected:
    - Original found in: core (class: com.ing.engine.commands.stringOperations.StringOperations)
    - Duplicate found in: sample-plugin (class: com.ing.plugin.cloader.PluginCloader)
    Duplicate method names detected in the loaded actions. Please resolve the conflicts.
    ```

- **ClassCastException Error**

    If you encounter a `ClassCastException` when casting Playwright objects, check the following:

    1. **Dependency Scope**: Ensure Playwright dependency uses `<scope>provided</scope>` in your pom.xml
    2. **Correct Type**: Verify you're casting to the correct Playwright type
    3. **Null Check**: Always check if the object is null before casting

    ```java
    // ✅ Correct pattern
    Page page = (Page) getPage();
    if (page != null) {
        page.navigate("https://example.com");
    }

    // ❌ Wrong - missing null check
    Page page = (Page) getPage();
    page.navigate("https://example.com"); // NullPointerException if null
    ```

- **Java Version Error (UnsupportedClassVersionError)**

    If you see an error like:

    ```
    java.lang.UnsupportedClassVersionError: 
    com/example/plugin/MyAction has been compiled by a more recent version of the Java Runtime
    ```

    **Cause**: You are using a plugin that was compiled with a newer Java version than your machine's JVM supports.

    **Solution**: Upgrade machine's JRE.

- **NoSuchMethodError**

    If you encounter `NoSuchMethodError` at runtime:

    ```
    java.lang.NoSuchMethodError: com.microsoft.playwright.Page.someNewMethod()
    ```

    **Cause**: Your plugin is trying to use a Playwright API method that doesn't exist in the framework's Playwright version.

    **Solution**: 
    1. Check the framework's Playwright version (currently 1.50.0)
    2. Update your plugin's Playwright dependency to match:

    ```xml
    <dependency>
        <groupId>com.microsoft.playwright</groupId>
        <artifactId>playwright</artifactId>
        <version>1.50.0</version>
        <scope>provided</scope>
    </dependency>
    ```

    3. Use only APIs available in Playwright 1.50.0

- **NoClassDefFoundError for Playwright Classes**

    If you see:

    ```
    java.lang.NoClassDefFoundError: com/microsoft/playwright/Page
    ```

    **Cause**: Missing Playwright dependency in your plugin's `pom.xml`.

    **Solution**: Add Playwright dependency with `provided` scope (see Step 1 of [How to Create Your Plugin](#how-to-create-your-plugin)).
