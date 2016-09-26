---
nav_sort: 2
src: /SDK Center/Android.md
---

# Android SDK Setup

This tutorial walks you through how to integrate GameSparks with your Android project on the Android Builder IDE.

<q>**Requirements?** The GameSparks Android SDK requires API 8 or greater and the Test Harness requires API 11 or greater for the example test harness project that we supply as a sample.</q>

The source repositories for the Android libraries can be found here:

https://bitbucket.org/gamesparks/gamesparks-java-sdk

https://bitbucket.org/gamesparks/gamesparks-android-sdk

To integrate GameSparks into your project:

*1.* In your Project's build.gradle add:
* Under buildscript dependencies:
  * classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.2'
  * classpath "com.github.dcendents:android-maven-gradle-plugin:1.3"
* Under allproject dependencies:
  * maven {url "http://repo.gamesparks.net/mvn"}

Our example looks like this:

```
buildscript {
  repositories {
      jcenter()
  }
  dependencies {
      classpath 'com.android.tools.build:gradle:1.5.0'
      classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.2'
      classpath "com.github.dcendents:android-maven-gradle-plugin:1.3"
  }
}

allprojects {
  repositories {
      jcenter()
      maven {
          url "http://repo.gamesparks.net/mvn"
      }
  }
}

```

*2.* In your module's build.gradle under dependencies add:
* 'compile 'com.gamesparks.sdk:gamesparks-android-client-sdk:+''.

Our sample looks like:

```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "23.0.2"

    defaultConfig {
        applicationId "com.example.test1"
        minSdkVersion 11
        targetSdkVersion 21
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.txt'
        }
    }
}

dependencies {
    compile 'com.android.support:support-v4:23.1.1'
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'com.gamesparks.sdk:gamesparks-android-client-sdk:+'
}

```

*3.* Finally, in regards to set up, add the following to your AndroidManifest.xml:

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

```

If you try to build your application at this point, you'll receive an error regarding an image clash.

*4.* In the application block in the manifest add:

```
 tools:replace="android:icon"

```

*5.* After adding the line, hover your mouse over it and press *Alt+Enter* on your keyboard to automatically add the necessary code to make this work. That will ensure that the API is ready to be used.

Now to initialize the GS module and connect our frontend to our backend!

*6.* In any of your activity's Java code OnCreate function place the following:

```

GSAndroidPlatform.initialise(this, "YOUR KEY", "YOUR SECRET", false, true);

```

Now you need an API key and secret, which you are given when you create a game on our platform, click [here](/Getting Started/Creating a Game/README.md) for a quick guide to show you how.

*7.* Once that's done, you now need to start the connection. To do that, place this code in the activity's code body:

```
@Override
	public void onStart()
	{
		super.onStart();
		GSAndroidPlatform.gs().stop();
		GSAndroidPlatform.gs().start();
	}

```

The reason we stop the module before we start it is to establish a new connection which works to refresh the connection.

<q>**Done!** After all this is done, you now are ready to use GameSparks API in your Android project. Details of the API can be found [here](/API Documentation/README.md)</q>
