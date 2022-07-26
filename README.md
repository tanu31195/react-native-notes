# [react-native](https://reactnative.dev)

- React.js + React native --> Real Native Mobile Apps (iOS/ Android)
- React itself is platform agnostic.
- react-dom adds web support.
- react-native adds react components, handle compilation, expose native platform APIs to JavaScript
- [Expo Docs](https://docs.expo.dev)

## Under the hood

- RN components(Views, TextInput) are compiled to real native app
- JS logic is not compiled
- JS logic is running in a JS thread, hosted by RN in the app
- No CSS, can use inline or StyleSheet objects (Syntax is based on CSS and only a subset is supported)

## Expo CLI VS RN CLI

- Expo CLI or React Native CLI can be used to create a new app
- Expo offers a managed app development workflow making it very convenient and easier
- RN CLI bare bone development
- Can eject out of expo anytime

## Setup

- [Setting up the development environment](https://reactnative.dev/docs/environment-setup)
- Install node
- `sudo npm install -g expo-cli`
- `expo --version`
- `expo init ProjectName` select blank workflow
- `npm start` or `expo start`
- app.json has app configuring

For Xcode go to preferences > locations > select command line tools
/Applications/Xcode.app/Contents/Developer/Applications to access simulator
