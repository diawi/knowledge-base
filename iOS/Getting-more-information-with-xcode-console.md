# Getting more information with xcode's console on iOS

Apple doesn't provide much information to the end user when the installation goes wrong. Often, error messages are generic ones like "The application could not be downloaded".

One way to get a little bit more information is to connect the device to a Mac with xcode, and look at the console.

## Accessing the console

The device console is located in xcode's Window > Devices menu

![Xcode Devices in the Window menu](/iOS/images/xcode-devices-menu.png)

In the Device window, choose your device on the left and the console will appear in the bottom right.

![Xcode Devices window](/iOS/images/xcode-devices-window.png)

Search for lines containing `itunesstored`: those error messages often help debugging problems with installations.

## Error messages
* Cannot load non-https manifest URL

The error in the screenshot above means that a manifest plist was requested on an HTTP url, but Apple requires that manifests must be served through HTTPS since iOS 8+.

This error should never happen on Diawi, but may happen on custom setups.
