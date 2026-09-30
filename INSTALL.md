# Install Guide
> [!IMPORTANT]
> **DO NOT EXTRACT the zip.**

# UNOFFICIAL FAN-MADE GUIDE CAN BE FOUND HERE: https://patchednexus.win/glsk/retro
# 中文安装说明 (iOS): https://docs.qq.com/doc/DTVpDV2V4eEpYbE50
> [!IMPORTANT]
> We do NOT provide help or support for installing GridlessSekai Retro beyond these instructions. Do not open any Issues to ask for help, unless it is a bug.

## Android

#### 1. Install the APK
- Transfer `GridlessSekaiRetro.apk` to your device and install it
- **Open the app once**, wait for the title screen or an error, then close it (this creates the data folder)

#### 2. Copy assets

Download `assets_android.zip` to your device's Downloads folder, then copy it to the app's data directory using one of these methods:

NOTE: experienced users, you just need to move the `assets_android.zip` to `/sdcard/Android/data/com.sbuga.gridlesssekair/files/`. You can do this with any method you want (such as root).

> [!TIP]
> Since `0.0.8`, the path `/sdcard/Android/obb/com.sbuga.gridlesssekair/` is also supported. Use this if needed.

**Option A: ADB (PC required)**

Download `assets_android.zip` to your PC, then run:
```
adb push assets_android.zip /sdcard/Android/data/com.sbuga.gridlesssekair/files/assets_android.zip
```

**Option B: Shizuku (no PC, no root)**
1. Download `assets_android.zip` on your device
2. Install [Shizuku](https://shizuku.rikka.app) and start it via Wireless Debugging ([guide](https://shizuku.rikka.app/guide/setup/#start-via-wireless-debugging))
3. Install ZArchiver (or another Shizuku-compatible file manager)
4. Move the file from `Downloads` to `/sdcard/Android/data/com.sbuga.gridlesssekair/files`

**Option C: Termux (no PC, no root)**
1. Download `assets_android.zip` on your device
2. Install [Termux](https://f-droid.org/en/packages/com.termux/) from F-Droid
3. Enable Wireless Debugging in Developer Options, then in Termux:
   ```
   pkg install android-tools
   adb pair localhost:<port>   # use pairing code from Settings
   adb connect localhost:<port>
   adb shell run-as com.sbuga.gridlesssekair cp /sdcard/Download/assets_android.zip ./files/assets_android.zip
   ```

> [!IMPORTANT]
> **DO NOT EXTRACT the zip.**

#### 3. Play
Open the app. The game will "download" assets locally (~30GB), so make sure you have 40GB+ free.

---

## iOS

#### 1. Install the IPA
**SIDELOAD!** Search on Google/YouTube, there are guides! We recommend using [Impactor (NEEDS PC)](https://github.com/claration/Impactor).

Example YouTube searches: `sideload ios no pc`, `sideload ios impactor` (requires PC).

**Do not open the app yet.**

#### 2. Move assets
- Download the assets `assets_ios.zip`
- Open the **Files** app
- Navigate to **On My iPhone** -> **GridlessSekai RETRO**
  - If you don't see it, make sure File Sharing is enabled (most sideloaders have a "Force File Sharing" option)
- Move your downloaded `assets_ios.zip` here.

> [!IMPORTANT]
> **DO NOT EXTRACT the zip.**

#### 3. Play
Open the app. The game will "download" assets locally (~30GB), so make sure you have 40GB+ free.
