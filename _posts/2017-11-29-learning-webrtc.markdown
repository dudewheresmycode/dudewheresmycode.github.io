---
layout: post
title:  "Learning WebRTC"
date:   2017-11-29 01:00:00 -0600
categories: programming
---
I spent a good chunk of last weekend learning about the WebRTC framework. It seems pretty cool so far. The main purpose of WebRTC is to facilitate real-time communications in-browser. It uses a peer-to-peer (P2P) approach, which means it can be used without a centralized server layer. This creates a plethora of possibilities for broadcasting P2P data.

I wanted to checkout the audio quality to see if WebRTC could be used for high quality audio transport. Last weekend I built a prototype for a near-real-time wireless audio sender/receiver. The main purpose would be to use a mobile phone as a wireless audio receiver for my laptop. Almost like wireless headphones. After fiddling with some of the capture settings, like turning off settings like `echoCancellation` and `noiseSuppression` I was able to get acceptable music audio quality. I’ll post a tutorial soon.

So far, WebRTC looks promising and I can’t wait to play with it a little more.