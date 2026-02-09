# APK vs AAB: which format to upload to Diawi

## Supported format

Diawi accepts __APK__ files (`.apk`). Android App Bundles (`.aab`) are __not supported__.

## What is the difference?

- __APK__ (Android Package) is the traditional format for distributing and installing Android apps. It is a self-contained file that can be installed directly on a device.
- __AAB__ (Android App Bundle) is a publishing format introduced by Google. It is used to upload apps to the Google Play Store, where Google generates optimized APKs for each device configuration. An `.aab` file cannot be installed directly on a device.

Since 2021, Google requires the AAB format for new apps published on the Play Store. As a result, many build pipelines now produce `.aab` files by default.

## How to generate an APK

If your build produces an `.aab` file, you can generate an APK instead:

### In Android Studio

Build > Build Bundle(s) / APK(s) > __Build APK(s)__

### With Gradle

```bash
./gradlew assembleRelease
```

instead of `./gradlew bundleRelease`.

The APK will be located in `app/build/outputs/apk/release/`.

### From an existing AAB file

Google provides the [bundletool](https://github.com/google/bundletool) command-line tool to generate APKs from an `.aab` file:

```bash
bundletool build-apks --bundle=app.aab --output=app.apks
bundletool extract-apks --apks=app.apks --output-dir=output/ --device-spec=device.json
```
