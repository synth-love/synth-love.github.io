---
layout: page
title: Delicate Synth
permalink: /delicate/
comments: true
---

Coming "Soon"
<3

Delicate Synth will be a fully-routable 8 operator polyphonic FM synthesizer LV2 plugin. It is designed to fit both the needs of musicians as well as developers by being efficiently embeddable in any real-time application with floating point support.

For developers, it will be [ISC-licensed](https://opensource.org/licenses/ISC), allowing it to be used in free or proprietary software.

Unfortunately, I am not ready to share it yet. I am still ironing out how its basic architecture will work, but it has made some progress. This is what it can do so far.

* Efficiently routes 8 operators into one another using a single matrix multiplication
* Does not link against the standard C math library, and never will[^1]
* Embeds a 256 point lookup table that fits nicely in the CPU cache
* Uses circular interpolation for alias-free sine wave audio
* Processes basic midi note messages and changes pitch accordingly
* Can do portamento between notes in octaves per second
* Can do polyphonic portamento (!!!)
* Uses differential envelopes[^2]

However, it still needs work before I am ready to upload it.

* Does not parse midi velocity, pitch, or modwheel
* Envelope attack rate and attack height should be key scaled
* Number of voices cannot be changed during runtime
* Unsure of how many envelope stages will be necessary, or if developers should choose at compile time
* Unsure if ports should be eviscerated in favor of LV2 patch messages[^3]
* No GUI implemented, although this will definitely be a separate binary, maybe even a separate project. This is a feature for musicians

Here is an image of it working in Ardour.

<img src="http://i.imgur.com/nnBSmNG.png" width="800px" height="auto" />

Here is a simple audio sample.

<iframe width="100%" height="160" src="https://clyp.it/sm0vzcud/widget" frameborder="0"></iframe>

-Jordan Halase

[^1]: The C standard math library significantly increases the size of the final binary. We absolutely want to stay within L1 CPU cache as much as we can, and we also need to take into account that our plugin will most likely be running alongside other plugins, too. Standard math is also designed to give numerically perfect results, which can use as much as 10x more CPU than we need to get a result that is indistinguishable to our ears. This optimization wouldn't matter for almost any application other than audio plugins, because they generally don't call these functions at least 44100 times per second.

[^2]: Linearity is adjusted by a 'bend' factor which changes the characteristic of an envelope. Linear envelopes give the familiar sounds of the Sega Genesis or old Sound Blaster chips. Logarithmic envelopes have a more organic feeling like the Yamaha DX7.

[^3]: There are already over 100 ports in Delicate Synth that describe the basic state of the FM matrix and operators. Envelope ports have not been added (yet?) and would increase the number of ports by at least an additional 4 envelope stages * 4 properties per envelope * 8 operators = 128 operator properties. All ports must be read to a local value at the beginning of every audio block before being processed, and this has performance implications if each port reads from outside a cache line. Thankfully, unlike other plugin formats like VST, LV2 has a mechanism for transferring all properties through a single port (Atoms) and bringing the number of ports down to single digits. A caveat to this is that it could make a plugin more reliant on a UI to control it, but we would help circumvent this by exposing a Delicate Atom API to developers to make communicating with Delicate Synth easier when either making a UI, or just by talking to it intimately from any point of view without violating UI/plugin separation.
