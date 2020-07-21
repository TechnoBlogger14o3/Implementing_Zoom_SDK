# Implementing Zoom SDK
Zoom has created a Java library for Android, letting us easily start or join Zoom video meetings inside our apps. The Zoom SDK makes it easy to integrate Zoom with our applications, and adds the power of Zoom to our applications.

Easy to use: Zoom SDK is built to be easy to use. Just import the libraries, call a few functions, and it will take care of all video conferencing related stuff for us.
Localizable: This SDK naturally supports 7 major languages, and we can add more to support your applications internationally.
Custom Meeting UI: If we want to add our own decorations to our Zoom meeting rooms, try the Custom UI feature to make our meeting room special.

# Zoom Android SDK Getting Started
Below are the prerequisites:
- Android API Level: Minimum is 21 and Maximum is 29
- Android Device & Emulator: OS: Android 5.0 (API Level 21) or later, and 
CPU: armeabi-v7a, x86, armeabi, arm64-v8a, x86_64
# Android Projet & Gradle Settings:
- Support AndroidX
- compileSdkVersion: 29+
- buildToolsVersion: 29+
- minSdkVersion: 21
# Required Dependencies:
```
implementation 'androidx.multidex:multidex:2.0.0'
implementation 'androidx.recyclerview:recyclerview:1.0.0'
implementation 'androidx.appcompat:appcompat:1.0.0'
implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
implementation 'com.google.android.material:material:1.0.0-rc01'
```
# Installing the Zoom SDK
- Download the Zoom SDK from this [link.](https://github.com/zoom/zoom-sdk-android/archive/master.zip)
- Verifiy below files
  - CHANGELOG.md
  - LICENSE.md
  - README.md
  - docs
  - [mobilertc-android-studio] <- Libraries and examples are inside.
  - proguard.cfg
  - version.txt
  
  # In the downloaded file you will see two folders named ***commonlib*** and ***mobilertc***. Import these two as a module. 
  - Change the APP_KEY property and the APP_SECRET property defined in AuthConstants.java to your own SDK key and secret.
  ```
  public final static String WEB_DOMAIN = "zoom.us";
  public final static String APP_KEY = "Your SDK Key";
  public final static String APP_SECRET = "Your SDK Secret";
  ```
# By now all things are placed correctly, its time to play with your app.
