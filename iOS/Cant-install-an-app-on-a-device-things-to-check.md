# Can't install an app on an iOS device? Things to check

Apple doesn't provide explicit error messages when installing apps on devices. It can be quite difficult to understand what could have gone wrong.

## Behaviors

### iOS install popup did not appear

After tapping the "Install" link on the Diawi installation page, if the iOS popup "Diawi would like to install&hellip;" did not appear, check that you don't already have the same app installed from the AppStore.
If an app with the same bundle identifier is already installed on the device from the AppStore, nothing will happen. This is a security behavior added by Apple in iOS 8+ to prevent a malicious developer from overwriting a real app with another one.

Delete the app installed from the AppStore to be able to install the testing one from Diawi.

### Nothing seems to happen

The popup appeared, but after tapping the "Install" button of the popup, nothing seems to happen: check the device's home screen as the installation should be in progress in the background. Since iOS 8+, app installation is performed in the background on the device's home screen and Safari doesn't show anything special, however the icon can be found on the home screen and a progress indicator shows the installation progress.

Also, since iOS 14+, the app icon may only appear in the __App Library__ instead of the home screen, depending on the device's settings.

> See paragraph "Installed app not visible on the home screen" on [iOS 16 changes and known issues](/iOS/iOS16-changes-and-known-issues.md) for more details.

### Untrusted Enterprise Developer popup

Starting from iOS 9+, the developer of an Enterprise signed app (in-house mobileprovision) has to be trusted by the user of the device, otherwise a popup will appear and prevent from using the app.

On iOS 9.0/9.1, this can be done in: Settings > General > Profiles > tap on the developer's profile, and tap on Trust.
On iOS 9.2+, this can be done in: Settings > General > Device Management > tap on the developer's profile, and tap on Trust.

### App fails to launch without internet connection

On first launch after installation, iOS contacts Apple's servers to validate the app's signing certificate. If the device has no internet connection at that moment, the app will fail to open. This applies to all provisioning profile types (Development, Ad-hoc, and In-house).

Make sure the device is connected to the internet — via Wi-Fi or cellular — when opening the app for the first time.

### App crashes immediately on launch

If the app installs but crashes immediately when opened, and the app is signed with a __Development__ provisioning profile, check that __Developer Mode__ is enabled on the device (iOS 16+).

> See paragraph "Developer Mode required for development apps" on [iOS 16 changes and known issues](/iOS/iOS16-changes-and-known-issues.md) for the detailed steps.

### Unable to download app popup

If an "Unable to download app" popup appears after some time, first check the internet connection, and be sure that the device is not behind a firewall that may prevent downloading .ipa files (as this happens a lot in enterprise firewall configurations).

Sadly, iOS won't give any detailed information on what went wrong here. As a user, Diawi provides information on the installation page about the most common checks. As a developer, a detailed list of checks can be found below.

Most common installation issues are:

 * expired provisioning profile
 * device's UDID not in the provisioning profile
 * incompatible device (minimum iOS version, device family, required device capabilities and supported architectures)
 * device has not enough space left

## A few things to check as a developer

If you have uploaded an app to Diawi and can't install it on some of your devices, here are a few things to check:

 * device's UDID must be in the provisioning profile built into the app by xcode
 * device's UDID must not start with "fffffff..." (if it is, then it is fake)
 * you are building a Release version of your app and for all architectures
 * the device is not behind an enterprise firewall preventing the download of the app

You may also try to drag&drop the app into iTunes and sync your device: it should install the app, otherwise it is not valid.

## More detailed explanations

### UDIDs in the provisioning profile
Apple rules regarding app installation also apply when using Diawi: if you are using a __Development or Ad-hoc__ provisioning profile, devices' UDIDs must be added to the provisioning profile used to sign your app. __In-house__ builds with an Enterprise Apple account don't require registering UDIDs (though since 2022, Apple has been deprecating Enterprise account and the In-house distribution, to be replaced by other internal distribution processes like MDM, Apple Business Manager, ... which only work well for release versions not practical for testing).

Since xcode 4, the .mobileprovision file is embedded into the .app/.ipa file when compiling. When in doubt about which version has been used by xcode, you may simply unzip the .ipa file, then right-click Show package content on the .app located inside the Payload folder and look for the embedded.mobileprovision. The file can be opened with a text editor (TextMate, Sublime Text, Atom, ...): contains some XML/plist contents with the list of UDIDs.

XML/plist data inside the .mobileprovision looks like this:
```
﻿<key>ProvisionedDevices</key>
<array>
    <string>37149a037f1..................................3c0078</string>﻿
    ....
</array>
```

Diawi displays the list of UDIDs of an uploaded app on the dashboard and on the installation page. A user can also identify its device on Diawi's webapp and a warning will then be displayed on the installation page if the user's device UDID is not inside that list.

### Valid UDIDs
UDIDs are string of 40 hexadecimal characters (`[0-9a-f]{40}`).

Device's UDID must be retrieved using iTunes or the Finder on a mac, or a webapp like [webapp.diawi.com](https://webapp.diawi.com): those UDIDs are known to be valid.

For some time, it was possible to get the device's UDID using a native API provided by Apple and integrated in some apps available on the AppStore. However, this API has been deprecated in iOS 7 and instead provides a __"fake" UDID starting with ffffff__.... Those UDIDs are __not valid__ and can't be used to identify a device and install apps on it.

### Built architectures

All currently supported iOS devices use the __arm64__ architecture. Since iOS 11 (2017), Apple dropped 32-bit support entirely, and since Xcode 12, armv7 is no longer included in default build architectures.

With the Debug configuration in Xcode, the default setting is to build only the "current" architecture (for faster compilation). With the Release configuration, all active architectures will be built. In practice today this only means arm64, but the Debug/Release distinction still matters when building for the iOS Simulator (which uses x86_64 or arm64 depending on the Mac).

Make sure you are distributing a __Release__ build (or at least a build targeting arm64) to ensure compatibility with all current devices.

#### Historical architectures

Before iOS 11, multiple architectures coexisted and apps could target one or more of them:

 * armv6: iPhone 2G+, iPod touch 1st gen.+
 * armv7: iPhone 3GS+, all iPads, iPad mini 1, iPod touch 3rd gen.+
 * armv7s: iPhone 5+, iPad 4+, iPad mini 1, iPod touch 3rd gen.+
 * arm64: iPhone 5s+, iPad Air+, iPad mini 2+, iPod touch 6th gen.+

(Source: [List of iOS devices on Wikipedia](https://en.wikipedia.org/wiki/List_of_iOS_devices#Features))

Newer devices were compatible with older architectures: an iPad Air (arm64) could run an armv7 built app, but not the opposite. As of Xcode 6/7, the default was armv7+arm64.
