---
title: "Legs for humanoid robots (I)"
date: 2016-06-02
excerpt: "The most common way to build the legs of a humanoid robot, and why it overloads the knee servo."
header:
  teaser: /assets/images/humanoid-legs-square.png
comments: true
categories:
  - blog
tags:
  - humanoid
  - tutorial
---

It doesn't matter which board it carries, how long its battery lasts or whether it's made of carbon fibre or PLA: the most important part of a humanoid robot is its legs.

Why am I writing this? It's a way of procrastinating, I guess, but also because there isn't much information online about how to build a humanoid robot. In Japan there are books that explain how to build humanoid robots and how to program them. I wish I could read them; for now I have to make do with looking at the drawings and the Robo-One videos and guessing how they do it.

![Japanese servos](/assets/images/humanoid-legs-servos.png){: .align-right width="300"}

Not only that: many of the servos they use (Kondo, Vstone, Futaba... not exactly the S3003) are not sold outside Japan, and most of them don't even have documentation in English. It's crazy! While the rest of the world pays a fortune for Dynamixel servos, they have options like the ones on the right: daisy chain connection, up to 67 kg·cm in the case of Kondo, metal gears, zero backlash...

After this little rant, let's get started! To keep things clear, I'll use yaw, pitch and roll to name the axis of each servo.

When I describe the configuration of a robot leg, I name the servos from the joint with the body down to the foot. So [Zowi](/robots/zowi) would be Y-R (yaw for the hip servo, roll for the ankle servo) and [Maus](/robots/maus) would be P-P (pitch for both servos).

# Serial legs

We'll start with the most basic morphology: servos chained in series, each one placed on a joint of the robot, which I'll simply call **serial morphology**. It's the one used by most commercial robots and the simplest one mechanically: the legs just chain servos one after another, using the shaft of each servo as the axis of the joint. Let's take the best-known humanoid kits as an example. These are the legs of the Kondo KHR-3HV, Robonova, Bioloid and Robovie-X:

![Commercial humanoids](/assets/images/humanoid-legs-commercial.png)

The configuration of each one is:

- Kondo KHR-3HV: Y-R-P-P-P-R
- Robonova: R-P-P-P-R
- Bioloid: Y-R-P-P-P-R
- Robovie-X: R-P-P-P-R

One important detail: the Kondo and the Bioloid have the same servo configuration, but there is a difference. In the Bioloid, the pairs of servos of the ankle and the hip are placed so that their rotation axes cross, forming a spherical joint. In practice, this makes the Bioloid leg easier to control, while the Kondo leg has a much larger range of movement.

# The problem with the knees

The serial morphology has a problem, a very serious one for humanoid robots: the knees. Let's draw the leg of a Bioloid like this:

![Bioloid leg scheme](/assets/images/humanoid-legs-scheme.png){: .align-center width="300"}

The circles are the pitch servos and the lines are the rigid parts of the robot. This is how the segments of the leg change when the leg bends, something that happens all the time when the robot walks, or simply when it crouches:

![Bent leg scheme](/assets/images/humanoid-legs-scheme-bent.png){: .align-center width="200"}

Servos 1 and 3 turn the same angle, but to keep the posture, servo 2 has to turn twice that angle. This is a big bottleneck: every time the leg stretches or bends, the knee servo has to move twice as much as the other two. On top of that, the knee servo is usually the one carrying the most weight, since it's low and far from the torso.

To sum up: the serial morphology is the leg configuration used by 99% of commercial robots, and it overloads the knee servo. Other morphologies avoid this problem, with more or less mechanical ingenuity, like the parallel legs of [Minikame](/robots/minikame) and [Maus](/robots/maus), or the knees of [Predator](/robots/predator), driven by two servos in parallel.
