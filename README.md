# react-native-image-picker
A React Native module that allows you to use the native UIImagePickerController UI to either select a photo from the device library or directly from the camera, like so:
![Screenshot of the UIActionSheet](https://github.com/marcshilling/react-native-image-picker/blob/master/AlertSheetImage.jpg)

## Install
1. `npm install react-native-image-picker@latest --save`
2. In the XCode's "Project navigator", right click on project's name ➜ `Add Files to <...>`
3. Go to `node_modules` ➜ `react-native-image-picker` ➜ add `UIImagePickerManager.h` and `UIImagePickerManager.m` files
4. Compile and have fun!

## Usage
1. In your React Native javascript code, bring in the native module:

  ```javascript
var UIImagePickerManager = require('NativeModules').UIImagePickerManager;
  ```
2. Use it like so:

  When you want to display the picker:
  ```javascript
  // The first arg will be the options for cusatomize titles in UIAlertSheet, the second is your callback
  // which sends string: type, string: response
  UIImagePickerManager.showImagePicker(null, (type, response) => {

    if (type !== 'cancel') {
      var source;
      if (type === 'data') { // New photo taken -  response is the 64 bit encoded image data string
        source = {uri: 'data:image/jpeg;base64,' + response, isStatic: true};
      } else { // Selected from library - response is the URI to the local file asset
        source = {uri: response};
      }

      this.setState({avatarSource:source});
    } else {
      console.log('Cancel');
    }
  });

  // Customize pt_BR (example)
  UIImagePickerManager.showImagePicker({
      'title': 'Selecione uma imagem para o perfil',
      'cancelButtonTitle': 'Cancelar',
      'takePhotoButtonTitle': 'Tirar foto...',
      'chooseFromLibraryButtonTitle': 'Escolher da galeria...'
    }, (type, response) => {

    if (type !== 'cancel') {
      var source;
      if (type === 'data') { // New photo taken -  response is the 64 bit encoded image data string
        source = {uri: 'data:image/jpeg;base64,' + response, isStatic: true};
      } else { // Selected from library - response is the URI to the local file asset
        source = {uri: response};
      }

      this.setState({avatarSource:source});
    } else {
      console.log('Cancel');
    }
  });
  ```
  Then later, if you want to display this image in your render() method:
  ```javascript
  <Image source={this.state.avatarSource} style={styles.uploadAvatar} />
  ```
