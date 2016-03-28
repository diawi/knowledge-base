# Getting more information with logcat on Android

Android doesn't provide much information to the end user when the installation goes wrong. Often, error messages are generic ones like "The application could not be downloaded".

One way to get a little bit more information is to connect the device to a computer with adb, and look at the logs through logcat.

## Accessing logcat with adb

Connect the device, then run adb (located in `android-sdk/platform-tools`), with the following command line:
```
$ ./adb logcat
```

NB: this may dump a huge number of lines. It is possible to filter using grep: 
```
$ ./adb logcat | grep --line-buffered 'E/'
```
This for example will only display errors (ie. lines containing E/).
