---
layout: page
title: LV2 Tutorials
permalink: /tutorials/
---

## Prologue

When I first got interested in programming with LV2, the learning experience was a lot of reading the standard and looking through reference documentation, sometimes looking at other plugins on GitHub. The official documentation at [the website](http://www.lv2plug.in/) is good, very good, but it is more "how" and less "why" which can be confusing, especially to those who are familiar programming with VST or AU. This series will showcase all the *big picture* information I wish I had when starting out to ease the process of getting into developing with the LV2 standard.

## What does "LV2" mean?

Right off the bat, I'm telling you that the name isn't important. There is a lot of niche history and potentially misleading information in the name. Just say "LV2" and be happy like you do with "VST", "AU", or "RTAS".

Just know that the LV2 specification is perfectly defined for Linux, OS X, and Windows, and can work on more.

## Why should I care about LV2?

Why would you use LV2 plugins for your project? Why should you even care? After all, VST and AU are pretty much the de facto standards when it comes to plugin-based realtime audio processing.

The first major point is the license. The LV2 API is under the terms of the [ISC License](https://opensource.org/licenses/ISC), which both fits on a PowerPoint slide and is compatible with nearly all licenses. You don't have to register as a third party developer, and you don't have to sign a contract for anything you publish with the standard. You can *just do it,* and then release your plugin or host under any license you choose.

Of course, licensing alone isn't enough to convince anyone to get involved. Here are some questions you might *actually* be asking right now.

* What makes LV2 *unique*?

* What does LV2 do for *me*?

* How does LV2 make *my* job *easier*?

Although, like a coin, there are three sides to this equation. In order to properly answer this, I will split up the answers I give depending on who you are.

## As a musician

* Arbitrary inputs and outputs

Traditional plugin APIs offer some floating point inputs and outputs. They may support MIDI and sometimes side-chain inputs. The first thing that struck me as very useful with LV2 was the ability for plugins to have any number of inputs and outputs. This allows for powerful modular style plugin linking and expressive utilities. It's even possible to make advanced configurations, and save that as a single preset entity that can be loaded into a traditional linear-style effect chain.

* Extensibility for free

Port types are not restricted to audio or midi. They can send and recieve *any* kind of message to one another that they want, and the host doesn't even need to implement nor understand what those messages are. Plugins that understand a type can be plugged into and control one another. An example could be an "arpeggiator" plugin that sends arpeggiated midi, as well as altering the other plugin's envelope and pitch data.

* You no longer have to hate a plugin because of its GUI.

LV2 maintains a strong separation of plugins and the UIs that operate on them. GUIs for LV2 plugins are typically in a separate binary, and sometimes in a separate project altogether. It's even possible for "fanmade" GUIs for certain plugins to exist.

## As a plugin developer



-Jordan Halase
