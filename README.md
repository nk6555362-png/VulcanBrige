# VulkanBridge — GPU Compatibility Monitor (MVP)

This is an honest first milestone for Realme 15 Pro 5G / Android 16: it reports the Vulkan and OpenGL ES capabilities exposed by Android, reads the actual OpenGL ES renderer string, and provides a simple launcher for apps marked by Android as games.

## What this app does
- Reads Android's advertised Vulkan version and hardware level.
- Reads the OpenGL ES version and `GL_VENDOR` / `GL_RENDERER` / `GL_VERSION` strings.
- Lists launchable apps whose `ApplicationInfo.category` is `CATEGORY_GAME` and can start them.
- Targets ARM64-compatible Android installations through the standard Android app toolchain (there are no custom native binaries in this MVP).

## What it does NOT do
- It is not an emulator for Windows, console, or Android games.
- It does not convert Vulkan commands into OpenGL ES commands.
- It does not replace the Qualcomm/Adreno system driver or inject code into other games.
- It cannot force an OpenGL-only game to use Vulkan or make a Vulkan-only game run on an incompatible driver.

A general Vulkan-to-OpenGL ES runtime for arbitrary closed-source Android games is not a normal standalone-app feature. Android restricts loading external graphics layers into non-debuggable production apps on non-rooted devices.

## Build APK with GitHub Actions
1. Create a new GitHub repository and upload the contents of this folder.
2. Open the **Actions** tab.
3. Run **Build Android APK** with **Run workflow**, or push to `main` / `master`.
4. Open the completed workflow run and download the `VulkanBridge-debug-apk` artifact.
5. Extract the artifact and install `app-debug.apk` on the phone. Android may ask you to allow installation from that source.

Build settings: compile SDK 36, target SDK 35, minimum SDK 26, Java 17, Gradle 8.13, Android Gradle Plugin 8.13.0.

## Important validation
This container did not have the Android SDK, Gradle, or network access, so an APK could not be compiled or tested here. The GitHub Actions workflow is included to build it in a standard hosted Android build environment. Test the resulting APK on the actual RMX5101 firmware before treating any capability report as verified.
