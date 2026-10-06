# Getting Logs for Bug Reports
Bugs happen. We have logs for that!

Unsure how to do something? Google it.

Screenshots of the logs work too, if copying them is a hassle.

# Android (no PC)
1. Enable Developer Mode on your Android Phone (Settings > About phone > tap Build number 7 times)
2. Open Developer options and enable the Bug report shortcut (adds it to the power menu)
3. Close the game on your phone
4. Launch the game and navigate to where the issue is occurring in game
5. Right after the issue, hold the power button (or the volume down button too, for some devices) and tap Bug report (or Developer options > Take bug report)
6. Wait for the notification. The report is saved in Bug reports
7. Install AOSP Files from the Play Store (a shortcut to Android's built-in Files app, less than 1 MB) and open it
8. Open the sidebar and tap Bug reports
9. Long-press the .zip, tap the three dots at the top right, then Copy to... Downloads
10. Extract the logs (pick the relevant ones), skip to Manually if you don't want to use Termux

### Termux (no PC)
```bash
pkg install unzip
termux-setup-storage
cd ~/storage/downloads
unzip -o bugreport-*.zip -d bugreport
grep -a "OfflineSekaiR" bugreport/dumpstate.txt > sekai_log.txt
grep -a -E "Fatal signal|E CRASH|FATAL EXCEPTION" bugreport/dumpstate.txt > crash_log.txt
```

### Linux / Mac
```bash
unzip -o bugreport-*.zip -d bugreport
grep -a "OfflineSekaiR" bugreport/dumpstate.txt > sekai_log.txt
grep -a -E "Fatal signal|E CRASH|FATAL EXCEPTION" bugreport/dumpstate.txt > crash_log.txt
```

### Windows (POWERSHELL)
```powershell
Expand-Archive bugreport-*.zip -DestinationPath bugreport
Select-String -Path bugreport\dumpstate.txt -Pattern "OfflineSekaiR" | ForEach-Object { $_.Line } | Out-File sekai_log.txt
Select-String -Path bugreport\dumpstate.txt -Pattern "Fatal signal|E CRASH|FATAL EXCEPTION" | ForEach-Object { $_.Line } | Out-File crash_log.txt
```

### Manually (no Termux)
1. Extract the .zip with any file manager or archive app
2. Open `dumpstate.txt` in a text editor (it's huge, 200MB+, so use one that can handle big files)
3. Search for `OfflineSekaiR` and `Fatal signal`
4. Copy the lines around where the issue happened (or screenshot them)

### Tombstones
If the game crashed, there's a crash dump inside the zip in `FS/data/tombstones/`
1. Open the tombstones (ignore the .pb ones) and check the `Timestamp` line at the top
2. Grab the one that matches your crash (Termux/Linux/Mac: `grep -a -H "^Timestamp" bugreport/FS/data/tombstones/tombstone_??`)
3. Attach it with your logs

Bug reports can contain your notifications and account names, so attach only the files above, not the whole zip

# Android (Shizuku rish)
Runs adb-level commands from Termux
Needs Wi-Fi once to start Shizuku, and again after every reboot
1. Install Shizuku (Play Store works) and Termux (from F-Droid or GitHub, not the Play Store)
2. Open Shizuku and start it with Wireless debugging (follow the steps in the app)
3. In Shizuku tap Use Shizuku in terminal apps > Export files. Files will open, pick Termux in the sidebar and tap Use this folder
4. In Termux edit the package name inside the script once
```bash
sed -i 's/PKG/com.termux/g' ~/rish
```
5. Run `sh ~/rish -c id` and tap Allow on the Shizuku prompt. It should print `uid=2000(shell)`
6. Close the game on your phone
7. Run `sh ~/rish -c logcat | grep --line-buffered "OfflineSekaiR" | tee sekai_log.txt`
8. Launch the game on your phone. Navigate to where the issue is occurring in game
9. Press Ctrl+C in Termux when it's done. The logs are in `sekai_log.txt` (or copy the printed lines)

If the game crashed, also run `sh ~/rish -c "logcat -b crash -d" > crash_log.txt`. For tombstones use the bug report route above

# Android (adb)
1. Connect your Android phone to a PC (or use Termux without PC - see INSTALL.md)
2. Enable Developer Mode on your Android Phone
3. Enable USB debugging (wireless too if Termux)
4. Install ADB (https://developer.android.com/tools/releases/platform-tools) on your PC and unzip it (Linux: `sudo apt install adb`, Mac: `brew install android-platform-tools` Termux: `pkg install android-tools`)
5. Navigate to the platform-tools folder and open CMD (Windows) or any new terminal (Linux/Mac/Termux)
6. Close the game on your phone
7. Run `adb logcat | findstr /C:"OfflineSekaiR"` (Windows) or `adb logcat | grep --line-buffered "OfflineSekaiR" | tee sekai_log.txt` (Linux/Mac/Termux)
8. Launch the game on your phone. Navigate to where the issue is occurring in game
9. Copy the logs printed!

# iOS
1. Connect your iOS device to a PC
2. Trust the PC on your device
3. Install libimobiledevice (windows: https://github.com/jrjr/libimobiledevice-windows, there are other versions you can find on Google) and unzip it (Linux: `sudo apt install libimobiledevice-utils`, Mac: `brew install libimobiledevice`)
4. Navigate to the suite path and open POWERSHELL (Windows) or a terminal (Linux/Mac)
5. Close the game on your phone
6. Run `./idevicesyslog | Select-String -Pattern "OfflineSekaiR"` (Windows) or `idevicesyslog | grep --line-buffered "OfflineSekaiR" | tee sekai_log.txt` (Linux/Mac)
7. Launch the game on your phone. Navigate to where the issue is occurring in game
8. Copy the logs printed!
