# piio-Gallery

## Installation
---
### Add piio Gallery into your HTML head
On your HTML file add piio.css and piio.js within the ```<head>``` tag like this:
```html
    <link rel="stylesheet" href="../../css/app.css">

    <link rel="preload" href="[BASE-URL]/piio-gallery.js" as="script">
    <script src="[BASE-URL]/piio-gallery.js" type="text/javascript"></script>
```

&nbsp;

### Set up your HTML markup
No special markup is needed to setup the HTML code.
Just wrap your elements inside a container element and assign an id value to it, which will be required as a parameter when initializing the gallery.
If desired, each image tag can be placed inside a div, an anchor tag or a span.
```html
    <div id="piio-gallery">
      <img data-image="your-image-url">
      <img data-image="your-image-url">
    </div>
```
In order to get lazy loading and better performance, instead of placing your images' urls inside the src attribute, place them within a data-image attribute.
&nbsp;

#### What to put on the src attribute of your img tags
The src attribute needs to be present on your img tags in order to have a valid HTML structure and should not be empty.

In order to have a valid HTML structure and a successful integration, we need to add a small image code to the src attribute. Here is the code we are going to add:
```
  src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA"
```
&nbsp;

Now your html markup should look similar to the following code:
```html
    <div id="piio-gallery">
      <img data-image="your-image-url" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA">
      <img data-image="your-image-url" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA">
      <img data-image="your-image-url" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA">
    </div>
```

&nbsp;

###  Variants
When using variants, gallery HTML markup should not have any children elements.
```html
    <div id="piio-gallery">
    </div>
```

Alternatively, another HTML markup must be created. The idea is similar to the gallery container. All variant elements should be wrapped within a container element with an id, which will also be required to initialize the gallery.
Each list should be nested inside a container element with a data-list attribute in the variant HTML markup.
```html
    <div id="piio-variants">
      <div data-list="list-1">
        <img data-image="your-list-1-image-url">
        <img data-image="your-list-1-image-url">
        <img data-image="your-list-1-image-url">
      </div>
      <div data-list="list-2">
        <img data-image="your-list-2-image-url">
        <img data-image="your-list-2-image-url">
        <img data-image="your-list-2-image-url">
      </div>
      <div data-list="list-3">
        <img data-image="your-list-3-image-url">
        <img data-image="your-list-3-image-url">
        <img data-image="your-list-3-image-url">
      </div>
    </div>
```
&nbsp;

### Initilize your Gallery
To initialize your gallery you need to specify the following information in your script file or in an inline script tag before your closing `<body>` tag.

```javascript
    const myGallery = piioGallery.init({
      gallerySelector: "#piio-gallery",
      ...
    });
    myGallery.render();
```
```gallerySelector``` is required.

&nbsp;

In order to customize your gallery you can check the available setting-parameters and add them as shown in the example below.

```javascript
    const myGallery = piioGallery.init({
      gallerySelector: "#piio-gallery",
      variantSelector: "#piio-variants",
      piioDomainKey: "[domain-key]",
      transition: "fade",
      carouselStyle: "thumbnails"
    });
    myGallery.render();
```


&nbsp;

&nbsp;

## Setting Parameters
&nbsp;

### Required Parameters
| Parameter         | Type    | Description
| ----------------- | ------- | -----------
| gallerySelector   | string  | The id of the container element of the gallery. Example:  `"#my-piio-gallery"`
| variantSelector   | string  | The id of the container element of the variants. Example:  `"#my-piio-variants"`


&nbsp;

&nbsp;

### Optional General Parameters
| Parameter         | Type                                       |Description
| ----------------- | ------------------------------------------ |-----------
| piioDomainKey     | string                                     | Your piio account name. It enables the gallery to work with piio image optimization. Example:  `"abcd"`
| themeProps        | [IThemePropsOptions](#IThemePropsOptions)  | Object that overrides the default theme colors.
| transition        | string                                     | The transition effect between slides. Available options: `"slide", "fade", "none"`.  **Default:** `"slide"`

&nbsp;

&nbsp;

### Optional Main Slider Parameters

| Parameter         | Type                                        | Description
|-------------------| --------------------------------------------|------------
| aspectRatio       | string or object                            | The aspect ratio of the main slider. Example-1:  `"3:2"` Example-2: `{ height: 400px}`.  **Default:** `"square"`
| mainNavigation    | string                                      | The aspect of the navigation buttons on the main slider. Available options: `"rectangle", "square", "circle", "radius", "none"`.  **Default:** `"rectangle"`
| zoomProps         | [IZoomPropsOptions](IZoomPropsOptions)      | Object that overrides the default zoom properties.

&nbsp;

&nbsp;


### Optional Carousel Parameters
| Parameter         | Type                                            |  Description
| ----------------- | ----------------------------------------------- | ------------
| carouselOffset    | number                                          | It's the space between the main slider and the carousel. It's measured in pixels.  **Default:** `15`
| carouselPosition  | string                                          | It's the location of the carousel relative to the main slider. Available options: `"left", "top", "right", "bottom"`.  **Default:** `"bottom"`
| carouselStyle     | string                                          | It's the display style of the carousel. Available options: `"thumbnails", "indicators", "none"`.  **Default:** `"thumbnails"`
| indicatorProps    |[IIndicatorPropsOptions](IIndicatorPropsOptions) | Object that overrides the default styles of the indicators. It's applied when `carouselStyle: "indicators"`.
| thumbnailProps    |[IThumbnailPropsOptions](IThumbnailPropsOptions) | Object that overrides the default styles of the thumbnails. It's applied when `carouselStyle: "thumbnails"`.

&nbsp;

&nbsp;

### Responsive Parameters
| Parameter         | Type                                        | Description
| ----------------- | ------------------------------------------- | -----------
| responsive        | [IResponsive](IResponsive)                  | Object that enables different gallery settings according to the device.

&nbsp;

&nbsp;

### Objects

&nbsp;

#### IThemePropsOptions
| Parameter         | Type                                        | Description
| ----------------  | ------------------------------------------- | -----------
| background        | string                                      | Overrides the background color of the theme. Colors must be specified in HSL, HSLA.
| color             | string                                      | Overrides the main color of the theme. Colors must be specified in HSL, HSLA.

Example:

````javascript
themeProps: {
  background: "hsla(234, 76%, 50%, 1)",
  color: "hsla(0, 100%, 100%, 1)",
}
````

&nbsp;

#### IZoomPropsOptions
| Parameter         | Type                                        | Description
| ----------------- | ------------------------------------------- | ------------
| position          | string                                      | Overrides the default position of the flyout zoom. Only works when `zoomProps.type === "flyout"`.  Available options: `"left", "top", "right", "bottom"`.  **Default:** `"right"`
| ratio             | number                                      | Sets the ratio of the image that will be zoomed, referenced to the main slider image.   **Default:** `2`
| type              | string                                      | Sets the type of zoom to use. Available options: `"inline", "flyout", "popup", "none"`.  **Default:** `"inline"`

Example:
````javascript
zoomProps: {
  position: "left",
  type: "flyout",
},
````

&nbsp;

#### IIndicatorPropsOptions
*Only works when `carouselStyle: "indicators"`


| Parameter         | Type                                        | Description
| ----------------- | ------------------------------------------- | -----------
| shape             | string                                      | Overrides the default shape of the indicators. Available options: `"circle", "square", "radius", "line"`.  **Default:** `"circle"`
| size              | number                                      | Overrides the default size of the indicators in pixels. **Default:** `13`
| spacing           | number                                      | Overrides the default margin of indicators in pixels. **Default:** `6`


Example:
````javascript
indicatorProps:{
  shape: "circle" | "square" | "radius" | "line",
  size: <custom_number>,
  spacing: <custom_number>,
},
````

&nbsp;

#### IThumbnailPropsOptions
*Only works when `carouselStyle: "thumbnails"`

| Parameter              | Type                                   | Description
| ---------------------- | -------------------------------------- | -----------
| height                 | number                                 | Sets the height of each thumbnail in pixels.  **Default:** `70`
| margin                 | number                                 | Sets the margin right of each tumbnail in pixels.  **Default:** `10`
| navigationShape        | string                                 | Sets the shape of the carousel navigation buttons. Available options: `"rectangle", "square" ,"circle" ,"radius", "none"`. **Default:** `"rectangle"`
| selectedBorderPosition | string                                 | Sets the border position of the selected Thumbnail. Only works if `selectedStyle: "border"`. Available options: `"left", "top", "right", "bottom", "all"`. **Default:** `"all"`
| selectedBorderWidth    | number                                 | Sets the border width in pixels. Only works if `selectedStyle: "border"`. **Default:** `3`
| selectedStyle          | string                                 | Sets the displays style of the selected thumbnail. **Default:** `"overlay"`
| width                  | number                                 | Sets the width of each thumbnail in pixels.  **Default:** `70`

Example:
````javascript
thumbnailProps: {
  height: 80,
  margin: 15,
  navigationShape: "circle",
  selectedBorderPosition: "all",
  selectedBorderWidth: 4,
  selectedStyle: "border",
  width: 120,
},
````

&nbsp;


#### IResponsive
| Parameter              | Type                                   | Description
| ---------------------- | -------------------------------------- | -----------
| tablet                 | Object                                 | All optional Main Slider parameters or Carousel parameters.
| mobile                 | Object                                 | All optional Main Slider parameters or Carousel parameters.

Example:
````javascript
responsive: {
  tablet:{
    carouselPosition: "right",
    carouselStyle: "indicators",
    mainNavigation: "rectangle",
    zoomProps: {
      type: "popup",
    },
  },
  mobile:{
    carouselPosition: "left",
    carouselStyle: "none",
    mainNavigation: "circle",
    zoomProps: {
      type: "inline",
    },
  }
},
````
