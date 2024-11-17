# **Prepare to test iOS devices**

## **Prerequisites**
-------

* **You need a Mac OS system**

* Make sure you have performed the [Base Setup](basesetup.md){ .md-button }


## **Xcode and Xcode command line tools**
-----------------------

#### Xcode

* Check if **Xcode** is present

* Check for **Xcode** and iOS supported versions [here](https://developer.apple.com/support/Xcode/)

* Download **Xcode** from the App Store or the [Apple Developer website](https://developer.apple.com/Xcode/)

* Open and check **Xcode**



#### Xcode Command Line Tools


* Check if **Xcode CLT** is already available  using :

   `Xcode-select -p`   or    `Xcode-select --print-path`


* If not available, download the command-line tool compatible with your **Xcode** version from the [Apple Developer website](https://developer.apple.com/download/all/)


* Alternatively, you can install the command-line tool for **Xcode** from terminal using following commands:

   `Xcode-select --install`

   `sudo Xcode-select -s /Applications/Xcode.app/Contents/Developer`


## **Check available iOS Simulators**
-----------------------

??? example "Using Xcode"

    * Open Xcode on your Mac.

    * Go to the top menu bar and select **Xcode** :material-arrow-right: **Open Developer Tool** :material-arrow-right: **Simulator**

    * On the **Simulator** menu go to **File** :material-arrow-right: Open **Simulator** and choose the iOS simulator device of your choice

??? example "Using Terminal"

    * To get list of all devices and their IDs

    ```{ .shell .copy }
    xcrun simctl list devices
    ```

    * To boot up any available simulator

    ```{.shell .copy}
    xcrun simctl boot "<name of simulator>" 
    
    example 
    
    xcrun simctl boot "iPhone 16"
    ```

    * To shut down a Simulator

    ```{.shell .copy}
    xcrun simctl shutdown <UUID>
    ```

[Android Setup](androidsetup.md){ .md-button } 
[iOS Setup](iOSsetup.md){ .md-button }    