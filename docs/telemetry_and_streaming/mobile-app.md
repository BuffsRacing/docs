# Mobile App

The app is built using React Native. 

* [GitHub Link](https://github.com/CUBRT/BuffsRacing-Control)
* App Links
	* iOS - Testflight - On Request
	* Android - APK - On Request

## Streaming

Refer to the page on [FFMPEG](../ffmpeg) - [LINK](../ffmpeg)

## Telemetry

### Phone Sensors

#### react-native-geolocation-service

We use this package to request for the device's latitude, longitude, and calculated speed.

Sample code:

```javascript
import Geolocation from 'react-native-geolocation-service';
```

```javascript
Geolocation.getCurrentPosition(
    (position) => {
      var positionCoords = position.coords;
      console.log(positionCoords);
      console.log(positionCoords.latitude);
    },
    (error) => {
      console.log(error.code,error.message);
    }
    )
```


#### react-native-sensors (temporarily removed)

Gives access to the phone's gyroscope and accelerometer

### OBD2REST

Communicates to the Raspberry Pi Zero W to access the OBD-II data

## Components

### `components/layoutStuff.js`

This component defines a section divider with optional header support. The header can be supplied by passing a title attribute.

Example:

```javascript
<Section title="Useless Padding" />
```

## Helper Functions

### Toast Message

```javascript
import Toast from 'react-native-toast-message';
```

```javascript
const toastMessage = (title,message,type="success") => {
  Toast.show({
    type: type,
    position: "top",
    text1: title,
    text2: message
})
}
```

```javascript
toastMessage("Toast Title","Toast Message")
```

### Permissions

Refer to `react-native-permissions`


