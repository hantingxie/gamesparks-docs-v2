---
nav_sort: 5
src: /Getting Started/Creating a Game/AndroidSDK Setup.md
---

# AndroidSDK Setup

## Introduction

This tutorial will walk you through integrating GameSparks with your Android project on the Android Builder IDE. For the example Test Harness project that we supply as a sample:
* The GameSparks Android SDK requires API 8 or greater.
* The Test Harness requires API 11 or greater.

## Source Repositories

The source repositories for the android libraries can be found here:
* [Java  SDK](https://bitbucket.org/gamesparks/gamesparks-java-sdk)
* [Android SDK](https://bitbucket.org/gamesparks/gamesparks-android-sdk)

## Integrating GameSparks into your project

*1.*  In your Project's build.gradle add *classpath "com.github.dcendents:android-maven-gradle-plugin:1.3"* under buildscript dependencies and make sure you reference the latest plugin version number after colon. Add *maven {url "http://repo.gamesparks.net/mvn"}* under allprojects repositories.
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

*2.*  In your module's build.gradle under dependencies, add *compile 'com.gamesparks.sdk:gamesparks-android-client-sdk:0.0.2'*. Make sure you reference the latest SDK version number after the colon. Our sample looks like:

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
        compile 'com.gamesparks.sdk:gamesparks-android-client-sdk:0.0.2'
    }
```

*3.*  Finally, in regards to set up add the following to your AndroidManifest.xml:

```
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
That will ensure that the API is ready to be used.

Now, to initialize the GS module and connect our frontend to our backend! In any of your activity's Java code OnCreate function place the following:

```

GSAndroidPlatform.initialise(this, "YOUR KEY", "YOUR SECRET", false, true);

```

Now, you'll need an API key and secret, which you're given when you create a game on our platform, click [here](/Getting Started/Creating a Game/README.md) for a quick guide to show you how. Once that's done, now you need to start the connection.

To do this, place this code in the activity's:

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

After all this is done, you are ready to use GameSparks API in your project. Details of the API can be found here : [https://api.gamesparks.net/?javasdk#](https://api.gamesparks.net/?javasdk#)
