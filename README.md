# PlayCanvasAR - Fast and Easy AR for the Web
PlayCanvasAR makes it *easy* to build *lightning fast* augmented reality applications. With it, you can construct web-based AR applications with *zero programming* using the PlayCanvas Editor. Just drag in your 3D models and watch them appear in AR!

![PlayCanvas Editor](/images/editor.png?raw=true)

But if you want to create something more interactive, you can call on the full power of the [PlayCanvas scripting API](https://developer.playcanvas.com/en/api/).

## Demo
Before you begin, print out the following markers: [Hiro](https://github.com/artoolkit/artoolkit5/blob/master/doc/patterns/Hiro%20pattern.pdf) and [Kanji](https://github.com/artoolkit/artoolkit5/blob/master/doc/patterns/Kanji%20pattern.pdf).

Now click [here](https://playcanv.as/p/eJ1ygzym/) for a demonstration. We recommend running it on mobile. If you use iOS, you'll need iOS 11 which is now in [public beta](https://beta.apple.com/sp/betaprogram/).

## Features

* **Amazing Performance** - PlayCanvasAR delivers 60 frames per second, even on mobile.
* **Marker-based Tracking** - PlayCanvasAR utilizes the amazing [ARToolkit](https://artoolkit.org/), an open source marker-based tracking library. Originally coded in C++, it has been [ported to JavaScript](https://github.com/artoolkit/jsartoolkit5) using [Emscripten](https://github.com/kripken/emscripten).
* **Incredible Visuals** - PlayCanvas provides an advanced WebGL graphics engine. It supports the latest WebGL 2 graphics API and implements Physically Based Rendering to achieve incredible visuals for your AR applications. And yes, [that's open sourced too](https://github.com/playcanvas/engine).

## Getting Started with PlayCanvasAR
1. Create an account on [playcanvas.com](https://playcanvas.com) (if you haven't already).
2. Fork the [AR Starter Kit](https://playcanvas.com/project/481413/overview) project (which contains the latest version of playcanvas-ar.js).
3. Hit the launch button and see AR in action (we recommend using your mobile device!).

## Scripting with PlayCanvasAR

The PlayCanvas Editor allows you to build your AR apps visually. But you may want to create AR powered entities programmatically. Or you may want to build AR apps by simply using the PlayCanvas Engine without the Editor. PlayCanvas AR exposes two script objects: 'arCamera' and 'arMarker'. 'Engine-only' scripting examples can be found in the examples folder.

### arCamera

This code creates an AR-enabled camera:

```javascript
var camera = new pc.Entity("AR Camera");
camera.addComponent("camera", {
    clearColor: new pc.Color(0, 0, 0, 0)
});
camera.addComponent("script");
camera.script.create("arCamera", {
    attributes: {
        cameraCalibration: asset,
        thresholdMode: 0,
        threshold: 100,
        videoTexture: true
    }
});
app.root.addChild(camera);
```

| Attribute | Type | Description |
| --- | --- | --- |
| cameraCalibration | [pc.Asset](https://developer.playcanvas.com/en/api/pc.Asset.html) | Data file containing the calibration properties for the camera to be used. |
| thresholdMode | Number | The thresholding mode to use. The standard ARToolKit options are available: Manual (0), Median (1), Otsu (2), Adaptive (3). Defaults to 0 (Manual). |
| threshold | Number | The binarization threshold is an 8-bit number that is in the range [0, 255], inclusive. The default value is 100, allowing ARToolKit to easily find markers in images that have good contrast. This value is only used when the mode is set to Manual. Defaults to 100. |
| videoTexture | Boolean | Streams the camera feed to a video texture if enabled. Otherwise, a video DOM element is used. Defaults to true. |

### arMarker

This code creates an AR marker entity:

```javascript
var hiro = new pc.Entity("Hiro Marker");
hiro.addComponent("script");
hiro.script.create("arMarker", {
    attributes: {
        pattern: asset,
        width: 1,
        deactivationTime: 0.25,
        shadow: true,
        shadowStrength: 0.5
    }
});
app.root.addChild(hiro);
```

| Attribute | Type | Description |
| --- | --- | --- |
| pattern | [pc.Asset](https://developer.playcanvas.com/en/api/pc.Asset.html) | The marker pattern to track. This can be the Hiro or Kanji markers or a marker you have generated yourself. |
| width | Number | The width of the marker. Defaults to 1. |
| deactivationTime | Number | The time in seconds from when a marker is lost before its children are deactivated. Defaults to 0.25. |
| shadow | Boolean | Enable this option to generate shadows in the plane of the marker that blend with the camera feed. Defaults to true. |
| shadowStrength | Number | Control the strength of the shadow. 1 is full strength and 0 is disabled. Defaults to 0.5. |

## Supported Operating Systems and Browsers
* Android 4.0+ (Chrome 21+)
* iOS 11+ (Safari 11+, Chrome 21+, Firefox 17+)
* Windows XP+ (Chrome 21+, Firefox 17+, Opera 18+, Edge 12+)
* macOS (Safari 11+, Chrome 21+, Firefox 17+, Opera 18+)
* Linux (Chrome 21+, Firefox 17+, Opera 18+)

## Join the fun!
AR is fun, so why not get involved? Find a bug? Need a feature? Want to contribute something? Add an issue!
