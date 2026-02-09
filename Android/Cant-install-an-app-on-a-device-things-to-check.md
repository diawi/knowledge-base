# Can't install an app on an Android device? Things to check

Android doesn't provide explicit error messages when installing apps on devices. It can be quite difficult to understand what could have gone wrong.

## Behaviors

### Allow unknown sources / Install unknown apps

By default on Android devices, installation is not allowed from "unknown sources", in other words from sources/sites other than the Play Store.

In order to install an app from Diawi, this __must be allowed__ on the device.

Since __Android 8.0 (Oreo)__, the setting is __per-app__: each app (e.g. Chrome, Firefox) must be individually allowed to install APKs. Go to __Settings > Apps > [the browser used to download] > Install unknown apps__ and toggle it on.

> On older Android versions (before 8.0), this was a single global toggle: in the Settings app, under Security or Applications, check the box "Unknown sources".

### App not installed — signature mismatch

If the device already has the same app installed from the Play Store (or signed with a different key), Android will refuse to install the version from Diawi. This is because Android requires all updates to an app to be signed with the __same key__ as the currently installed version.

This also applies when switching between debug and release builds, as they use different signing keys.

To resolve this, __uninstall the existing version__ from the device before installing the one from Diawi or use different package identifiers for test and release builds.
