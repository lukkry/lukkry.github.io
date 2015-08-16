---
layout: post
title:  "Writing a 'hello world' application with WebRTC"
date:   2015-08-16 19:59:05
---
Have you ever wondered what it takes to write a web application which is able to send bytes of data between directly connected browsers, in real time? Me too, that’s why I decided to learn about WebRTC (Web Real-Time Communication), a technology which powers many well-known, real-time applications like Google Hangouts or Facebook Messenger.

Even though I use WebRTC everyday when working with the [twilio.js][twilio-js] library, I don’t deal with it directly, because it’s all wrapped in Twilio API.

The best way to learn a new technology is to just use it, so I’ve decided to write a simple video application, where WebRTC is used to connect peers (browsers) and send audio and video data between them. You can see it in action at [webrtc.lukkry.info][webrtc]. The code is on [GitHub][webrtc-sandbox].

I am by no means a WebRTC expert and this is not a WebRTC tutorial. It's mainly meant as a reminder for how I implemented that particular application, so I can do it again once I've forgotten.

## What is WebRTC?
"WebRTC is a free, open project that provides browsers and mobile applications with Real-Time Communications (RTC) capabilities via simple APIs." - webrtc.org

One of the nicest things about WebRTC is that it is built in into all major browsers (except Safari and IE) so users are not forced to install any additional plugins. If you’re doing any real time communication on the web using Flash or Java, it might be a good fit for you.

It’s worth noting that WebRTC is not a protocol, it’s a technology which requires many different protocols, like ICE, STUN, TURN, SDP etc., in order to work.

## WebRTC Sandbox Architecture Overview

The following description illustrates how the WebRTC Sandbox uses WebRTC to connect peers and send media (audio and video) between them.

The whole system can be divided into three separate parts:

* Signaling server - “Go” application,
* Browser - JavaScript application,
* STUN server - provided by Google.

<img class="center-image webrtc-high-lvl-overview" src="/assets/webrtc_high_level_v1.svg" />

A signaling server is used to setup a direct connection between peers and once the connection is established, that server is not used anymore. The STUN server is used to determine the IP address of each peer.

The signaling server is responsible for:

* generating a UUID, a universally unique identifier, which is assigned to each peer, so the future messages can be routed easily,
* sending messages between peers.

Each peer connects to the server via WebSocket and can send messages in the following format:

{% highlight ruby %}
type: [peer.connected | peer.disconnected | icecandidate | sdp.offer | sdp.answer]
from: UUID
to:   [UUID | *] # * instructs the server to broadcast the message to all peers.
{% endhighlight %}

Below, you can see a diagram which shows how messages flow between different parts of the system. Remember that some of these actions, like fetching ICE candidates and sending an SDP offer, could happen concurrently.

<img class="center-image webrtc-low-lvl-overview" src="/assets/webrtc_low_level_v1.svg" />

## Sum-up
Learning WebRTC might be a little bit overwhelming at the beginning; it involves many different protocols, think about ICE, STUN, SDP, and you need to remember that some actions could be taken concurrently. However, once you get your head around this, it all turns out to be quite simple, and you’ll be surprised how easily you can send data between directly-connected browsers these days.


## References

* [WebRTC Sandbox code][webrtc-sandbox]
* [webrtc.org][webrtc-org]
* [Getting Started with WebRTC][webrtc-tutorial]
* [WebRTC API][webrtc-api]
* [WebRTC exposed: What we can learn from blackbox exploration of popular voice & video services][webrtc-signal]

[webrtc-sandbox]: https://github.com/lukkry/webrtc-sandbox
[twilio-js]: https://www.twilio.com/docs/client/twilio-js
[webrtc]: http://www.webrtc.lukkry.info
[webrtc-org]: http://www.webrtc.org/
[webrtc-tutorial]: http://www.html5rocks.com/en/tutorials/webrtc/basics/
[webrtc-api]: https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API
[webrtc-signal]: https://www.twilio.com/signal/2015/videos/webrtc-exposed-what-we-can-learn-from-blackbox-exploration-of-popular-voice-video-services
