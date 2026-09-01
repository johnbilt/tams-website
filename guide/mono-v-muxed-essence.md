---
layout: guide
permalink: /guide/mono-v-muxed-essence/
kicker: Guide
title: Guide to Working With TAMS
subtitle: Mono Essence v Muxed Media
hero_image: /images/resources_background.png
---

Creating new content in a TAMS store starts with the creation of the relevant essence flows.  For simplicity in the workflows it is recommended that mono-essence flows are used.  This means separating audio and video into separate segments and registering them under separate flows.

The separation means that for workflows where multiple video resolutions share the same audio or for edit by reference workflows the media manipulation is simplified and no duplication is required.  A multi-essence flow is created to represent the combination of video and audio, but for mono-essence workflows this is represented using flow collections and no segments are directly registered to the multi-essence flow.

It is possible to use muxed media files where the workflow requires this.  In this scenario the muxed media segments are registered directly to the multi-essence flow. It is still necessary to have the separate essence flows as these contain the technical parameters for the essence.  There are also additional container mapping elements added to the essence flows to point to the relevant tracks within the muxed essence files.

![Diagram showing separate media segments compared to muxed media segments](/images/mono_and_muxed_essence.png)

### Multiple Muxed Media Sets
