---
title: "Laser Tower"
date: 2014-12-01
excerpt: "A 3D printed pan-tilt turret that tracks targets of different colours with a webcam and points a laser at them. A computer vision project from my master's."
header:
  teaser: /assets/images/laser-tower-square.jpg
comments: true
categories:
  - robots
---

The laser tower of death (*torreta láser de la muerte*) is a turret that aims at targets of different colours, soda cans in principle, and shoots them, at least virtually. I built it in 2014 with David Estévez and Roberto Herrera, as the project for the Computer Vision course of my master's in robotics at Universidad Carlos III de Madrid.

![Laser Tower](/assets/images/laser-tower.jpg){: .align-center width="480"}

The original idea was a turret that actually shot at things. Somewhere along the project we came to the conclusion that building a machine that fires at everything in front of it could be slightly dangerous, especially since, during the tests, its aim wasn't always very accurate. So it got a laser instead.

# The turret

It's a pan-tilt with a webcam on top, so the camera always looks where the turret is pointing. These are the components:

- **Camera:** Logitech C270 HD
- **Servos:** 2x Hitec HS-805BB+
- **Controller:** Arduino UNO
- **Power supply:** 12 V 2 A adapter

The parts were designed in OpenSCAD and printed in ABS on my own printer, a Prusa Air 2. The whole thing is mounted on a tripod.

![The turret and its target area](/assets/images/laser-tower-setup.jpg)

# Software

Both the camera and the Arduino are connected to a computer that runs a Python program. It finds the targets in the image by their colour and uses visual servoing to move the servos and aim at them. David wrote a detailed explanation of the software on his wiki at the time, but sadly it's no longer online.

Here it is in action:

<iframe width="560" height="315" src="https://www.youtube.com/embed/st-i3KdZ-CQ" title="Simple Visual Servoing for Automated Turret Control" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The printable parts and the code are in the [project repository](https://github.com/JavierIH/laserTower) on GitHub.
