# Install tvOS for Google TV with a coding agent

Open a coding agent with terminal access on a computer connected to the same network as your TV. Copy the block below. You can also follow the [manual installation steps](README.md#install-on-your-tv).

```text
Install tvOS for Google TV on my TV. Do the computer-side setup for me and give me one short instruction at a time when I need to use the remote or enter a code.

1. Use https://github.com/bhaveshchow20/tvos-google and read https://github.com/bhaveshchow20/tvos-google#install-on-your-tv. Reuse my checkout if it points to that repo, or clone the project. Check Git, Python 3 and adb locally. Set up the repo's tools/venv and install tools/requirements.txt as the README describes.

2. Walk me through Developer options and ask for the endpoint my TV displays. With Wireless debugging, use adb pair with the pairing port and let me enter the code in my terminal. Then use adb connect with the separate connection port. With Network debugging, connect to the endpoint shown on my TV and have me accept the on-screen authorization. Use adb -s with that exact endpoint for every device command. Set TV_HOST to the connected endpoint and TV_ADB_BINARY=adb for the repo's tools.

3. Verify that adb reports the device as authorized. Read the model and Android version and confirm that it is my Android TV or Google TV device running Android 8.0 or later. Record the current Home component using the README's resolve-activity command. Check for an existing com.gathin.tvhome install with adb shell pm path com.gathin.tvhome. If present, help me save its theme and wallpapers before applying this project's configuration.

4. Use the APK from https://github.com/bhaveshchow20/tvos-google/releases if one is publicly available. Otherwise build from this checkout with (cd launcher && ./gradlew assembleRelease), using JDK 17 and Android SDK platform and build tools 34. The APK is at launcher/app/build/outputs/apk/release/app-release.apk. Install with adb -s "$TV_HOST" install -r "$APK" and confirm success before continuing. If Android rejects the update because of a signing mismatch, explain the conflict and leave the installed app and its data in place.

5. From the repo root, run tools/theme.sh themes/tvos27 with the TV_HOST and TV_ADB_BINARY values from step 2. Then preview with adb -s "$TV_HOST" shell am start -W -n com.gathin.tvhome/.MainActivity. Keep the stock launcher enabled. Have me confirm that the floating dock appears, the D-pad moves between tiles, and selecting the clock opens Control Center. If the theme step fails, diagnose that error before attempting Home setup.

6. After the preview works, ask if I want to make it my default Home. If I do, use the Home app picker when available, or follow the README's set-home-activity and verification steps. If my firmware keeps stock Home, leave the launcher available in preview mode. Skip debloating and changes to unrelated apps.

7. Offer optional features after the basic install works. For TMDB Top Shelf, use a private copy of themes/tvos27 and have me enter tmdb_key locally. For Now Playing, guide me through notification access. For Sleep or supported remote shortcuts, explain the optional accessibility helper and enable it only if I choose it.

Finish with what worked, the saved Home component and how to restore it, and how to disconnect ADB and turn off TV debugging. Keep pairing codes, keys and account details out of chat and logs.
```
