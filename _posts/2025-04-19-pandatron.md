---
title: "Pandatron"
date: 2025-04-19
categories:
  - Robots
---

Pandatron is a line-following robot I built back in 2017 as my first step into the world of line-follower competitions. Two years before, I teamed up with Rubén Espino and Javier Baliñas to take part in several events of the spanish national robotics league, [LNRC](https://robotsleague.com/). These events included line-followers, mini-sumos, and humanoid robot battles, where I competed with [Raider](/robots/raider).

![panda](/assets/images/empty.jpg)

Rubén had one of the most iconic bots in the league: Pumatron. This little beast has an insane track record—it's been to tons of events and is probably one of the most awarded line-followers in Spain. So I decided to build my own robot and named it Pandatron, as a nod to Pumatron. It’s not a hardcore competitive bot, but it was the perfect project to learn the fundamentals and get my feet wet.

Pandatron has a self-supporting PCB chassis, and it’s powered by an STM32F103C8T6 microcontroller. The schematic is based on my earlier bot, Ratatron, and it includes eight sensors to detect the black line. For the motors, I went with the good old reliable TB6612FNG driver. The wheels are standard ones from the LNRC scene, with Scaleauto foam tires (great grip for cloth tracks).

As always, everything is open-source, you can find the firmware, PCB files, and printable parts on my [GitHub repo](https://www.github.com/javierih/pandatron).

![Pandatron](/assets/images/pandatron-fondoblanco.jpg)

# BOM
## PCB components

| Label                 | Package       | Value             | Comments              |
|-------------------    |-----------    |---------------    | ------------------    |
| U1                    | SIP 3T        | TR05S3V3          |                       |
| U2                    | SSOP24-P      | TB6612FNG         |                       |
| U3                    | LQFP-48       | STM32F103C8T6     | https://goo.gl/DWbec2 |
| U4-11                 | QRE1113GR     | QRE1113           | https://goo.gl/W69LTh |
| Y2                    | HC-49s        | 8MHz              |                       |
| SW1, SW4              | SKQG          | SPST              | https://goo.gl/RqLESx |
| LED / POWER           | 603           | Green / Red       |                       |
| R1, R2                | 603           | 100Ω              |                       |
| R6, R8                | 603           | 10kΩ              |                       |
| R9, R10               | 603           | 100kΩ             |                       |
| R7, R13, R14, R15     | 603           | 47Ω               |                       |
| RN1, RN3              | Array 603     | 47k               |                       |
| C1, C6                | 603           | 1uF               |                       |
| C2, C3                | 603           | 100nF             |                       |
| C4                    | 603           | 4.7uF             |                       |
| C5                    | 603           | 10nF              |                       |
| C7, C8                | 603           | 20p               |                       |
| C11, C13              | 603           | 0.1uF             |                       |
| C12, C14              | 1206          | 10uF              |                       |
| Female pin header     | 2.54          | 01x08             |                       |

## Other hardware

This parts can be modified by constructor choice.

| Component             | Brand and model               |
|-------------------    |---------------------------    |
| Motors                | Pololu 10:1                   |
| Battery               | Turnigy Nano-Tech 320mAh 2s   |
| Voltage regulator	    | XP Power TR05S3V3             |
| Wheels                | Scaleauto ProComp             |

You will need too a ST-Link V2 programmer (or compatible)

# License
Hardware: CC-BY-SA

Software: GPLv3

