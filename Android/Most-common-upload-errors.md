# Most common upload errors

When an app package is uploaded to Diawi, the content is processed to validate some key elements needed for the installation.
This page provides some insight on most common errors that this processing might produce.

## Invalid package
Diawi expects __APK__ files (`.apk`) for Android applications. Android App Bundles (`.aab`) are __not supported__ as they cannot be installed directly on a device.

> See [APK vs AAB: which format to upload](/Android/APK-vs-AAB.md) for more details on the difference and how to generate an APK.

## Unsigned APK
Android requires all APKs to be __signed__ before they can be installed on a device. If the uploaded APK is not signed, the installation will fail.

APKs built with a __Debug__ configuration in Android Studio are automatically signed with a debug key, so this is usually not an issue during development. However, if you are generating APKs through a custom build pipeline or CI/CD, make sure the signing step is included.

To sign a Release APK in Android Studio: Build > Generate Signed Bundle / APK > APK > select your keystore and key > Release > Finish.

With Gradle, make sure your `build.gradle` includes a `signingConfigs` block for the release build type:
```groovy
android {
    signingConfigs {
        release {
            storeFile file("keystore.jks")
            storePassword "..."
            keyAlias "..."
            keyPassword "..."
        }
    }
    buildTypes {
        release {
            signingConfig signingConfigs.release
        }
    }
}
```

## Debug vs Release build
While debug APKs can be uploaded and installed via Diawi, keep in mind that:

* debug APKs are signed with a __debug key__ that is unique to each developer machine — updating an app on a device requires an APK signed with the __same key__
* debug APKs may have debugging features enabled that affect performance and behavior
* debug APKs are typically larger than release APKs

For sharing with testers or clients, prefer distributing __Release__ builds.
