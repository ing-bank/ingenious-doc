# **Prepare to test Android devices**

## **Prerequisites**
-------
Make sure you have performed the [Base Setup](basesetup.md){ .md-button }

#### Download Required Tools

For running automated tests on a real physical device we need the following :

??? info "platform-tools"

    * These are essential for interacting with Android devices and emulators during testing
    * The important tool here is `adb` (Android Debug Bridge), which allows you to install/uninstall apps, access logs, and perform other device-related tasks

??? info "build-tools"

    * While not directly related to Appium, build-tools are crucial for compiling and packaging your app
    * They handle tasks like generating APKs, creating DEX files, and managing resources

??? info "cmdline-tools"

    * These command-line utilities are useful for managing SDK packages and other tasks  

In case we need to run on emulators will need additional tools :

* **platforms**

* **emulator**

* **skins**


## **Android SDK**
-----------------------

The easiest way to set up the Android SDK requirements is by downloading [Android Studio](https://developer.android.com/studio). 

We need to use its SDK manager (Settings :material-arrow-right: Languages & Frameworks :material-arrow-right: Android SDK) to download the following items:

* Android SDK Platform (select whichever Android platform we want to automate, for example, API level 30)
* Android SDK Platform-Tools

If you wish, you can also download these items without Android Studio:

* Android SDK Platform can be downloaded using sdkmanager included in [Android command-line tools](https://developer.android.com/studio#command-line-tools-only)
* [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools)


## **Setting up ANDROID_HOME**
-----------------------

??? info "Windows"

    * Set path for the `Android SDK` folder (the folder containing the cmdline-tools folder) in an environment variable `ANDROID_HOME`
    * Also add the path until `bin` folder in the `PATH` system variable as `%ANDROID_HOME%/bin`
    * Run `appium-doctor --android` to check

??? info "Mac OS"

    Add the `ANDROID_HOME` in `.bash_profile` (for old MACs) or in `.zshrc` or `.zprofile` (for new MACs)

    ```{ .shell .copy }
    export ANDROID_HOME=$HOME/Library/Android/sdk
    ```

    Additionally make sure that the following folders are added to the `PATH` variable

    ```{.shell .copy}
    export PATH=$PATH:$ANDROID_HOME/platform-tools
    export PATH=$PATH:$ANDROID_HOME/cmdline-tools
    export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
    export PATH=$PATH:$ANDROID_HOME/build-tools
    export PATH=$PATH:$ANDROID_HOME/platforms
    export PATH=$PATH:$ANDROID_HOME/emulator
    ```

[Android Setup](androidsetup.md){ .md-button } 
[iOS Setup](iOSsetup.md){ .md-button }    