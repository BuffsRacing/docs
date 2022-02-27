# FFMPEG Configurations

## React Native

To test if FFMPEG is correctly installed, you can use this command to perform a test stream.

`ffmpeg -v verbose -t 05:00 -f lavfi -i testsrc -f lavfi -i testsrc -f lavfi -i testsrc -f lavfi -i testsrc -ar 44100 -r 30 -g 60 -keyint_min 60 -b:v 400000 -c:v libx264 -preset medium -bufsize 400k -maxrate 400k -f flv rtmp://YOUR_RTMP_URL`

Equivalent React Native Code:

```javascript
import { FFmpegKit,ReturnCode } from 'ffmpeg-kit-react-native';

FFmpegKit.execute(`-v verbose -t 05:00 -f lavfi -i testsrc -f lavfi -i testsrc -f lavfi -i testsrc -f lavfi -i testsrc -ar 44100 -r 30 -g 60 -keyint_min 60 -b:v 400000 -c:v libx264 -preset medium -bufsize 400k -maxrate 400k -f flv "${rtmpURL}"`).then(async (session) => {
    const returnCode = await session.getReturnCode();
  
    if (ReturnCode.isSuccess(returnCode)) {
  
      // SUCCESS
  
    } else if (ReturnCode.isCancel(returnCode)) {
  
      // CANCEL
  
    } else {
  
      // ERROR
  
    }
  });
```

An iPhone 12, is able to stream `1280x720` normally on a stable WiFi connection, whereas a Google Pixel 3 streaming `640x480` is still a bit choppy. This could probably be improved by tweaking the ffmpeg command.

### Android

The input device on Android is called `android_camera`. Sadly, FFMPEG on Android cannot use the microphone. Thus, if trying to set the RTMP URL to YouTube, `-i anullsrc` flag needs to be passed to add a silent audio. Otherwise, streaming to YouTube will silently fail.

`ffmpeg -f android_camera -video_size 640x480 -i discarded -r 30 -c:v libx264 -f flv "YOUR_RTMP_URL"`

The hardcoded resolution of `640x480` will be moved to a configurable option in the app.

### iOS

The input device on iOS is called `avfoundation`. 

`ffmpeg -f avfoundation -r 30 -video_size 1280x720 -pixel_format bgr0 -i 0:0 -vcodec h264_videotoolbox -vsync 2 -f flv "YOUR_RTMP_URL"`

The hardcoded resolution of `1280x720` will be moved to a configurable option in the app.

## Linux

As of writing the script, Raspberry Pi OS (64 bit) was still in beta, and `video4linux` was not working properly in our testing. Thus, we tested this command on Raspbian OS, and are in the process of updating the Pi to RPi OS and updating the command.

`ffmpeg -f v4l2 -framerate 25 -video_size 640x480 -i /dev/video0 -c:v libx264 -b:v 700k -maxrate 700k -bufsize 700k -an -f flv rtmp://YOUR_RTMP_URL`
