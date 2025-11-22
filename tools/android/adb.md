`adb` is a command-line tool that allows you to communicate with an Android device or emulator. 

You can use it to:
- Install or uninstall apps
- Pull (download) or push (upload) files
- Access a device’s shell
- Extract APKs
- Debug apps

🔐 If Your Device Isn't Detected
* Make sure **USB mode** is set to **File Transfer (MTP)**
* Make sure USB drivers are installed (especially on Windows)
* Try `adb kill-server && adb start-server`


---
# Installation 
```
sudo apt install android-tools-adb
```

# Useful ADB Commands
```
adb devices               # List connected devices
adb shell                 # Open shell on the device
adb install app.apk       # Install APK
adb uninstall com.pkg     # Uninstall app
adb logcat                # View device logs
```

# File Operations
```
adb push myfile.txt /sdcard/      # Send file to device
adb pull /sdcard/myfile.txt .     # Get file from device
```

# App & Activity Control
```
# List installed apps
adb shell pm list packages

# Show APK path
adb shell pm path com.example.app                

# Start activity
adb shell am start -n com.example/.MainActivity
```

# List users
```
adb shell pm list users
```

# List all packages for user
```
adb shell pm list packages --user 0
```

# Dump App Info
```
adb shell dumpsys package com.example.app
```
This gives you:
- Permissions
- Activities
- Services
- Broadcast receivers
- Exported components (important for pen testing)

# Take a screenshot
```bash
adb shell screencap -p /sdcard/screen.png
adb pull /sdcard/screen.png
```

# **Extract an APK from installed app**
```bash
adb shell pm path com.example.app
# Output: package:/data/app/com.example.app-1/base.apk

adb pull /data/app/com.example.app-1/base.apk
```

---
# Start Activity 

## Show app package name
```
aapt dump badging movo.apk
```

## List All Activities
```
adb shell dumpsys package com.codlop.mov | grep -i activity
```

##  Launch the Target Activity
```
adb shell am start -n com.codlop.mov/.MainActivity
```

## Check Exported Components
```
adb shell dumpsys package com.example.app | grep -i exported
```

---
# Use logcat

## Find App’s PID
```
adb shell pidof com.example.app
```

## Filter logs for that PID 
```
adb logcat --pid=12345
```
Or dynamically:
```
adb shell pidof com.example.app | xargs -I {} adb logcat --pid={}
```

## Filter by Log Level
```
adb logcat *:E     # Only show Errors
adb logcat *:W     # Warnings and above
adb logcat *:D     # Debug and above
adb logcat *:V     # Verbose (everything)
```

## Search for Sensitive Info
```
adb logcat | grep -i "token"
adb logcat | grep -i "password"
adb logcat | grep -i "exception"
adb logcat | grep -i "jwt"
```

## Clear Logs
```
adb logcat -c 
```

# usage stats

```
adb shell dumpsys usagestats | grep com.instagram.android
```


# Practical Example

Clear logcat
```
adb logcat -c 
```

First run `adb logcat` with no any filter
```
adb logcat
```

Then search for app name to get the app package name.
```
adb shell dumpsys package com.wb.greencar
```

Then find App’s PID
```
adb shell pidof com.wb.greencar
```

Then filter logs for that PID
```
adb logcat --pid=12345
```

# Some targets
```
com.appsbunches.promateapp
com.appsbunches.promate
```

