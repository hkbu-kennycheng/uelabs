# Lab 6 Development and Virtual reality

We would use the our previous project, making it support VR and develop it to our mobile devices.

# Android Development Setup

Some essential setup are required for deploying Android application in Unreal Engine, for example installing the Android Software Development Kit (SDK) and Native Development Kit (NDK) etc. Unreal Engine provides a script helping us to automate this process.

## Running SetupAndroid script

Please navigate to the Unreal Engine installation location. The default location is **`C:\Program Files\Epic Games\UE_4.25` for Windows**, and **`/Users/Shared/UE_4.25` for MacOS**. Under **`Engine -> Extras -> Android``**, please run **SetupAndroid.bat for Windows**, or **SetupAndroid.sh for MacOS**.

```bash
SUCCESS: Specified value was saved.

SUCCESS: Specified value was saved.
Press any key to continue . . .
```
The process is finished if you see the above message in Console output.

## Project Settings

In the creation of our previous project, we selected Desktop Computer as the target hardware. Thus, we need to reconfigure it, making the project targeting Mobile or Tablet device. You may found the settings in **Target Hardware** under **Project Settings**.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab6/Project%20Settings%2014_8_2020%208_37_48%20am.png?raw=true)

## Try 

# Google VR Setup


## Adding Plugin

Unreal Engine provide us a lot of plugins, in order to extend functionalities of the Unreal Engine. We could install the plugins via `Edit -> Plugins` on the top menu bar.

Please open up the plugins dialog, search for **Google VR** and **check the Enabled checkbox** to enable it.

![](https://github.com/hkbu-kennycheng/uelabs/blob/master/lab6/googlevr.png?raw=true)

### Project Settings for Google VR plugins

Here are the settings required for Google VR. They are located in in `Project Settings -> Platforms -> Android`.

![](https://docs.unrealengine.com/Images/Platforms/VR/GoogleVR/QuickStart/GVRQS_Config_Now_00.webp)


![](https://docs.unrealengine.com/Images/Platforms/VR/GoogleVR/QuickStart/GVRQS_SDK_Version_00.webp)

![](https://docs.unrealengine.com/Images/Platforms/VR/GoogleVR/QuickStart/GVRQS_Build_arm64_Support_00.webp)

![](https://docs.unrealengine.com/Images/Platforms/VR/GoogleVR/QuickStart/GVRQS_GoogleVR_Options_01.webp)

## Checking requirements for your phone

In order to run the application, we need a phone or tablet with 64bit processor. [Droid Information](https://play.google.com/store/apps/details?id=com.inkwired.droidinfo&hl=en) is an application to show your Android System information.

![](https://lh3.googleusercontent.com/t7UNvCaNXUD85WbZxAlSalKbaYqU1QrlIOLT69gUhdU55g12b2O9aMwkKkjCfk3PHA)

In the System tab, please find **Instruction Sets**. Showing **arm64-v8a** means a 64bit processor, otherwise it would not support Google VR.

## Launch the Application in your phone

We have just finished the setup, and finally we could launch the project on our mobile device. Please select your mobile device under `Launch Options -> ...`, you will find your device there. 

