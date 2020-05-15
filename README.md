# AppStateActiveRepro

A basic app to demonstrate that React Native AppState cannot be used to detect the app being opened from a backgrounded or inactive state when following the [documented instructions](https://reactnative.dev/docs/appstate#basic-usage).

The AppState 'change' event listener cannot reliably be used to detect app state changes because it does not have access to the component's correct `appState` state property.

To reproduce:

- Run the app using either iOS or Android, on a device or simulator/emulator with debugging enabled.
- Close the app
- Reopen the app

You will see the logs stating the appState has changed from 'active' to 'active', rather than from 'inactive'/'background' to 'active'.
'App has come to the foreground!' will not be logged.

You will also notice that the `appState` is always logged as 'active' in the 'change' handler.

## Workaround

Omitting the `[]` from the `useEffect` hook results in the AppState 'change' handler having access to the component's state, meaning the handler functions as expected. This does however mean that the event listeners for the AppState change event are added and removed each time the component rerenders.

An example of this can be seen on the branch titled `workaround`.

Another workaround is to use a class component rather than a functional component.

## React Native Environment Info:

System:

- OS: macOS 10.15.4
- CPU: (12) x64 Intel(R) Core(TM) i7-8750H CPU @ 2.20GHz
- Memory: 83.97 MB / 16.00 GB
- Shell: 5.7.1 - /bin/zsh
- Binaries:
- Node: 12.16.1 - ~/.nvm/versions/node/v12.16.1/bin/node
- Yarn: 1.22.4 - /usr/local/bin/yarn
- npm: 6.13.4 - ~/.nvm/versions/node/v12.16.1/bin/npm
- Watchman: 4.9.0 - /usr/local/bin/watchman
- Managers:
- CocoaPods: 1.9.1 - /Users/laurence/.rvm/rubies/ruby-2.6.5/bin/pod
- SDKs:
- iOS SDK:
- Platforms: iOS 13.4, DriverKit 19.0, macOS 10.15, tvOS 13.4, watchOS 6.2
- Android SDK:
- API Levels: 26, 27, 28
- Build Tools: 28.0.2, 28.0.3
- System Images: android-28 | Intel x86 Atom\*64, android-28 | Google Play Intel x86 Atom
- Android NDK: Not Found
- IDEs:
- Android Studio: 3.6 AI-192.7142.36.36.6241897
- Xcode: 11.4.1/11E503a - /usr/bin/xcodebuild
- Languages:
- Java: 1.8.0_201 - /usr/bin/javac
- Python: 2.7.16 - /usr/bin/python
- npmPackages:
- @react-native-community/cli: Not Found
- react: 16.11.0 => 16.11.0
- react-native: 0.62.2 => 0.62.2
- npmGlobalPackages:
- \_react-native\*: Not Found
