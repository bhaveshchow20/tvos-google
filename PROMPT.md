# Set up tvOS for Google TV with a coding agent

Copy the prompt below into a coding agent running on a computer on the same network as your TV. You can also follow the [manual installation guide](docs/INSTALL.md).

```text
Help me install **tvOS for Google TV** on my Google TV or Android TV. Use the project at https://github.com/bhaveshchow20/tvos-google and read its installation guide at https://github.com/bhaveshchow20/tvos-google/blob/main/docs/INSTALL.md before running commands.

Ask for my TV model, Android version, and the debugging endpoint shown on the TV. Walk me through pairing if my TV uses Wireless debugging. Let me enter the pairing code locally. Select the exact endpoint on every ADB command and confirm that the connected device matches my TV before changing anything.

Record the current Home component and check whether the launcher package `com.gathin.tvhome` is already installed. If I already use that package, help me save my existing theme and wallpapers before replacing them. Use an APK from this project’s Releases or build from the repo. Install with `adb install -r`. If Android rejects the signing key, stop and explain the options without uninstalling anything.

Apply the bundled `themes/tvos27` configuration with the repo’s theme tool, then launch it for preview. Keep the stock Home app enabled. Ask me to check the dock, D-pad focus and Control Center with the physical remote. Only change the default Home app if I ask, and verify that Home opens the new launcher after the change. Leave unrelated apps and system settings alone.

Ask which optional features I want. For TMDB Top Shelf, guide me through entering my key locally in a private copy of the configuration. Enable notification access or accessibility helpers only if I choose the feature that needs it. If a firmware-specific feature fails, tell me which one and leave the working setup in place.

Finish by reporting what was installed and verified, how to restore the previous Home app, and how to turn off debugging on the TV. Keep pairing codes, keys and account details out of logs and chat.
```
