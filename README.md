jQuery.imageZoom
============

A jQuery plugin that allows inline zooming and dragging of images. 
Initially written for mobile devices, but also works on desktop (using mouse-wheel to zoom).


Requirements
------------

 - [jQuery 1.6.+](http://jquery.com/)
 - For mobile devices: [hammer.js](https://github.com/EightMedia/hammer.js)
 - For desktop: [jquery-mousewheel](https://github.com/brandonaaron/jquery-mousewheel)


Installation
------------

Grab/Include [hammer.js](https://github.com/EightMedia/hammer.js) for mobile 
and/or [jquery-mousewheel](https://github.com/brandonaaron/jquery-mousewheel) for desktop.

Include `jquery.imagezoom.js` in your code. Example:

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>
<script type="text/javascript" src="javascript/hammer.js"></script>
<script type="text/javascript" src="javascript/jquery.hammer.js"></script>
<script type="text/javascript" src="javascript/jquery.mousewheel.js"></script>
<script type="text/javascript" src="javascript/jquery.imagezoom.min.js"></script>
```

Demo
------------

Here's a [demo](http://bummzack.github.com/jquery-imagezoom/demo/) showing zoom on images as well as a regular DOM element.


Usage
------------

Imagine you have a website with a fixed zoom-level on mobile-devices, using something like:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=0">
```

What if you would like to provide your users with a way to zoom into images nevertheless? Then this plugin is for you.

Ideally, the image is available in a larger resolution than it displays on screen. Example:

```html
<!-- 800x800 image shown as 200x200 on screen -->
<img id="zoomImage" src="http://placekitten.com/800/800" style="width: 200px; height: 200px;"/>
```

Here are some examples how to enable zooming:

```js
// enable zoom on a specific element
$("#zoomImage").imageZoom();

// enable zoom on all images
$("img").imageZoom();

// enable zoom on all images and disable hammer on non-mobile devices (see options)
var isMobile = navigator.userAgent.match(/Mobile/i) == true;
$("img").imageZoom({ disableHammer: !isMobile });
```

To revert the object to a non-zoomable state, use `$(selector).imageZoom("destroy");`:

```js
// disable zoom on images
$("img").imageZoom("destroy");
```

Options
------------

 - `wrapper`, a HTML snippet that should be used as wrapper. Defaults to `"<div></div>"`
 - `wrapperClass`, class that will be assigned to the wrapper. Defaults to `"zoomWrapper"`
 - `minZoom`, minimal zoom level. Defaults to `1`
 - `maxZoom`, maximal zoom level. Defaults to `5`
 - `confine`, whether or not the image should be confined within its original bounds. 
    Eg. if set to `true` you won't be able to scale the image below 100% and only move the image within the bounds. Defaults to `true`
 - `scrollSensitivity`, scroll sensitivity multiplier. Only relevant for desktop. Defaults to `0.2`
 - `hammerSettings`, settings object for the hammer plugin. Defaults to
 
        {
            prevent_default: false,
            swipe: false,
            scale_treshold: 0,
            drag_min_distance: 0
        }
        
 - `disableHammer`, whether or not to disable hammer events. Useful to disable hammer on desktop, even when it's loaded. Defaults to `false`


Limitations
------------

This plugin relies on the CSS3 property `transform` and `transform-origin`. Thus the zooming won't work in a browser that doesn't support transformations.