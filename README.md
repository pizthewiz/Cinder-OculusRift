Cinder-OculusRift
==================

This is (yet another) Oculus Rift block for Cinder, and a collaboration between [Paul Houx](https://github.com/paulhoux) and myself. *Thanks Paul for all the initial work!* It is up-to-date with the 0.4.4 version of the Oculus SDK, and the latest glNext Cinder version. It has been tested with the DK2 only. Both Windows & Mac OS X are supported, although Windows (with direct-mode enabled) is still the prefered platform.

Samples
-----------------
* Basic Sample: Features the standard use case scenario, with all the most common functionalities.
![BasicSample](https://dl.dropboxusercontent.com/u/29102565/oculus/basicsample.png)

* Spherical Stereo: Maps a sample Arnold stereo 360 texture to a sphere. Useful for both live-action & pre-rendered CG content. (Can be easily derived into a video player, using say [Cinder-Hap2](https://github.com/mpcdigital/Cinder-Hap2).)
![SphericalStereo](https://dl.dropboxusercontent.com/u/29102565/oculus/sphericalstereo.png)

* Instanced Stereo: Similar to the basic sample, only it uses instanced stereo rendering as described [here](https://docs.google.com/presentation/d/19x9XDjUvkW_9gsfsMQzt3hZbRNziVsoCEHOn4AercAc/edit).

Usage
-----------------
First, initialize the rift manager in prepareSettings, and disable framerate. (Aslo make sure that msaa 16 is disabled.)

```
hmd::RiftManager::initialize();
settings->disableFrameRate();
```

Create an Oculus Rift instance, and attach it to a window (with vsync enabled preferably).
```
hmd::OculusRift		mRift;
...
mRift.attachToWindow( app::getWindow() )
```

The OculusRift class has two cameras: a convenience host camera controling overall head position and orientation, and an active eye camera which is updated by the SDK according to the tracked orientation & position. Their transformations are composed and can be queried from hmd::OculusRift.


In the draw() loop, iterate over each eye (enabling it) and draw your scene as follows:
```
for( auto eye : mRift.getEyes() ) {
		mRift.enableEye( eye );
		drawScene();
}
```

To avoid judder, make sure you hit **75fps**!

TODO:
* Integrate and test Anttweakbar's GUI
* Incorporate Oculus's VST plugin (work is already done)