Certainly! To use device features like Camera and Location in a React Native app, you can leverage several libraries. Here, I'll provide examples using `react-native-camera` for the camera and `react-native-geolocation-service` for location. Additionally, I'll include an example of using the `react-native-voice` library for voice recognition.

### Camera Example:
1. Install the required packages:
```bash
npm install react-native-camera react-native-geolocation-service react-native-voice
```

2. Link the packages:
```bash
react-native link react-native-camera
react-native link react-native-geolocation-service
react-native link react-native-voice
```

3. Camera Component:
```jsx
// CameraComponent.js
import React, { useState, useRef } from 'react';
import { RNCamera } from 'react-native-camera';
import { View, TouchableOpacity, Text } from 'react-native';

const CameraComponent = () => {
  const cameraRef = useRef(null);

  const takePicture = async () => {
    if (cameraRef.current) {
      const options = { quality: 0.5, base64: true };
      const data = await cameraRef.current.takePictureAsync(options);
      console.log(data.uri); // Display or save the image URI as needed
    }
  };

  return (
    <View style={{ flex: 1 }}>
      <RNCamera
        ref={cameraRef}
        style={{ flex: 1 }}
        type={RNCamera.Constants.Type.back}
        flashMode={RNCamera.Constants.FlashMode.off}
        autoFocus={RNCamera.Constants.AutoFocus.on}
      />
      <TouchableOpacity onPress={takePicture} style={{ position: 'absolute', bottom: 20, alignSelf: 'center' }}>
        <Text style={{ fontSize: 20, color: 'white' }}>Take Photo</Text>
      </TouchableOpacity>
    </View>
  );
};

export default CameraComponent;
```

### Location Example:
```jsx
// LocationComponent.js
import React, { useState, useEffect } from 'react';
import Geolocation from 'react-native-geolocation-service';
import { View, Text } from 'react-native';

const LocationComponent = () => {
  const [location, setLocation] = useState(null);

  useEffect(() => {
    const getCurrentLocation = async () => {
      try {
        const position = await Geolocation.getCurrentPosition(
          (position) => setLocation(position.coords),
          (error) => console.log(error),
          { enableHighAccuracy: true, timeout: 15000, maximumAge: 10000 }
        );
      } catch (error) {
        console.log(error);
      }
    };

    getCurrentLocation();
  }, []);

  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      {location && (
        <>
          <Text>Latitude: {location.latitude}</Text>
          <Text>Longitude: {location.longitude}</Text>
        </>
      )}
    </View>
  );
};

export default LocationComponent;
```

### Voice Recognition Example:
(Note: This example requires setting up a speech-to-text API or using a local solution for voice recognition.)

These examples provide a basic structure, and you may need to customize them based on your app's specific requirements and styling. Make sure to check the documentation for each library for additional configuration options and details.