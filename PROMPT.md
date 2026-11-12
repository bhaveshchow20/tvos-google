# Install tvOS for Google TV with a coding agent

Copy the block into a coding agent with terminal access on a computer on the same network as your TV. Have the remote handy for pairing and the final checks. [Manual installation](README.md#install-on-your-tv)

```text
Install tvOS for Google TV on my real Android TV or Google TV. Run the computer-side steps yourself and continue through verification and cleanup. Give me one short instruction at a time when I need to use the TV remote or enter a pairing code. Ask about optional features after the basic install works.

PREPARE

- Use the project at https://github.com/bhaveshchow20/tvos-google. Reuse a checkout of that repository or clone it. Read https://github.com/bhaveshchow20/tvos-google#install-on-your-tv for platform-specific setup. Use this project's launcher and theme tools.
- Check for Git, Python 3, and Android platform tools. Set up missing prerequisites using the computer's supported installation method. Run python3 -m venv tools/venv and tools/venv/bin/python -m pip install -r tools/requirements.txt from the repo root. In Git Bash on Windows, use tools/venv/Scripts/python.exe for the venv interpreter.
- Ask me which TV to connect to and help me find Developer options and its debugging endpoint. For Wireless debugging, run adb pair with the endpoint from the pairing screen, let me enter the code locally, then run adb connect with the separate connection endpoint shown on the main debugging screen. For Network debugging, connect to the TV's advertised endpoint and tell me when to accept the authorization dialog. If pairing succeeds but connection fails, recheck the connection port and the computer's Local Network access before retrying. If you cannot reach the TV from your environment, tell me how to open the session in a terminal with LAN access.

IDENTIFY AND SAVE THE CURRENT SETUP

- Set TV_HOST to the exact connected endpoint and TV_ADB_BINARY=adb. Use adb -s "$TV_HOST" for all device commands. Confirm get-state returns device, then read ro.product.model, ro.build.version.release and ro.build.version.sdk with adb shell getprop. Confirm the model with me before making changes. This launcher requires Android TV or Google TV with SDK 26 or newer.
- Record the last line of adb -s "$TV_HOST" shell cmd package resolve-activity --brief --user 0 -a android.intent.action.MAIN -c android.intent.category.HOME. Save the component and recovery instructions locally. If it resolves to a chooser or you cannot identify the previous Home app, keep the install in preview mode.
- Run adb -s "$TV_HOST" shell pm path com.gathin.tvhome to check for an existing install. This package is shared with the original CleanYourTV launcher. If present, locate my original theme folder or try pulling /sdcard/Android/data/com.gathin.tvhome/files to a private directory outside the repo. Verify the backup before replacing theme files. If the TV blocks access and I want to keep the current theme, pause before applying the new one. Keep saved configs and screenshots private.

INSTALL AND VERIFY THE LAUNCHER

- Use a public APK from https://github.com/bhaveshchow20/tvos-google/releases when available. Otherwise set up JDK 17 and Android SDK platform 34 and build tools 34, then run (cd launcher && ./gradlew assembleRelease). Use launcher/app/build/outputs/apk/release/app-release.apk as the built APK. Record the release or source commit used.
- Run adb -s "$TV_HOST" install -r "$APK" and verify success. If Android asks for on-screen confirmation, tell me what to accept. If it reports a signing conflict, leave the existing app and its data in place and explain that an in-place update needs the same signing key. If the TV refuses sideloading or the SDK is too old, report the error and stop the install.
- From the repo root, export TV_HOST and TV_ADB_BINARY and run tools/theme.sh themes/tvos27. Confirm it succeeds. Launch the preview with adb -s "$TV_HOST" shell am start -W -n com.gathin.tvhome/.MainActivity. If the theme step or launch fails, diagnose that step before making any Home changes. Leave the stock launcher enabled and leave other TV apps and settings alone.
- Use the repo's screenshot command, tools/venv/bin/python -I tools/tv.py --screenshot <local-file.png>, to capture Home and inspect it for the dock and clock capsule. If the TV cannot provide a usable capture, check the foreground activity and ask me to confirm the screen. Ask me to move focus with the real D-pad and open Control Center from the clock capsule. A screenshot and the remote checks should agree before calling the preview verified.
- If I choose to make it default, use the TV's Home app picker where available. Otherwise run adb -s "$TV_HOST" shell cmd package set-home-activity --user 0 com.gathin.tvhome/.MainActivity. Verify the resolved Home and then ask me to press the physical Home button. Check the foreground activity with adb -s "$TV_HOST" shell dumpsys activity activities if needed. If Home opens the stock launcher or a broken screen, restore the saved Home component and leave the app available for preview.

CUSTOMIZE AND FINISH

- Offer to set dock order and size, appearance, or wallpaper. Use Launcher settings or the keys in https://github.com/bhaveshchow20/tvos-google/blob/main/themes/tvos27/README.md. If I want TMDB Top Shelf, create a private local theme copy and have me enter tmdb_key locally. Apply the copy and verify artwork by resting on a supported app in the dock for a few seconds. For Now Playing or Sleep and remote shortcuts, guide me through the applicable optional permission and have me test the real feature. Keep pairing codes and API keys out of chat, logs, and Git.
- Give me a local recovery note with the exact previous Home component, the command to restore it using cmd package set-home-activity --user 0, and the location of any saved theme. Explain that tools/theme.sh --reset clears the active theme and that reapplying my saved theme restores its configuration and wallpaper.
- Disconnect ADB for this TV and walk me through turning off the debugging modes used for setup. Run python3 tools/adb-closed.py "$TV_HOST" against the TV's actual connection endpoint. If it times out or is unreachable, say the closure check was inconclusive. Report what was installed, what you verified on the TV, what remains optional, and where the recovery note is saved.
```

The setup flow is adapted from [CleanYourTV’s agent prompt](https://github.com/Gathin23/cleanyourtv/blob/main/PROMPT.md).
