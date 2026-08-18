## Version Compatibility

### Framework Versions

Please see [INGenious Version History](ingeniousVersions.md) for the version table of releases.

### Plugin Compatibility Requirements

| Component | Requirement | Why |
|-----------|-------------|-----|
| **Java Compiler** | Java 17 or lower | Framework JVM runs Java 17; cannot load bytecode from newer Java versions |
| **Playwright Version** | 1.50.0 (same as framework) | Must use same version to avoid `NoSuchMethodError` |
| **API Version** | Match framework's API version | Ensures interface compatibility |


### Java Version Compatibility Matrix

| User's JRE/JVM      |  Main App and API Java Version |Plugin Java Version| Result | Notes |
|---------------------|---------------------|--------------------------------|--------|-------|
| 17                  | 17                  | 17                   | ✅ **Recommended** | All components match; full compatibility |
| 17                  | 17                  | 11                   | ✅ Works | Plugin limited to Java 11 features; runs on Java 17 JVM |
| 17                  | 17                  | 21                   | ❌ **UnsupportedClassVersionError** | Plugin compiled with newer Java; cannot load on Java 17 JVM |
| 17                  | 11                  | 17                   | ⚠️ Works, new features must only be used internally within the plugin | If the plugin uses Java 17 features only internally and never exposes them to the main app (e.g., via method signatures, return types, or exceptions), it will generally work—but care must be taken to avoid accidental exposure. IT is recommended to compile plugins for the same or older Java version as the main app. |
| 17                  | 17                   | 8                   | ✅ Works | Plugin limited to Java 8 features; runs on Java 17 JVM |
| 11                  | 17                   | 17                  | ❌ **UnsupportedClassVersionError** | Main App and plugin compiled with newer Java; cannot load on Java 17 JVM |
| 21                  | 17                   | 17                   | ✅ Works | Plugin limited to Java 17 features; runs on Java 21 JVM |

### Playwright Version Compatibility Matrix

| Main App Playwright Version | Plugin Playwright Version | Result | Notes |
|-----------------------------|--------------------------|--------|-------|
| 1.50.0                      | 1.50.0                   | ✅ **Recommended** | Versions match; full compatibility |
| 1.50.0                      | 1.55.0                   | ❌ **NoSuchMethodError** | Plugin may compile and reference newer APIs, but any call to a new API on a Playwright object from the main app will fail at runtime |
| 1.50.0                      | 1.40.0                   | ✅ Works | Plugin uses only older APIs, which are present in the main app |

!!!Note "Same pattern applies with appium dependency."

!!!Note "IDE May Suggest APIs Not Available at Runtime"
    During development, your IDE may show and allow you to use new Playwright APIs if your plugin's dependency is set to a newer version. However, at runtime, only the Playwright version loaded by the main app is actually present. If your plugin tries to use a newer API that does not exist in the main app’s Playwright version (even if the code compiles), it will result in runtime errors such as `NoSuchMethodError`.

!!!Note "Match Plugin Playwright Version and Use Provided Scope"
    **Always set your plugin's Playwright dependency version to exactly match the main app, and use `<scope>provided</scope>`. This ensures that what you see in development matches what will work at runtime, and prevents subtle, hard-to-debug errors.**
