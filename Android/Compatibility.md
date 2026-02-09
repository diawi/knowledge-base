# Compatibility of wireless app installation on Android devices

Wireless installation of apps on Android devices should work starting from __Android 2.0+__ on all smartphones or tablets.

Known __compatible__ web browsers are:

 * Chrome
 * Firefox
 * Samsung Internet
 * Android Browser

Known __not compatible__ web browsers are:

 * none so far

### In-app WebViews

Some apps (Facebook, Gmail, Messenger, ...) open links in an embedded webview instead of the device's browser. These in-app webviews may not handle APK downloads correctly: the download may fail silently or the file may not be openable after download.

If a Diawi link does not work from an in-app browser, tap the menu icon and choose to open the link in Chrome or the default browser, or copy and paste the URL manually.
