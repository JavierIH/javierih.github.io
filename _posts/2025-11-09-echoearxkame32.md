---
title: "EchoEar x Kame32"
date: 2025-11-09
comments: true
categories:
  - robots
tags:
  - kame32
  - echoear
---

In this post I’m sharing a concept project that combines my Kame32 robot with Espressif’s EchoEar conversational device by redesigning the robot’s top cover to include a magnetic connector that provides a direct serial interface between both systems. EchoEar runs the [Xiaozhi](https://github.com/78/xiaozhi-esp32) project, and with a small firmware modification it now sends an emotion identifier over UART each time an emotion is displayed on its screen. The Kame32’s ESP32-based main board listens for these signals and triggers synchronized physical actions, allowing the robot to react in real time to the conversation.

Here you can see the EchoEar mounted on top of the modified Kame32 body. The magnetic connector aligns naturally and keeps the device firmly in place while still being easy to detach.

![echoearxkame32-1](/assets/images/echoearxkame32-1.jpg)

This is the EchoEar unit on its own, showing the printed top piece that integrates the magnetic port.

![echoearxkame32-2](/assets/images/echoearxkame32-2.jpg)

A close-up of the magnetic connector that enables the serial communication between both devices.

![echoearxkame32-3](/assets/images/echoearxkame32-3.jpg)

Finally, the hybrid robot next to a standard Kame32 model for comparison.

![echoearxkame32-4](/assets/images/echoearxkame32-4.jpg)

Also available on: [Printables](https://www.printables.com/model/1475283-echoear-x-kame32-concept),  [Thingiverse](https://www.thingiverse.com/thing:7195505), [Cults3D](https://cults3d.com/:3673074), [MakerWorld](https://makerworld.com/es/models/1977741-echoear-x-kame32-concept)
