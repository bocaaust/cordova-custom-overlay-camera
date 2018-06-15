### Description

Cordova plugin which allows the caller to customise a camera preview, including a custom button and overlaying a mask image in center.

### Using the plugin

- Install plugin.

```
cordova plugin add https://github.com/bocaaust/phonegap-custom-overlay-camera.git
```

- Add custom images for the capture button and mask to your project. The image locations under the cordova www directory cannot currently be modified.

|         Path           |        Description        |
| -----------------------| --------------------------| 
| www/img/cameraoverlay/your_mask_image_file_name.png | The center mask image |
| www/img/cameraoverlay/capture_button.png | The default image for the capture button |
| www/img/cameraoverlay/capture_button_pressed.png | The image for the capture button when tapped |

- Call the plugin from JavaScript. 

```js
navigator.customCamera.getPicture(filename, maskfilename, success, failure, [ options ]);
```

|         Parameter       |        Description        |
| ----------------------- | --------------------------| 
| filename | The filename to use for the captured image - the file will be stored in the local application cache. Note that the plugin only returns images in the JPG format. |
| maskfilename | The filename of center mask image - the captured image will be cliped according to this mask. |
| success | A callback which will be executed on successful capture with the file URI as the first parameter. |
| error | A callback which will be executed if the capture fails with an error message as the first parameter. |
| options | An optional object specifying capture options. |

### Capture options

|         Option       | Default Value |        Description        |
|----------------------|---------------|---------------------------| 
| quality | 100 | The compression level to use when saving the image - a value between 1 and 100, 100 meaning no reduction in quality. |
| targetWidth | -1 | The target width of the scaled image, -1 to disable scaling. |
| targetHeight | -1 | The target height of the scaled image, -1 to disable scaling.  |

### Image scaling

Setting both targetWidth and targetHeight to -1 will disable image scaling. Setting both values to positive integers will scale the image to that exact size which may result in distortion. If the aspect ratio should be respected, supply only the targetWidth or targetHeight and the other will be set based on the aspect ratio.

### Example

```js
navigator.customCamera.getPicture('filename.jpg', 'mask.png', function success(fileUri) {
    alert("File location: " + fileUri);
}, function failure(error) {
    alert(error);
}, {
    quality: 80,
    targetWidth: 120
});
```
