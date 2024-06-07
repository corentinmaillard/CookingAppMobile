# CookingAppMobile
This app allows you to browse and display a range of cooking recipes. In addition to exploring existing recipes, you can also add your own favorite recipes to the collection. Developed using React Native and Expo.

## Mobile functionality
For the mobile functionality, I chose the camera. And for that I use the package :
- expo-file-system

This is the code that I use for the implementation of the camera in the app>(tabs)>create.tsx file
```cpp
const pickImage = async () => {
    // Ask for permission to access the camera
    const { status } = await ImagePicker.requestCameraPermissionsAsync();
    if (status !== 'granted') {
      // If permission is not granted, show an alert and exit the function
      Alert.alert('Permission Denied', 'We need camera permissions to take a picture.');
      return;
    }

    // Launch the camera to take a picture
    let result = await ImagePicker.launchCameraAsync({
      mediaTypes: ImagePicker.MediaTypeOptions.Images, // Allow only images
      allowsEditing: true, // Allow editing of the image (cropping, etc.)
      aspect: [4, 3], // Aspect ratio for the image
      quality: 1, // Quality of the image (1 is the highest quality)
    });

    // If the user did not cancel the image picking
    if (!result.canceled) {
      // Set the image URI in the state
      setImageUri(result.assets[0].uri);

      // Read the image as a base64 string and set it in the state
      const base64 = await FileSystem.readAsStringAsync(result.assets[0].uri, {
        encoding: FileSystem.EncodingType.Base64,
      });
      setImageBase64(base64);
    }
  };
```

## Run the app
You can run the app with the command line :

```cpp
npx expo start
```

After that you can scan the qr code with the expo mobile app and you will be able to use my mobile app.
