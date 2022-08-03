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

## Core

- [Core](https://reactnative.dev/docs/components-and-apis)
- We can communicate with the parent component by passing event handler functions via props
- We can change app configurations by `app.json` file

## Debugging

- cmd + d for developer menu
- Install standalone react dev tools `npm install -g react-devtools`
- `react-devtools`

## Styling

- [Style](https://reactnative.dev/docs/style)
- [Color Reference](https://reactnative.dev/docs/colors)
- StyleSheet.create makes it easier with auto completion and performant
- Uses camel case Eg: backgroundColor rather than background-color
- Can pass an array of styles (last style in the array has precedence)
- Styles do not cascade down to child components
- There're some properties which will not work in Android or iOS.
- Example: borderRadius in Text component will not work in iOS. So we need to wrap it with a View component to get the same styling

## Layouts

- Uses [Flexbox](https://reactnative.dev/docs/flexbox) to create layouts
- Flexbox uses two axis main and cross according flexDirection
- By default flexDirection is column (top to bottom)

- justifyContent: main axis, alignItems: cross axis
- column > main axis: top to bottom, cross axis: left to right
- row > main axis: left to right, cross axis: top to bottom

## Handle Events

- Different props are available in the components which allows to interact and handle events.
- For example `<TextInput onChangeText={goalInputHandler} />` onChangeText expects a function.
- Note that  goalInputHandler is passed and not goalInputHandler(). If we add () it will execute the function at the time the UI is rendered.
- So we only add a pointer to the function without the ().
- When using a setState function we can pass a function which will return the existing state value.
- Rather than directly changing state. currentGoals in this example `setGoalsList(currentGoals => [...currentGoals, enteredGoalText]);`

### ScrollView

- Great for limited content like articles
- But for lists this shouldn't be used as it can have performance impact due to all items in list being refreshed if the UI is updated.

### FlatList

- Items will be lazy loaded so better performance for long lists
- By default it will look for key value in the data item
- If data item doesn't have a key value we can use keyExtractor prop
