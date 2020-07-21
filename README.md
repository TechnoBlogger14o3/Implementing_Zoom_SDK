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
  
 - In the downloaded file you will see two folders named ***commonlib*** and ***mobilertc***. Import these two as a module. 
  - Change the APP_KEY property and the APP_SECRET property defined in AuthConstants.java to your own SDK key and secret.
  ```
  public final static String WEB_DOMAIN = "zoom.us";
  public final static String APP_KEY = "Your SDK Key";
  public final static String APP_SECRET = "Your SDK Secret";
  ```
# By now all things are placed correctly, its time to play with your app.
- In the MainActivity initialize the ZoomSDK, and implement ``` ZoomSDKInitializeListener, View.OnClickListener, ZoomSDKAuthenticationListener ```
- And initialize it like this
 ``` 
        ZoomSDK sdk = ZoomSDK.getInstance();
          if (sdk.isLoggedIn()) {
            finish();
            showApiExampleActivity();
            return;
          }

          if (savedInstanceState == null) {
            sdk.initialize(this, SDK_KEY, SDK_SECRET, WEB_DOMAIN, this);
          }
 ```
 
 ```
   @Override
    public void onZoomSDKInitializeResult(int errorCode, int internalErrorCode) {

        if (errorCode != ZoomError.ZOOM_ERROR_SUCCESS) {
            Toast.makeText(this, "Failed to initialize Zoom SDK. Error: " + errorCode + ", internalErrorCode=" + internalErrorCode, Toast.LENGTH_LONG).show();
        } else {
            Toast.makeText(this, "Initialize Zoom SDK successfully.", Toast.LENGTH_LONG).show();
            ZoomSDK sdk = ZoomSDK.getInstance();
            if (sdk.tryAutoLoginZoom() == ZoomApiError.ZOOM_API_ERROR_SUCCESS) {
                sdk.addAuthenticationListener(this);
                btnLogin.setVisibility(View.GONE);
                progressBar.setVisibility(View.VISIBLE);
            } else {
                btnLogin.setVisibility(View.VISIBLE);
                progressBar.setVisibility(View.GONE);
            }
        }
    }
  ```

- You have to provide your Username and Password to initialte the call. 
```
 private void onClickBtnLogin() {
        String userName = mEdtUserName.getText().toString().trim();
        String password = mEdtPassord.getText().toString().trim();
        if (userName.length() == 0 || password.length() == 0) {
            Toast.makeText(this, "You need to enter user name and password.", Toast.LENGTH_LONG).show();
            return;
        }
        ZoomSDK zoomSDK = ZoomSDK.getInstance();
        if (zoomSDK.loginWithZoom(userName, password) != ZoomApiError.ZOOM_API_ERROR_SUCCESS) {
            Toast.makeText(this, "ZoomSDK has not been initialized successfully or sdk is logging in.", Toast.LENGTH_LONG).show();
        } else {
            mBtnLogin.setVisibility(View.GONE);
            mProgressPanel.setVisibility(View.VISIBLE);
        }
    }
```
