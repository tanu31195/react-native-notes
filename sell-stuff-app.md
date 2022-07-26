# react-native-sell-stuff-app

## Notes

React native can only return one component so we can wrap components using React.Fragment
    <React.Fragment>
        ...
    </React.Fragment>
or we can use `<> ... </>`

Multiples styles can be passed as an array
`style={[styles.button, {backgroundColor: colors[color]}]}`

Images
Below line tries to load the image(path/url) dynamically. RN cannot determine which image to bundle
`<Image style={styles.image} source={require(image)} />`

To solve this we can pass the require in the image prop(require('path'))
`<Image style={styles.image} source={image} />`

FlatList
A unique key is required for every item in the list. We can use the below function to set it if the default **item.key** is unavailable
`keyExtractor={}`

SafeAreaView
In iOS this will work but for Android we need to set padding. For that we can use the Platform and StatusBar APIs.
`paddingTop: Platform.OS === 'android' ? StatusBar.currentHeight : 0`
Another alternative is to use **Expo Constants**
`expo install expo-constants`
`import Constants from 'expo-constants'`
and add padding
`paddingTop: Constants.statusBarHeight`
When using SafeAreaView with the Constants.statusBarHeight padding will have no impact

<https://docs.expo.io/versions/latest/>
[React Native Gesture Handler](https://docs.swmansion.com/react-native-gesture-handler/)
`expo install react-native-gesture-handler`
When we use **expo install**, it will make sure the library that is installed to be compatible with the version of expo that we are using
If we're using a library that is part of the expo eco system it's better to use **expo install**

Simply passing a reference of the component, we cannot set props this way
`renderRightActions={ListItemDeleteAction}`
Pass a function and render the component so we can pass props
`renderRightActions={() => <ListItemDeleteAction />}`

If key and value are same as shown below (Check Icon Component),
`backgroundColor: backgroundColor`
we can just use the shorthand value
`backgroundColor`

<https://icons.expo.fyi/>

## Inputs

### TextInput

    <TextInput
    style={styles.textInput}
    placeholder="Pass code"
    onChangeText={text => setFirstName(text)}
    keyboardType="number-pad"
    maxLength={5}
    keyboardAppearance='dark'
    clearButtonMode='always' //only works on iOS
    secureTextEntry //this is same as secureTextEntry={true}
    keyboardType='email-address' 
    placeholderTextColor='green' 
    returnKeyType='emergency-call' 
    textContentType='oneTimeCode'
     />

### Switch

    <Switch 
    value={isNew} 
    onValueChange={newValue => setIsNew(newValue) } 
    ios_backgroundColor='red' 
    thumbColor='blue' 
    />

### Picker

<https://reactnative.directory/?search=picker>
<https://github.com/react-native-picker/picker>

`npm install @react-native-picker/picker --save`

iOS
CocoaPods on iOS needs this extra step

`npx pod-install`

Above picker cannot be used as it's not part of the expo eco system, but we can use it by ejecting expo

`expo install @react-native-community/datetimepicker`

## Forms <https://formik.org/docs/overview>

`npm i formik`

### Form validation <https://www.npmjs.com/package/yup>

`npm i  yup`

<https://stackoverflow.com/questions/55451304/formik-yup-password-strength-validation-with-react>

    .matches(
    /^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{8,}$/,
    'Must Contain 8 Characters, One Uppercase, One Lowercase, One Number and one special case Character')

Use [] to access a property by a name
`<ErrorMessage error={errors[name]} visible={touched[name]} />`

### Importing and re-exporting components (forms/index.js)

    import AppForm from './AppForm'
    import AppFormField from './AppFormField'

    export { AppForm, AppFormField };

or

    export { default as AppForm } from './AppForm';
    export { default as AppFormField } from './AppFormField';
