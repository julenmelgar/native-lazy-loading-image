# Image lazy loading

## Browser compatibility

```<img loading=lazy>``` is supported by most popular Chromium-powered browsers (Chrome, Edge, Opera), Firefox and the implementation for WebKit (Safari) is in progress. caniuse.com has detailed information on cross-browser support. Browsers that do not support the loading attribute simply ignore it without side-effects.

![Image of Yaktocat](https://carlosazaustre.es/static/8f2aa9ce993325615e213b44baf06dd8/7d769/lazy-loading-images-caniuse.png)

## The loading attribute

```
<img src="image.png" loading="lazy" alt="…" width="200" height="200">
```

Here are the supported values for the loading attribute:

* ```auto```: Default lazy-loading behavior of the browser, which is the same as not including the attribute.
* ```lazy```: Defer loading of the resource until it reaches a calculated distance from the viewport.
* ```eager```: Load the resource immediately, regardless of where it's located on the page.

## Images should include dimension attributes

While the browser loads an image, it does not immediately know the image's dimensions, unless these are explicitly specified. To enable the browser to reserve sufficient space on a page for images, it is recommended that all <img> tags include both width and height attributes. Without dimensions specified, layout shifts can occur, which are more noticeable on pages that take some time to load.


```<img src="image.png" loading="lazy" alt="…" width="200" height="200">```

Alternatively, specify their values directly in an inline style:


```<img src="image.png" loading="lazy" alt="…" style="height:200px; width:200px;">```

The best practice of setting dimensions applies to <img> tags regardless of whether or not they are being loaded lazily. With lazy-loading, this can become more relevant. Setting width and height on images in modern browsers also allows browsers to infer their instrinsic size.

Images will still lazy-load if dimensions are not included, but specifying them decreases the chance of layout shift. If you are unable to include dimensions for your images, lazy-loading them can be a trade-off between saving network resources and potentially being more at risk of layout shift.

While native lazy-loading in Chromium is implemented in a way such that images are likely to be loaded once they are visible, there is still a small chance that they might not be loaded yet. In this case, missing width and height attributes on such images increase their impact on Cumulative Layout Shift.

Images that are defined using the <picture> element can also be lazy-loaded:


```
<picture>
  <source media="(min-width: 800px)" srcset="large.jpg 1x, larger.jpg 2x">
  <img src="photo.jpg" loading="lazy">
</picture>
```

Although a browser will decide which image to load from any of the <source> elements, the loading attribute only needs to be included to the fallback <img> element.

## Info
[web.dev](https://web.dev/native-lazy-loading/#improved-data-savings-and-distance-from-viewport-thresholds)
