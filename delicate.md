---
layout: page
title: Delicate Synth
permalink: /delicate/
comments: true
---

Coming Soon~
<3

Delicate Synth will be a fully-routable 8 operator polyphonic FM synthesizer LV2 plugin. It is designed to fit both the needs of musicians as well as developers by being efficiently embeddable in any real-time application with floating point support.

For developers, it will be [ISC-licensed](https://opensource.org/licenses/ISC), allowing it to be used in free or proprietary software.

Unfortunately, I am not ready to share it yet. I am still ironing out how its basic architecture will work, but it has made some progress. This is what it can do so far.

* Efficiently routes 8 operators into one another using a single matrix multiplication
* Does not link against the standard C math library, and never will
* Embeds a 256 point lookup table that fits nicely in the CPU cache (May use 128 or even 64 point further down the line if it doesn't introduce unacceptable distortion)
* Uses circular interpolation for alias-free sine wave audio
* Processes basic midi note messages and changes pitch accordingly

However, it still needs work before I am ready to upload it.

* Does not parse midi velocity, pitch, or modwheel
* No envelope generator of any kind yet implemented
* Unsure of how many envelope stages will be necessary, or if developers should choose at compile time
* Unsure if linear or logarithmic envelopes should be used, or if developers should choose at compile time
* Unsure of how envelopes should be routed inside the plugin
* Unsure if LFOs should be implemented explicitly, or if timing information should be passed to main oscillators
* Unsure how polyphony should be handled in an efficient manner
* No GUI implemented, although this will definitely be a separate binary, maybe even a separate project. This is a feature for musicians

Here is an image of it working in Ardour.

<img src="http://i.imgur.com/nnBSmNG.png" width="800px" height="auto" />

-Jordan Halase
