# Image

The standard way of displaying images in Lightning is to just specify the `src`. This is the prefered way for your App's local assets (such as background, splash screen, logo and icons).

It's adviced that you optimize an App's local assets, by resizing them to the exact size and quality you will be using them. This will be beneficial for the memory usage of your App.

However when you don't have control over the images you're displaying in your App (because they come from a remote API for example), you can use the Image plugin to resize and crop images.

## Usage

Whenever you need to resize image, import the Image plugin from the Lightning SDK

```js
import { Img } from '@lightningjs/sdk'
```

## Available methods

### Exact

Resizes the image to the exact dimensions, ignorning the ratio.

```js
Img(url).exact(width, height)
```

### Landscape

Resizes the image by width, maintaining the ratio.

```js
Img(url).landscape(width)
```

### Portrait

Resizes the image by height, maintaining the ratio

```js
Img(url).portrait(height)
```

### Cover

Resizes the image in such a way that it covers the entire area. Depending on the orientation (portrait or landscape) of the image it will resize the image by width or by height.

```js
Img(url).cover(width, height)
```

### Contain

Resizes the image in such a way that it is contained within the available area. Depending on the orientation (portrait or landscape) of the image it will resize the image by width or by height.

```js
Img(url).contain(width, height)
```

### Original

Generate an image without resizing it (i.e. use the original dimensions), while still passing it through the proxy (and taking advantage of caching).

```js
Img(url).original()
```

## Image quality

To increase performance on lower end boxes, especially those with limited GPU memory, there exists a `platform` setting to control the _image quality_.
Depending on this setting the images returned by the image server will be _smaller_ than actually displayed on the screen.
Lightning will then _stretch_ the images to fit the desired dimensions. This will save on used GPU memory, but off course impacts the visual quality of the images.

Please note that within the context of the Metrological AppStore this setting is defined as a platform setting _outside_ of the control of the App.
You can however experiment with this during local development via `settings.json`:

```json
{
    "appSettings": {
    },
    "platformSettings": {
        "image": {
          "quality": 50
        }
    }
}
```

The platform setting `image.quality` can be a value between `1` and `100`, where 1 means low quality and 100 equals original image quality.
If preferred this value can also be defined as a string with a percentage-sign appended (i.e. `"75%"`).
