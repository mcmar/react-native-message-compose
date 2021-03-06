# react-native-message-compose
React Native library for composing Message / SMS / Text. Wraps MFMessageComposeViewController for iOS and Intent for Android.

For composing email, check out [joonhocho/react-native-mail-compose](https://github.com/joonhocho/react-native-mail-compose).

## Getting started

Tested with React Native 0.43.x.

`$ react-native install react-native-message-compose`


## Android (Manual Installation)
Theses steps are automatically done by `react-native install`.

 - Add to your `{YourApp}/android/settings.gradle`:
```
include ':react-native-message-compose'
project(':react-native-message-compose').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-message-compose/android')
...other modules
```

 - Modify your `{YourApp}/android/app/build.gradle`:
```
dependencies {
    compile project(':react-native-message-compose') // Add this
    ...other modules
}
```

 - Modify your `{YourApp}/android/app/src/main/java/com/{YourApp}/MainApplication.java`:
```
...
import com.reactlibrary.messagecompose.RNMessageComposePackage; // Add this
...
public class MainApplication extends Application implements ReactApplication {
...
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new RNMessageComposePackage() // Add this
          ...other modules
      );
    }
```

## iOS (Required)
These steps MUST be done manually. They are NOT done by `react-native install`.

- Make sure you have a Swift Bridging Header for your project. Here's [how to create one](http://www.learnswiftonline.com/getting-started/adding-swift-bridging-header/) if you don't.
- Open up your project in xcode and right click the package.
- Click `Add files to '{YourApp}'`.
- Select to `{YourApp}/node_modules/react-native-message-compose/ios/RNMessageCompose`.
- Click 'Add'.


Add to your Swift Bridging Header, `{YourApp}/ios/{YourApp}-Bridging-Header.h`:
```
#import <React/RCTBridgeModule.h>
#import <React/RCTViewManager.h>
#import <React/RCTEventEmitter.h>
```

## Usage
```javascript
import MessageCompose from 'react-native-message-compose';

// later in your code...
async sendMessage() {
  try {
    await MessageCompose.send({
      recipients: ['1234567890'],
      subject: 'This is subject',
      body: 'This is body',
      // ![NOTE] SMS attachments are not supported in Android.
      attachments: [{
        filename: 'mytext', // [Optional] If not provided, UUID will be generated.
        ext: '.txt',
        mimeType: 'text/plain',
        text: 'Hello my friend', // Use this if the data is in UTF8 text.
        data: '...BASE64_ENCODED_STRING...', // Or, use this if the data is not in plain text.
      }],
    });
  } catch (e) {
    // e.code may be 'cannotSendText' || 'cancelled' || 'failed'
  }
}
```


## LICENSE
```
The MIT License (MIT)

Copyright (c) 2017 Joon Ho Cho

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
