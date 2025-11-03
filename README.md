# EASY GEOFENCING

![Easy Geofencing](https://miro.medium.com/max/3160/0*YZbbxorfoqfoxjfK.png)

Easy Geofencing is a flutter geofencing package for flutter application (android & ios) which provides  geofencing functionalities. It is completely written in pure dart language and updated for modern Flutter and Android versions.

> **Note**: This is an updated version compatible with Flutter 3.x and Android 14 (API 34). The original package has been modernized with latest dependencies and Android compatibility.

## FEATURES

![features](https://www.pngkit.com/png/full/423-4235401_small-feature-clipart.png)

* Geofence status triggered on location changes[init,enter,exit] as a geofence Status
* Get continuous geofence status updates
* Optimized dart code
* Battery optimized dart package
* **NEW**: Flutter 3.x compatibility
* **NEW**: Android 14 (API 34) support
* **NEW**: Modern location permissions handling

## REQUIREMENTS

* Flutter 3.0.0 or higher
* Dart 3.0.0 or higher
* Android: API level 21 (Android 5.0) or higher
* iOS: iOS 12.0 or higher

## USAGE

![usage](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ0jeVzQXjiGjkHHxuR3NpYIrSra17ApYRVKQ&usqp=CAU)

To add the easy_geofencing to your flutter application read the [install](https://pub.dev/packages/easy_geofencing/install) instructions. Below are some Android and iOS specifics that are required for the easy_geofencing to work correctly.

## FOR ANDROID

**AndroidX**

The easy_geofencing plugin requires the AndroidX version of the Android Support Libraries. This means you need to make sure your Android project supports AndroidX. Detailed instructions can be found [here](https://flutter.dev/docs/development/packages-and-plugins/androidx-compatibility).

The TL;DR version is:

1. Add the following to your "gradle.properties" file:

```
android.useAndroidX=true
android.enableJetifier=true
```
2. Make sure you set the `compileSdkVersion` in your "android/app/build.gradle" file to 34 (for Android 14 compatibility):

```
android {
  compileSdkVersion 34
  targetSdkVersion 34

  ...
}
```
3. Make sure you replace all the `android.` dependencies to their AndroidX counterparts (a full list can be found here: https://developer.android.com/jetpack/androidx/migrate).

**Permissions**

On Android you'll need to add the location permissions to your Android Manifest. To do so open the AndroidManifest.xml file (located under android/app/src/main) and add the following permissions as direct children of the `<manifest>` tag:

``` xml
<!-- Location permissions -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />

<!-- Background location permission for Android 10+ -->
<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />

<!-- Android 14+ foreground service permissions -->
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE_LOCATION" />

<!-- Android 13+ notification permission -->
<uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
```

**Important Notes for Android 14+:**
- Apps targeting Android 14 need explicit foreground service permissions
- Background location access requires user approval through system settings
- Notification permission is required for foreground services

## FOR IOS

On iOS you'll need to add the following entries to your Info.plist file (located under ios/Runner) in order to access the device's location. Simply open your Info.plist file and add the following:

``` xml
<key>NSLocationWhenInUseUsageDescription</key>
<string>This app needs access to location when open.</string>
<key>NSLocationAlwaysUsageDescription</key>
<string>This app needs access to location when in the background.</string>
```

If you would like to receive updates when your App is in the background, you'll also need to add the Background Modes capability to your XCode project (Project > Signing and Capabilities > "+ Capability" button) and select Location Updates. Be careful with this, you will need to explain in detail to Apple why your App needs this when submitting your App to the AppStore. If Apple isn't satisfied with the explanation your App will be rejected.


## API

### START EASY GEOFENCING SERVICES

At first you need to start the geofence service and for that you need to pass the following arguments:

- `pointedLatitude`: the latitude of the geofence area center
- `pointedLongitude`: the longitude of the geofence area center
- `radiusInMeter`: the radius of the geofence area in meters
- `eventPeriodInSeconds`: geofence status stream period in seconds

``` dart
import 'package:easy_geofencing/easy_geofencing.dart';

EasyGeofencing.startGeofenceService(
    pointedLatitude: "34.2165157",
    pointedLongitude: "71.9437819",
    radiusMeter: "250.0",
    eventPeriodInSeconds: 5
);
```

### GET GEOFENCE STATUS STREAMS

To get the stream geofence Status updates on location changes, you need to subscribe `getGeofenceStream` to listen geofence status streams on current location updates.

``` dart
import 'package:easy_geofencing/easy_geofencing.dart';

StreamSubscription<GeofenceStatus> geofenceStatusStream = EasyGeofencing.getGeofenceStream().listen(
  (GeofenceStatus status) {
    print(status.toString());
});
```
### Stop Geofence Service
To stop geofence service you need to specify this:

``` dart
import 'package:easy_geofencing/easy_geofencing.dart';

EasyGeofencing.stopGeofenceService();
```
Also, stop GeofenceStatus stream subscription listener which is `geofenceStatusStream` in our case

``` dart
geofenceStatusStream.cancel();
```

## MIGRATION GUIDE

### From 0.2.x to 1.0.0

This is a major version update with breaking changes:

1. **Flutter Version**: Minimum Flutter version is now 3.0.0
2. **Dart Version**: Minimum Dart version is now 3.0.0
3. **Android**: Minimum API level is now 21, target API is 34
4. **Dependencies**: Updated geolocator to 12.0.0
5. **Permissions**: Additional Android permissions required for modern compatibility

Update your `pubspec.yaml` environment constraints:
```yaml
environment:
  sdk: ">=3.0.0 <4.0.0"
  flutter: ">=3.0.0"
```

## Issues

Please file any issues, bugs or feature requests as an issue on our [GitHub](https://github.com/jay-simformsolutions/easy_geofencing/issues) page.

## Dependencies

This plugin is depended on geolocator plugin of baseflow.com

## Want to contribute

If you would like to contribute to the plugin (e.g. by improving the documentation, solving a bug or adding a cool new feature), feel free to send your [pull request](https://github.com/jay-simformsolutions/easy_geofencing/pulls).

## Authors

This easy_geofencing plugin for Flutter was originally developed by [uzairleo](https://github.com/uzairleo) and updated for modern Flutter/Android compatibility by [jay-simformsolutions](https://github.com/jay-simformsolutions).