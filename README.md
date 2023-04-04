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
- Nested text elements will be affected by text related styles from parent

### Adding Shadow

`elevation: 4, //to add shadow only works on android`
`// for ios can use below properties`
`shadowColor: "#000",`
`shadowOffset: { width: 1, height: 5 },`
`shadowRadius: 10,`
`shadowOpacity: 0.5,`
`backgroundColor: 'white',` backgroundColor is required for visibility

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
- Note that goalInputHandler is passed and not goalInputHandler(). If we add () it will execute the function at the time the UI is rendered.
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

### Image

- If it's a network image we add the source equal to an object with the uri.
- `<Image source={{uri: selectedMeal.imageUrl}}/>`
- For network image width and height should be set

### Adding Custom fonts

- `expo install expo-font`
- Can also use google fonts as well using a package
- Use in the App load

  `useFonts({
  'open-sans': require('./assets/fonts/OpenSans-Regular.ttf'),
  'open-sans-bold': require('./assets/fonts/OpenSans-Bold.ttf'),
})`

- Add in the style with the identifier given in the App component `fontFamily: 'open-sans-bold',`
- `useFonts` hook returns an array and it's first element returns if the fonts are loaded

## Dimensions API

- Import from react-native
- Js Object not a component and this can be used anywhere
- `Dimensions.get('window')` screen and window is same in iOS
- In Android screen is whole screen with status bar window is without status bar
- `const deviceWidth = Dimensions.get("window").width;`
- `padding: deviceWidth < 380 ? 12 : 24,` value can be used with ternary operator or directly
- Using percentage values is not helpful as width and height can be different when we want the property values to be same

### Screen Orientation (useWindowDimensions)

- app.json > `"orientation": "portrait",` can be `default` = both or `landscape`
- Can use `const deviceHeight = Dimensions.get("window").height` to determine orientation and add styling
- `marginTop: deviceHeight < 380 ? 30 : 100,`
- Check landscape mode if width > height
- If orientation is not locked(when user changes orientation while using the app) above solution will not work because only once the code will executed when the file code is parsed and executed(when code is outside the component function).
- As a solution for the above issue we can use the `useWindowDimensions` hook provided by react native inside the component function
- `const { width, height } = useWindowDimensions();` this will be dynamic because the hook will keep watching for changes
- Use in JSX code
  `const marginTopDistance = height < 380 ? 30 : 100;`
  `return (`
  `<View style={[styles.rootContainer, { marginTop: marginTopDistance }]}>`

- We can use `useWindowDimensions` hook to have different UI layouts according to the orientation
  `if (width > 500) {`
  `content = (`

### KeyboardAvoidingView

- Can be used to avoid breaking the app when keyboard is viewed
- App view can be wrapped using KeyboardAvoidingView component
- KeyboardAvoidingView has 3 behaviors 'padding', 'height' and 'position'
- Position is best in most use cases as it shift the view.
- But when using position the KeyboardAvoidingView should be wrapped with a ScrollView

`<ScrollView style={styles.screen}>`
`<KeyboardAvoidingView style={styles.screen} behavior='position'>`
`<View style={[styles.rootContainer, { marginTop: marginTopDistance }]}>`

## Platform API

- For platform specific changes we can use Platform from React Native
- `borderWidth: Platform.OS === 'ios' ? 5 : 1,` or
- `borderWidth: Platform.select({ ios: 5, android: 1 }),` more readable
- Can have different files for platform specific changes by adding files with platform extension to filename
- Eg: `Title.android.js` `Title.ios.js` Imports will only need Title `import Title from "../components/ui/Title";`
- Can use same method to have different constant/colors files

### expo-status-bar

- `import { StatusBar } from "expo-status-bar";` in App.js
- To style the status bar `<StatusBar style="light" />` dark, auto, inverted

## Navigation [React Navigation](https://reactnavigation.org/docs/getting-started/)

- `sudo npm install @react-navigation/native`
- `npx expo install react-native-screens react-native-safe-area-context`
- `sudo npx expo install @react-navigation/native-stack`

  `<NavigationContainer>`
  `<Stack.Navigator>`
  `<Stack.Screen name='MealCategories' component={CategoriesScreen} />`
  `<Stack.Screen name='MealsOverview' component={MealsOverviewScreen} />`
  `</Stack.Navigator>`
  `</NavigationContainer>`

- First child (top most screen) inside `<Stack.Navigator>` will be used as the initial screen
- `<Stack.Navigator initialRouteName="CategoriesScreen">` initialRouteName can also be used to set the initial screen

### navigation prop & useNavigation hook

- Using `navigation` prop can be used to forward navigation in child components or
- Can use `import { useNavigation } from "@react-navigation/native"` hook as an alternative to passing navigation prop
- `const navigation = useNavigation();` can be executed in any component function(can be a registered screen or not)

### route prop & useRoute

- route prop is available for any screen component that is registered in the navigator
- It contains an object with params passed to that screen
- `useRoute` hook contains the same behavior and can be used as an alternative instead of the prop
- Can be used in nested component which is not registered as a screen
- Also contains name(name of the screen), key(automatically added unique key of the screen), path(string that opened the screen via deep link)

### [Stack Navigator](https://reactnavigation.org/docs/stack-navigator)

- `@react-navigation/stack` is extremely customizable, it's implemented in JavaScript. While it runs animations and gestures using natively, the performance may not be as fast as a `@react-navigation/native-stack` implementation. native-stack offers native performance and exposes native features such as large title on iOS etc.

### [Drawer Navigator](https://reactnavigation.org/docs/drawer-navigator)

- Similar to Stack navigator configuration
- `const Drawer = createDrawerNavigator()`
- `<NavigationContainer>` > `<Drawer.Navigator>` > `<Drawer.Screen>`
- `drawerIcon: ({color,size}) = > (<Ionicons name="home color={color} size={size} />)` Add add icon
- Can use navigation prop `navigation.toggleDrawer()`
- Can fully customize using own components

### [Bottom Tabs Navigator](https://reactnavigation.org/docs/bottom-tab-navigator)

- `const BottomTab = createBottomTabNavigator()`
- `<NavigationContainer>` > `<BottomTab.Navigator>` > `<BottomTab.Screen>`
- Can render a fully customized tab bar

#### Customize Screens

- We can use `<Stack.Screen options={{}}` prop to customize specific screens [stack-navigator options](https://reactnavigation.org/docs/native-stack-navigator#options)
- If we need to apply same customizations to all screens add them to the navigator `<Stack.Navigator screenOptions={{}}`
- To dynamically set options we can pass an arrow function and get route and navigation properties by react navigation, and it should return an options object

  `<Stack.Screen`
  `name='MealsOverview'`
  `component={MealsOverviewScreen}`
  `options={({route, navigation}) => {`
  `const title = route.params.title`
  `return {`
  `title: title`
  `}`
  `}}`
  `/>`

- As an alternative `navigation.setOptions({ title: categoryTitle });` can be used. It should be used in useEffect/useLayoutEffect
- useLayoutEffect is used to run the effect simultaneously with the component function

#### Add header buttons

- Header button can be added through the `Stack.Screen options` or from the screen `navigation.setOptions`

`<Stack.Screen`
`name='MealDetail'`
`component={MealDetailScreen}`
`options={{`
`title: "Meal Detail",`
`headerRight: () => {`
`return <Button title='Save' />;`
`},`
`}}`
`/>`

- or

`useLayoutEffect(() => {`
`navigation.setOptions({`
`headerRight: () => {`
`return <Button title='Save' onPress={headerButtonPressHandler} />;`
`},`
`});`
`}, [navigation, headerButtonPressHandler]);`

## Nested Navigators

- When nesting navigators each navigator brings in a header, can be hidden
- [Check commit](https://github.com/tanu31195/react-native-meals-app/commit/ae1ef74e28a87fad635561305f1d3f0a41bc34b1)

## Context API & Redux

- [Redux vs React's Context API](https://academind.com/tutorials/reactjs-redux-vs-context-api)
- [Context API + Hooks](https://academind.com/tutorials/reactjs-context-api-with-hooks)
- [Redux Toolkit](https://redux-toolkit.js.org/tutorials/quick-start)

- [Context API commit](https://github.com/tanu31195/react-native-meals-app/commit/81a4d41efe53721d1cafb0bb652227e399d2aa0b)
- [Redux Toolkit commit](https://github.com/tanu31195/react-native-meals-app/commit/0cb7deb42d5a7871b1647c7f1a0117515610c00a)

## Other Commands

- `expo install expo-linear-gradient`
- `expo install expo-app-loading`
- `sudo npx expo install react-native@0.71.4`
- `sudo expo update 48`
- `npm install react-native-reanimated@1 --save --save-exact`
- `npm install axios`
- `sudo expo publish`

## Expo Router

Use [`expo-router`](https://expo.github.io/router) to build native navigation using files in the `app/` directory.

## 🚀 How to use

```sh
npx create-react-native-app -t with-router
```

## 📝 Notes

- [Expo Router: Docs](https://expo.github.io/router)
- [Expo Router: Repo](https://github.com/expo/router)
- [Request for Comments](https://github.com/expo/router/discussions/1)

`npx create-expo-app@latest -e with-router`

`npm install expo-font axios react-native-dotenv`

`npx expo start --ios`
