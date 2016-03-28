# iOS 8 changes and known issues

## Valid bundle identifier in the manifest

Since iOS 8.x, Apple has changed the way the manifest is read by the device.

Before, the device didn't check the bundle identifier in the manifest: the app installed could have a different identifier.
Now, the bundle identifiers must match.

> Diawi provides manifests with valid bundle identifiers.

## Mandatory HTTPS on the manifest URL

Since iOS 8.x, Apple has changed the way the manifest is downloaded by the device.

Before, the device could load a manifest from an http or https URL.
Now, the manifest will be accepted by the device only from an https URL.

> Diawi provides https for manifest URLs.

## No more provisioning profile management

Since iOS 8.0, provisioning profiles can't be installed manually anymore, and they do not appear anymore in the Settings app. 
They are embedded inside the .app/.ipa file by xcode, and are installed automatically with the app.

## Background app installation

Since iOS 8.0, app installation happens in the background: after tapping the install link, it may seem that nothing happens, but the app is actually being installed on the Springboard. Check the Springboard to see the app icon.

## iOS 7 to iOS 8 update

If an app has been installed on iOS 7 and then the device updated to iOS 8, it may be possible that the development app couldn't be installed anymore: there seems to be some kind of cache on the bundle identifier preventing wireless installation.
A trick was used during the first months after iOS 8 release by providing another temporarily fake bundle identifier in the manifest.
