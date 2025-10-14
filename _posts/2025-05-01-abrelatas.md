---
title: "Abrelatas"
date: 2025-05-01
categories:
  - robots
---

Abrelatas is my 1lb combat robot, built in 2023 for the robot combat tournament at [OSHWDem](https://www.oshwdem.org/). It's a 4-wheel drive vertical spinner, mostly 3D printed.

![Abrelatas](/assets/images/abrelatas9.jpg)

It’s a fairly simple build, there’s no microcontroller onboard. Everything is directly connected to the receiver, and all motor directions, acceleration curves, etc., are set up on the transmitter side.

| ![Abrelatas](/assets/images/abrelatas6.jpg) | ![Abrelatas](/assets/images/abrelatas5.jpg) |
| ![Abrelatas](/assets/images/abrelatas2.jpg) | ![Abrelatas](/assets/images/abrelatas3.jpg) |

I designed two versions of the blade: one symmetric and one asymmetric. Using FreeCAD, it’s easy to calculate the center of mass, so I decided to go with a single-tooth asymmetric blade. A single tooth increases the chances of hitting the opponent with full energy on each rotation. The blades were cut in 3mm carbon steel using [LaserBoost](https://www.laserboost.com/), a service I highly recommend.

![Abrelatas](/assets/images/abrelatas1.jpg)

The motor powering the blade is a Sunnysky X2212 980KV, a leftover from an old drone project. It has more torque than the mythical gold motors and comes with prop mounting holes that made it easier to integrate into the design.

For the blade transmission, I used radiocassette belts, not ideal since they’re square-profile and my pulleys are round. But again, it’s what I had on hand. A good future upgrade would be to switch to GT2 belts, or something similar. I intentionally avoided toothed belts: during impacts, it's better if the transmission can slip slightly, acting like a slipper clutch, to protect the motor from damage.

![Abrelatas](/assets/images/abrelatas4.jpg)

The tires are lightweight foam tires from Scaleauto. typically used in line-following robots. Their super low weight allowed me to go for a 4-wheel setup instead of 2.

The drive motors are N20 gear motors with a 30:1 reduction. In hindsight, I would go with 50:1 for more torque and finer control. For motor drivers, I used two 20A RC ESCs, each driving two N20s in parallel. The receiver is a cheap 2.4GHz 4-channel unit compatible with my FrSky Taranis X9D transmitter (definitely overkill for a combat bot, but it’s what I used to fly drones in the past). Power comes from Tattu 3S 450mAh LiPos with a solid discharge rate. They've held up really well so far.

When this version gets destroyed (and it will soon), I’ll redesign it with fewer wheels (probably 2 instead of 4) to shift more weight into the blade and a lower blade gear reduction for more RPM.

You can find all the design files, CAD models, and code on my [GitHub](https://github.com/javierih/abrelatas).

Here is a video of Abrelatas in action:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Tvm4GXLFNsc?si=Lqsd60Rds4Wwfra9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
[]()

# Bill of materials

<style>
table {
  width: 100%;
  table-layout: fixed;
}

td, th {
  width: 25%;
  vertical-align: top;
  text-align: left;
  border: none !important;
  padding: 10px;
}

</style>

| **Item**      | **Description**       | **Units** | **Link**                                                  |
| Spinner motor | Sunnysky X2212 980KV  | 1         | [Aliexpress](https://s.click.aliexpress.com/e/_oldCXqp)   |
| Wheel motors  | N20 600rpm            | 4         | [Aliexpress](https://s.click.aliexpress.com/e/_opPCzkd)   |
| Tires         | Scaleauto             | 4         | [Boxerslot](https://boxerslot.com/neumaticos-slot-124/675-scaleauto-sc-4802-neumatico-espuma-124-procomp-30mm-diamext-20.html)   |
| ESCs          | 20A                   | 2         | [Aliexpress](https://s.click.aliexpress.com/e/_oEAXy3P)   |
| Battery       | Tattu 3S 450mAh       | 1         | [Aliexpress](https://s.click.aliexpress.com/e/_opgXWGv)   |
| Transmitter   | FrSky Taranis X9D     | 1         | [Aliexpress](https://s.click.aliexpress.com/e/_oDKeYXf)   |
| Receiver      | FrSky compatible 4ch  | 1         | [Aliexpress](https://s.click.aliexpress.com/e/_oErHXpn)   |
| Belts         | 120mm                 | 2         | [Aliexpress](https://s.click.aliexpress.com/e/_opPbQEt)   |
| Bearings      | 693ZZ                 | 2         | [Aliexpress](https://s.click.aliexpress.com/e/_onsn3RF)   |
| Screws        | M3x6 (for the blade)  | 8         | [Aliexpress](https://s.click.aliexpress.com/e/_opnr99D)   |
| Screws        | M3x8                  | 28        | [Aliexpress](https://s.click.aliexpress.com/e/_opnr99D)   |
| Screws        | M3x45                 | 3         | [Aliexpress](https://s.click.aliexpress.com/e/_opnr99D)   |
| Nuts          | M3                    | 24        | [Aliexpress](https://s.click.aliexpress.com/e/_oCUTIFp)   |
| Nuts          | M3 nyloc              | 5         | [Aliexpress](https://s.click.aliexpress.com/e/_o2EQdDv)   |


# License
CC-BY-SA


