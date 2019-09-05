HTML5 Cordova Starter Project
=============================
This project requires the basic setup needed to make an html5 game available as an app trough Cordova.
In it's most basic form you copy some folders and merge a package.json. We also try to awnser some commen pitfalls that we've encountered.

Getting Started
---------------
First and foremost you have to make sure that both node.js and npmjs are installed on your system. Cordova requires these to be available.

When that is done you should install cordova through npmjs globaly:
```bash
ale@NL0NTB032:~$ sudo npm install -g cordova
```

There are some platform specific requirements too but you can easily find them in the Cordova documentation:
* Android: https://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html#installing-the-requirements
* iOS: https://cordova.apache.org/docs/en/latest/guide/platforms/ios/index.html#installing-the-requirements

### Copy Files

Now to get started with the app itself, your first step will be to copy the following folders and files from this project over to your game. The folders need to be copied over with contents for your ease!

* ./platforms
* ./plugins
* ./res
* ./www
* ./config.xml

### Merge package.json
Next step is merging your existing (hopefully? :D) package.json with the one from this project. You can simply add the **devDependencies** and **cordova** properties to your package.json

### Adjust config.xml
Next up is changing the copied config.xml, which will happen in the top of your config.
Based on the following example you need to change the widget id, widget version, name and description to match your game.
```xml
<widget id="your.awesome.packagename" version="3.3.3" xmlns="http://www.w3.org/ns/widgets" xmlns:cdv="http://cordova.apache.org/ns/1.0">
    <name>
        Your awesome game name!
    </name>
    <description>
        Your awesome game description!
    </description>
</widget>
```

### Generate icons
Icons and splash screens are located in the ./res folder. These are prefilled. If you want to create your own icon you should make a nice big one (at least 512x512) and then you can use this service to create them for you: http://pgicons.abiro.com/

### Populate www folder
Cordova needs your game to be available in the www folder. This folder will be the main entry point of your app and requires an index.html to be there in order to run.
You can specify a different entry point in your config.xml (line #12)

### Run cordova
Once all is setup you can initialize your cordova project by running:
```bash
ale@NL0NTB032:/path/to/my/game$ cordova prepare
```

and then building it with:
```bash
ale@NL0NTB032:/path/to/my/game$ cordova build
```

F.A.Q.
------
### Android Studio is complaining about some license thing
In order to build apps, you will need to accept the license agreements of Android SDK components. In order to do this, there are a few ways. Try to see which one works for you.

1) Locate your ANDROID_HOME path. (This is usually ~/Library/Android/sdk or ~/USER/Android/sdk or ~/USER/AppData/Local/Android/sdk) (sdk folder is your ANDROID_HOME).

You can also see the path if you navigate to "File > Settings > Appearance & Behavior > System Settings > Android SDK" in Android Studio.
Run the code below to accept all the licenses that are needed;

```bash
ale@NL0NTB032:~$ ~/ANDROID_HOME/tools/bin/sdkmanager --licenses
```

2) Depending on which SDK version you're using, run the following code in command line;
```bash
ale@NL0NTB032:~$ ~/ANDROID_HOME/tools/bin/sdkmanager "build-tools;26.0.1" "platforms;android-26"
```
### How do I force the orientation
Good Question! In the config.xml you can find the following tags:
```xml
<preference name="Orientation" value="" />
```
By default we have configured it to work in landscape. If you want to force portrait you can use **portrait** as value. If you want to let it work in portrait and landscape, you can use **all**.

### How do I build / sign my (Android) app?

Ok , 90% of the internet purely exists to awnser this but here's a quick recap:

First you create a cordova release build, if you skip the release parameter you'll create a debuggable build instead (iOS has no release tag, all builds are debuggable with x-code):
```bash
ale@NL0NTB032:/path/to/my/game$ cordova build android --release
```

Next up is signing and aligning (in that order):

```bash
ale@NL0NTB032:/path/to/my/game$ jarsigner -keystore ~/path/to/my/keystore.keystore ./platforms/android/app/build/outputs/apk/release/app-release-unsigned.apk my-keystore-alias

ale@NL0NTB032:/path/to/my/game$ zipalign -v 4 ./platforms/android/app/build/outputs/apk/release/app-release-unsigned.apk ./android-release.apk
```

Disclaimer
----------
We at Azerion just love playing and creating awesome games. We aren't affiliated with Cordova. We just needed some awesome starter kit to jump-start our HTML5 apps. Feel free to use it for creating apps for your own awesome games!
HTML5 Cordova Starter Project is distributed under the MIT license. All 3rd party libraries and components are distributed under their
respective license terms.
