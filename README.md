## Why this fork

This repository is a curated fork of [bkonyi's FlutterGeofencing](https://github.com/bkonyi/FlutterGeofencing/) repository. Changes will be cherry-picked in from other community members' forks (when the licensing allows), as well as from the upstream repository should they happen. This is because the development speed in upstream is slow and other member may have significant bugfixes that would benefit.

## Branching

Pre-release will be tagged on the `develop` branch, release will be tagged off the `main` branch.

## Versioning

Significant changes will be tagged in this repository, and the tagging convention should roughly follow the convention of pub versions. The tags will have names such as (v_._._) corresponding to the version of the package.

## Usage

To use this repo, simply add the following to the project's `pubspec.yaml`:

```yaml
dependencies:
  geofencing:
    git:
      url: https://github.com/yangsfang/bkonyi-fluttergeofencing.git
      ref: v0.1.0
```

## Interesting forks (in alphabetical order):

* [JFreakDK](https://github.com/JFreakDK/FlutterGeofencing)
* [mister-rao](https://github.com/mister-rao/FlutterGeofencing)
* [umbrew](https://github.com/umbrew/FlutterGeofencing)
* [vovaklh](https://github.com/vovaklh/FlutterGeofencing)

**[bkonyi](https://github.com/bkonyi/)'s Note:** 
this plugin is not officially supported and is meant to be used as an example. Please feel free to pull it into your own projects, but _there is no official version hosted on pub.dev and support may be limited_. If you run into any issues running this sample, please file an issue or, even better, submit a pull request!

What is geofencing? 
[here](https://developer.android.com/training/location/geofencing)

# Geofencing

A sample geofencing plugin with background execution support for Flutter.

## Getting Started
This plugin works on both Android and iOS. Follow the instructions in the following sections for the
platforms which are to be targeted.

### Android

Add the following lines to your `AndroidManifest.xml` to register the background service for
geofencing:

```xml
<receiver android:name="io.flutter.plugins.geofencing.GeofencingBroadcastReceiver"
    android:enabled="true" android:exported="true"/>
<service android:name="io.flutter.plugins.geofencing.GeofencingService"
    android:permission="android.permission.BIND_JOB_SERVICE" android:exported="true"/>
```

Also request the correct permissions for geofencing:

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
```

Finally, create either `Application.kt` or `Application.java` in the same directory as `MainActivity`.
 
For `Application.kt`, use the following:

```kotlin
class Application : FlutterApplication(), PluginRegistrantCallback {
  override fun onCreate() {
    super.onCreate();
    GeofencingService.setPluginRegistrant(this);
  }

  override fun registerWith(registry: PluginRegistry) {
    GeneratedPluginRegistrant.registerWith(registry);
  }
}
```

For `Application.java`, use the following:

```java
public class Application extends FlutterApplication implements PluginRegistrantCallback {
  @Override
  public void onCreate() {
    super.onCreate();
    GeofencingService.setPluginRegistrant(this);
  }

  @Override
  public void registerWith(PluginRegistry registry) {
    GeneratedPluginRegistrant.registerWith(registry);
  }
}
```

Which must also be referenced in `AndroidManifest.xml`:

```xml
    <application
        android:name=".Application"
        ...
```
 
### iOS

Add the following lines to your Info.plist:

```xml
<dict>
    <key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
    <string>YOUR DESCRIPTION HERE</string>
    <key>NSLocationWhenInUseUsageDescription</key>
    <string>YOUR DESCRIPTION HERE</string>
    ...
```

And request the correct permissions for geofencing:

```xml
<dict>
    ...
    <string>Main</string>
    <key>UIRequiredDeviceCapabilities</key>
    <array>
        <string>location-services</string>
        <string>gps</string>
        <string>armv7</string>
    </array>
    <key>UIBackgroundModes</key>
    <array>
        <string>location</string>
    </array>
    ...
</dict>
```

### Need Help?

For help getting started with Flutter, view our online
[documentation](https://flutter.io/).

For help on editing plugin code, view the [documentation](https://flutter.io/developing-packages/#edit-plugin-package).
