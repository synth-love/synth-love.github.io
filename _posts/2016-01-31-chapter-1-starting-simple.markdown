---
layout: post
title: "Chapter 1: Starting Simple"
date: 2016-01-31 20:06:42
categories: LV2
---

LV2 plugins are dynamically linked libraries. As with any plugin architecture, this makes beginner's tutorials a bit difficult because there's no dirt-simple "Hello World" example you can do. Your plugin must have everything present to even consider working. So instead of diving right into a programming example, let's go through a high-level overview of what the host needs from your plugin.

## URI?

How do you tell apart one LV2 plugin from another? How do you ensure that an LV2 plugin is *globally unique*? How can you ensure that a project file will load the same plugin across machines? Across plugin versions? Across install directories? File names? What if they break compatibility with previous versions?

The answer is to refer to your plugin by a globally unique identifier, like a string. How do you ensure a string is globally unique? The current convention is to use a web address.

Using a web address has some benefits. It's easier to make sense of rather than mashing on your keyboard for the sake of being unique. You own the web address. You needn't worry about namespace collisions with other developers' plugins. If you want to be useful, you can have that address actually resolve to something, like the page for your plugin.

Just know that using a web address is merely convention. Although

* You will probably get screamed at for using anything other than a web address.
* You will especially get screamed at for using an invalid web address.
* You can possibly get into legal trouble for using someone else's address without permission.

As far as LV2 is concerned, it is *JUST* a string. It is *JUST* a means of making sure your plugin won't get confused with another, or freak out because your plugin is installed in a different folder, or break because it expected a different version of your plugin. It doesn't connect to the internet or even know that it's a web address.

A common way plugin developers get a hold of an address is to simply make a GitHub page for their project and use that as their URI. For simple one-off exercise plugins, you can use [www.example.org](http://www.example.org/)/my_test_plugin_name_here.

## Plugin discovery

LV2 defines [where plugins are installed on the system](http://lv2plug.in/pages/filesystem-hierarchy-standard.html). On Windows, LV2 hosts will scan `%APPDATA%/LV2` and `%COMMONPROGRAMFILES%/LV2`. Of course, you can add paths to hosts if you can't install to the default paths for some reason.

If, for example, I wanted to load [Delicate Synth](/delicate), the host will look for where the plugin by the id "http://delicate.synth.love/" is installed on the system, and then load that. Of course, fancier hosts could show me a list of plugins by their names, and do the URI thing internally.
