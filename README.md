# Unofficial, unaffiliated and unassociated fork of https://github.com/davemorrissey/subsampling-scale-image-view for internal use in Cryptomator for Android.

> [!IMPORTANT]  
> This project is provided under the terms of the [Apache License, Version 2.0;](LICENSE) while it is made available to the public,
> it is important to note that this repository is **not intended for public use** and therefore **no support** is provided whatsoever.
>
> For a project designed for use by the public, please refer to the [original repository.](https://github.com/davemorrissey/subsampling-scale-image-view)
>
> An excerpt from the README of the original project is reproduced below for your convenience and to provide proper attribution.  
> This project is not affiliated, associated, endorsed by, or in any way officially connected with David Morrissey, or any of their affiliates.

---

# Excerpt from the original README

Subsampling Scale Image View
===========================

A custom image view for Android, designed for photo galleries and displaying huge images (e.g. maps and building plans) without `OutOfMemoryError`s. Includes pinch to zoom, panning, rotation and animation support, and allows easy extension so you can add your own overlays and touch event detection.

The view optionally uses subsampling and tiles to support very large images - a low resolution base layer is loaded and as you zoom in, it is overlaid with smaller high resolution tiles for the visible area. This avoids holding too much data in memory. It's ideal for displaying large images while allowing you to zoom in to the high resolution details. You can disable tiling for smaller images and when displaying a bitmap object. There are some advantages and disadvantages to disabling tiling so to decide which is best, see [the wiki](https://github.com/davemorrissey/subsampling-scale-image-view/wiki/02.-Displaying-images).

#### Demo

![Demo](docs/images/demo.gif)

## Features

#### Image display

* Display images from assets, resources, the file system or bitmaps
* Automatically rotate images from the file system (e.g. the camera or gallery) according to EXIF
* Manually rotate images in 90° increments
* Display a region of the source image
* Use a preview image while large images load
* Swap images at runtime
* Use a custom bitmap decoder

*With tiling enabled:*

* Display huge images, larger than can be loaded into memory
* Show high resolution detail on zooming in
* Tested up to 20,000x20,000px, though larger images are slower

#### Gesture detection

* One finger pan
* Two finger pinch to zoom
* Quick scale (one finger zoom)
* Pan while zooming
* Seamless switch between pan and zoom
* Fling momentum after panning
* Double tap to zoom in and out
* Options to disable pan and/or zoom gestures

#### Animation

* Public methods for animating the scale and center
* Customisable duration and easing
* Optional uninterruptible animations

#### Overridable event detection
* Supports `OnClickListener` and `OnLongClickListener`
* Supports interception of events using `GestureDetector` and `OnTouchListener`
* Extend to add your own gestures

#### Easy integration
* Use within a `ViewPager` to create a photo gallery
* Easily restore scale, center and orientation after screen rotation
* Can be extended to add overlay graphics that move and scale with the image
* Handles view resizing and `wrap_content` layout

## Quick start

**1)** Add the view to your layout XML.

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <com.davemorrissey.labs.subscaleview.SubsamplingScaleImageView
        android:id="@+id/imageView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</LinearLayout>
```

**2a)** Now, in your fragment or activity, set the image resource, asset name or file path.

```java
SubsamplingScaleImageView imageView = (SubsamplingScaleImageView)findViewById(id.imageView);
imageView.setImage(ImageSource.resource(R.drawable.monkey));
// ... or ...
imageView.setImage(ImageSource.asset("map.png"))
// ... or ...
imageView.setImage(ImageSource.uri("/sdcard/DCIM/DSCM00123.JPG"));
```

**2b)** Or, if you have a `Bitmap` object in memory, load it into the view. This is unsuitable for large images because it bypasses subsampling - you may get an `OutOfMemoryError`.

```java
SubsamplingScaleImageView imageView = (SubsamplingScaleImageView)findViewById(id.imageView);
imageView.setImage(ImageSource.bitmap(bitmap));
```

## Photo credits

* San Martino by Luca Bravo, via [unsplash.com](https://unsplash.com/photos/lWAOc0UuJ-A)
* Swiss Road by Ludovic Fremondiere, via [unsplash.com](https://unsplash.com/photos/3XN-BNRDUyY)

## About

Copyright 2018 David Morrissey, and licensed under the Apache License, Version 2.0. No attribution is necessary but it's very much appreciated. Star this project if you like it!
