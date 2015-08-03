---
layout: post
title:  "Writing a 'hello world' application with WebRTC"
date:   2015-08-03 19:59:05
categories: webrtc
---
Have you ever wondered what it takes to write a web application which is able to send bytes of data between directly connected browsers, in real time? Me too, that’s why I decided to learn about WebRTC (Web Real-Time Communication), a technology which powers many well-known, real-time applications like Google Hangouts or Facebook Messenger.

Even though I use WebRTC everyday when working with the twilio.js library, I don’t deal with it directly, because it’s all wrapped in Twilio API.

The best way to learn a new technology is to just use it, so I’ve decided to write a simple video application, where WebRTC is used to connect peers (browsers) and send audio and video data between them. You can see it in action at webrtc.lukkry.info. The code is on [GitHub][webrtc-sandbox].

I am by no means a WebRTC expert and this is not a WebRTC tutorial. It's mainly meant as a reminder for how I implemented that particular application, so I can do it again once I've forgotten.

[webrtc-sandbox]: https://github.com/lukkry/webrtc-sandbox
