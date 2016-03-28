# iOS 9 changes and known issues

## Enterprise developers and in-house applications

Since iOS 9.0, Apple has changed the way in-house apps are authorized on the devices.

Before, an app distributed with an in-house signature and mobileprovision could be installed and launched directly.
At first launch of the app, an "Untrusted Enterprise Developer" will show.
The app developer has to be "trusted" through the Settings of the device.

> See paragraph "Untrusted Enterprise Developer popup" on [Can't install an app on a device? Things to check](/iOS/Cant-install-an-app-on-a-device-things-to-check) for the detailed steps.

## Development apps can't overwrite AppStore apps

Since iOS 9.x, Apple has changed the way development/in-house vs AppStore apps are installed.

Before, a development app with the same bundle identifier could overwrite an existing AppStore app.
This could be dangerous since a legitimate app from the AppStore could then be replaced by an unknown app.
Now, when trying to install a development app with the same bundle identifier as an app from the AppStore already on the device, nothing will happen.

> See paragraph "iOS install popup did not appear" on [Can't install an app on a device? Things to check](/iOS/Cant-install-an-app-on-a-device-things-to-check) for more information on this.
