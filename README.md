# DS3: Design For Another World
VR Game for DS3: Design For Another World for CS485-1 Human Computer Interactions Spring 2023 at Emory University 
<br>
Made in Unity `2021.3.20f1`
<br>
By Samantha Lin [@Seraclin](https://github.com/Seraclin), Emma Klein, Muhammad Shahid, Allen Zhang [@theJokerEvoker](https://github.com/theJokerEvoker), Jonathan Kim [@JKim0212](https://github.com/JKim0212)

# Tips and Tricks
I used Unity `2021.3.20f1` on Windows 10 with an iPhone for VR development. And here are some common things I came across. There might be different behavior for MacOS or Android or different versions of Unity.
## General Unity Stuff
* For general VR development with VR headsets (e.g. Oculus, HTC Vive, Valve Index, or any device compatible with [SteamVR](https://store.steampowered.com/app/250820/SteamVR/)) and motion controllers, you should use the [XR Interactions Toolkit](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@2.3/manual/general-setup.html) package. You can also use [XR Device Simulator](https://docs.unity3d.com/Packages/com.unity.xr.interaction.toolkit@2.3/manual/xr-device-simulator-overview.html) to simulate a VR headset. Both packages can be installed via "Tools > Package Manager > XR Interaction Toolkit" and make sure to import the Samples: "Starter Assets" and optionally the "XR Device Simulator". You can find the controls for the device simulator by double-clicking the Default XRI Input Actions asset or opening the Input Manager. The Unity 3D (VR) starting template also comes pre-installed with many of the needed packages but make sure to update them. A good XR tutorial can be found [here](https://www.youtube.com/watch?v=5ZBkEYUyBWQ). 
* [Unity Input](https://docs.unity3d.com/ScriptReference/Input.html) has two seperate systems: the old built-in [Input Manager](https://docs.unity3d.com/Manual/class-InputManager.html) and the new [Input System Package](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.5/manual/index.html). The new `Input System` package (installed via 'Tools > Package Manager > Input System') is a bit more difficult to understand, but it is much more flexible than the older input system, especially for different controller inputs. To check what input system your project is using for your platform(s), go to 'Edit > Project Settings > Player > Other Settings > Configuration > Active Input Handling'. I generally like to set it to "Both" as the XR Interaction Toolkit utilizes the new `Input System`. Here's a [tutorial](https://gamedevbeginner.com/input-in-unity-made-easy-complete-guide-to-the-new-system/#input_system) for the new input system.
* For [Canvas/UI elements](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/UICanvas.html), the 'Render Mode' should be changed to 'World Space'. If you don't do this, UI elements wll appear in the middle of your camera rather than spaced out for VR.

## Git and Version Control
* If you are using Git for version control, make sure to use the default Unity `.gitignore`. You might have to remove the front '/' for the lines `[Ll]ibrary/` to `[Mm]emoryCaptures/` (e.g. `/[Ll]ibrary/` --> `[Ll]ibrary/`) if your project directory isn't in the same directory as your `.gitignore`.
* Unity `.scene` and `.prefab` files don't merge nicely, so make sure only one person is editing them at a time. Otherwise, you will have to deal with merge conflicts.

## Android/iOS VR
* In [Unity Hub](https://unity.com/download) when you're installing the latest LTS version of Unity, make sure to add modules for other platforms (e.g. Android, iOS, etc.). You can alternatively install an older version (e.g. 2019) since some features (e.g. WebVR) have become deprecated in newer versions.
* If you're using an iOS/Android phone, your best bet is to use the [Google Cardboard SDK](https://github.com/googlevr/cardboard-xr-plugin) which is designed for the Google Cardboard. Here's the [documentation for setting it up in Unity](https://developers.google.com/cardboard/develop/unity/quickstart) with a [video walkthrough](https://youtu.be/uBcwVRqOGho). It should come with basic gyroscopic movement and stereoscopic rendering. It was recently updated in 2021 from the now-deprecated GoogleVR, so there's not many tutorials about the new version. 
    * If the Cardboard SDK isn't working, you can try the [older deprecated GoogleVR version](https://github.com/googlevr/gvr-unity-sdk). Here's a [video tutorial for the older version](https://youtu.be/lU1XBhk9NCI), but it most likely requires an older version of Unity (e.g. 2019). There are no guarantees that the older version will work.
    * Here are some [common issues](https://github.com/googlevr/cardboard/issues/140)
    * For Android, make sure in 'Edit > Project Settings > XR Plug-in Management > Android' to have "Initialize XR on Startup" unchecked, and to only have "Cardboard XR Plugin" and "OpenXR" checked.
* A list of possible sensor inputs for Android or iOS can be found [here](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.5/manual/Sensors.html). Generally, you'll want to use the [Gyroscope](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.5/manual/Sensors.html#gyroscope) and [AttitudeSensor](https://docs.unity3d.com/Packages/com.unity.inputsystem@1.5/manual/Sensors.html#attitudesensor). These have to be enabled via script in order to be used. Note: Gyroscope returns a `Vector3`, while AttitudeSensor returns a `Quaternion`.
* If you are directly using the gyroscope and attitudeSensor, you have to do some Quaternion math to rotate them correctly in Unity. A formula for this can be found [here](https://gamedev.stackexchange.com/questions/174107/unity-gyroscope-orientation-attitude-wrong) (note: this formula will only rotate the camera with respect to your device's position rather than to your current position. You can add in an offset to fix this).
    * Another [code snippet](https://forum.unity.com/threads/re-orient-trackedposedriver.499715/) can be useful for reorienting a TrackedPoseDriver to face a certain direction. 
* To build your project to iOS, you MUST have [Xcode](https://developer.apple.com/xcode/), which is only available on MacOS. Thus, you cannot build to an iOS device unless you have a Mac (or an emulator at your own risk). Here's a [tutorial](https://www.youtube.com/watch?v=-Hr4-XNCf8Y) for building to Apple for testing.
* For Android, there shouldn't be a restriction. Here's a [tutorial](https://www.youtube.com/watch?v=Nb62z3J4A_A) for building for Android for testing.
    * If you're getting an error like `Theme.AppCompat.NoActionBar not found`, you might have to check `Custom Main Gradle Template` and `Custom Gradle Properties Template` in 'Edit > Project Settings > Player > Android > Publishing Settings > Build Settings' and edit them accordingly. 
* For viewing on Android/iOS phones without having to build/export your project each time, I recommend using the [Unity Remote](https://docs.unity3d.com/Manual/UnityRemote5.html) app which can be downloaded from your respective app store. Connect your phone via cable to your computer (Note: iOS requires also having iTunes open) and have both the app and Unity editor open (if not detected, you have to replug or restart the editor). In Unity, navigate to "Edit > Project Settings > Editor" and select your device in the Unity Remote section. When you press play in the Editor, you should also see the scene on your phone and receive some inputs from your mobile device. Note: the framerate will be significantly lower on Unity Remote than if you had build it.
    * If you're using Cardboard SDK, Unity Remote won't work, and you will have to build the project in order to test it. 
### The ShineCon Bluetooth Controller
* The ShineCon Bluetooth controller has different behavior between Android and iOS devices. When I paired it to my iPhone, it didn't do anything in VR mode besides change the Volume +/-. When you put it into Music mode on iOS (@+B) it allows you to control music Prev/Next Song with volume controls, but only within the music app. Since it's not "Made for Apple", it's not considered a controller, even though the instruction manual describes it as an "iCade" controller. I observed that it functions like key inputs on iOS when in VR Mode:
    * Up Stick w/e
    * Down Stick x/z
    * Right Stick d/c
    * Left Stick a/q
    * @ button o/g
    * Power button l/v
    * A - volume down
    * X - volume up
    * B - u/f
    * Y - j/n
    * Bumper h/g
* For Android, it seems that the input controls are read differently:
    * Bumper - Joystick1Button0
    * B - Joystick1Button1
    * Y - JoystickButton3
    * The actual Joystick, A, and X weren't detected
* I found the controller can only connect to iOS or Android devices via Bluetooth. I tried to connect it directly to my laptop, but got a 'Driver Error'.
* Unity Remote does not register the controller input, so you may have to build the project directly to the phone for testing.
## WebXR/VR for Unity
* I don't recommend using WebXR since it's very experimental. Unity XR does not support WebGL, so it is not guaranteed to work on certain devices/browsers and is basically unsupported on iOS. Use at your own risk.
* In general, the [WebVR API](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API) is no longer supported and is deprecated. It might still work on some older browsers and devices, but it's unlikely to work on most modern browsers. Also a lot of the packages used are now deprecated and work best on Unity 2019.
* The replacment [WebXR API](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API) is the newer version, but it's still pretty experimental.
* [WebXR Exporter by Mozilla Firefox](https://github.com/MozillaReality/unity-webxr-export) is deprecated and not officially supported by Unity, so there is no guarantee of it working properly for certain platforms/devices or future versions of Unity. Instead there's the [De-Panther WebXR](https://github.com/De-Panther/unity-webxr-export) package which is a basically a maintained version of the Firefox WebXR. It can be used to make WebXR experiences similar to [A-Frame](https://aframe.io/docs/1.4.0/introduction/) using the WebXR API. Although, I found it to be quite buggy and laggy on my iPhone and laptop, so it seems Android devices perform the best. You need to have the WebGL module installed. You also might need to use an older version of Unity. An (outdated) tutorial can be found [here](https://www.youtube.com/watch?v=ck4MDy1pUoQ).
* If you're getting an graphics error, you need to make sure to go to 'Edit > Project Settings > Player > WebGL > Other Settings > Rendering > Color Space' and set the Color Space to "Linear" with the Auto Graphics API unchecked. Alternatively, you can use "Gamma" Color space with Auto Graphics API still checked, but it tends to perform worse.
## Finding Assets
* The [Unity Asset Store](https://assetstore.unity.com/) has a bunch of free 3D assets. A lot of them even come ready-made with animations and scripts, for example this [gun asset](https://assetstore.unity.com/packages/3d/props/guns/modern-guns-handgun-129821). Just make sure it is VR compatible and not too graphics heavy.
* [DevAssets](https://devassets.com/) by [Brackeys](https://brackeys.com/) has many free Unity assets. Brackeys also has many useful Unity tutorials on his [YouTube Channel](https://www.youtube.com/@Brackeys) although he retired from making tutorials in 2020.
* [SketchFab](https://sketchfab.com/3d-models?date=week&features=downloadable&sort_by=-likeCount) also has some free .fbx 3D models, but it's less likely that they will be compatible with Unity.
