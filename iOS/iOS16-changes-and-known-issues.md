# iOS 16 changes and known issues

## Developer Mode required for development apps

Since iOS 16, Apple requires __Developer Mode__ to be enabled on the device in order to install and run apps signed with a development provisioning profile.

To enable Developer Mode:

1. Open the __Settings__ app
2. Go to __Privacy & Security__
3. Scroll down to __Developer Mode__
4. Toggle it __on__
5. The device will ask to restart — tap __Restart__
6. After reboot, confirm by tapping __Turn On__ when prompted

> Note: The Developer Mode menu only appears in Settings after the device has been connected to Xcode, or after attempting to install a development-signed app.

## Installed app not visible on the home screen

Since iOS 14, Apple introduced the __App Library__, which can cause newly installed apps to not appear on the home screen.

After a successful installation from Diawi, the app icon may only be in the App Library (swipe left past the last home screen page) instead of appearing directly on the home screen. This depends on the device's settings.

To ensure new apps appear on the home screen: __Settings__ > __Home Screen & App Library__ > select __Add to Home Screen__.

Alternatively, the app can always be found by swiping down on the home screen to use Spotlight search, or by browsing the App Library.
