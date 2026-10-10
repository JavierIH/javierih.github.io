---
title: "Jev solving a micromouse maze"
date: 2026-10-10
comments: true
categories:
  - robots
---

[Jev](https://typesafe.ai/) is an AI model that doesn't write text: you give it some data and a few closed questions (yes/no, pick an option, a score), and it answers each one with a probability. I think that fits a robot really well: sensor readings in, a decision for the motors out. So I tried it with [Ratatron](/robots/ratatron/), my micromouse.

# The setup

Jev runs in the cloud, so the robot does the talking over Bluetooth: in every cell it stops, sends its readings and waits for an order (forward, left, right or back). A Python script on the PC asks Jev and sends the order back. Whatever Jev chooses, the robot does. The only exception: it won't drive into a wall it knows about. If Jev asks for that, it says so and asks again.

# Round 1: follow the right-hand wall

The simplest maze strategy there is, given to Jev in plain English:

```json
"move": {
  "type": "choice",
  "instructions": "Choose the robot's next move. The robot follows the right-hand rule: it keeps its right hand on the wall. Never move into a wall.",
  "criteria": {
    "forward": "Drive one cell straight ahead",
    "left": "Turn 90 degrees left in place, then drive one cell",
    "right": "Turn 90 degrees right in place, then drive one cell",
    "back": "Turn 180 degrees in place, then drive one cell"
  }
}
```

I tried two versions of the data. **A, the raw sensors**: the four IR readings in mm and the calibration needed to read them.

```json
{
  "context": "A micromouse robot is stopped at the centre of a cell of a maze and must choose its next move. Four IR sensors measure distances in mm: two pointing forward and one to each side; a reading below wall_if_ir_below_mm means a wall on that side.",
  "ir_mm": { "front_left": 87, "front_right": 102, "side_left": 91, "side_right": 226 },
  "calibration": {
    "wall_if_ir_below_mm": 140,
    "front_wall_at_cell_centre_mm": 94,
    "side_wall_at_cell_centre_mm": { "left": 89, "right": 76 }
  },
  "behind": "open: the cell it came from"
}
```

**B, the walls already read by the code**:

```json
{
  "context": "A micromouse robot is stopped at the centre of a cell of a maze and must choose its next move.",
  "moves": { "forward": "blocked by a wall", "left": "blocked by a wall", "right": "open" },
  "behind": "open: the cell it came from"
}
```

Both in the 16x16 maze of [OSHWDem 2026](/robots/ratatron/), the one where Ratatron got second, in a simulator that generates the IR readings from the walls. Left, raw sensors; right, walls. A red wall is one Jev wanted to drive into.

<video src="/assets/images/jev-sim-oshwdem2026.mp4" controls muted playsinline style="width: 100%; height: auto;" aria-label="Jev following the right-hand wall in a 16x16 maze, simulator: raw sensors versus walls"></video>

With the walls, it reaches the centre in 278 decisions without a single mistake. With the raw sensors, it never leaves the first 17 cells: 150 decisions and 114 attempts to drive into a wall. The funny part is that Jev does see the walls: asked in separate yes/no questions, it got all 450 right. But when it chooses the move, it doesn't use that, and mostly picks `right`, as if "right-hand rule" meant "turn right".

So the lesson is clear: Jev doesn't chain steps. The code has to do the reading.

# Round 2: explore like a micromouse

A wall follower is a three-line `if`, though. So I gave Jev the decision a real micromouse makes during the search: which way to explore to reach the centre.

It took me a few tries to find what to tell it:

- **The cells left to the centre for each move.** Jev did exactly what Ratatron's floodfill does, all 196 decisions. But that number *is* the floodfill, so picking the smallest one isn't much of a decision.
- **Whether each move gets closer to the centre in a straight line.** Jev cared about nothing else: in every maze I tried, it ended up going back and forth between the same two cells, forever, because one of them was "closer to the centre".
- **Only the walls and how many times each next cell has been visited.** This is the one that works:

```json
{
  "context": "A micromouse robot is exploring an unknown maze to reach its centre. It is stopped in a cell and must choose its next move. For each move you get what the robot knows: the walls it has seen and whether the next cell has been visited before.",
  "moves": {
    "forward": "open; the next cell has not been visited yet",
    "left": "blocked by a wall",
    "right": "open; the next cell has been visited once",
    "back": "open; the next cell has been visited 2 times"
  }
}
```

Jev: `forward`, with 0.98. No rule, nobody tells it to prefer new cells, but that's what it does: it explores like someone marking the walls with chalk, and it never gets stuck. Ratatron's own floodfill on the right:

<video src="/assets/images/jev-explore-oshwdem2026.mp4" controls muted playsinline style="width: 100%; height: auto;" aria-label="Jev exploring the OSHWDem 2026 maze next to Ratatron's floodfill, simulator"></video>

The floodfill reaches the centre in 196 decisions. Jev, with no idea where the centre is, takes its time, but it gets there: 378 decisions, 231 of the 256 cells, and not a single loop. It never chose a visited cell when a new one was available.

I also tried it in 8 other competition mazes. It reached the centre in 6 of them, taking 1.5 to 3.6 times as many decisions as the floodfill; in the other 2 it was still wandering through cells it had already seen after 500 decisions. The behaviour was the same in all of them: no loops, and always a new cell when there was one.

# On the real robot

Here Jev is driving Ratatron with the same visited-cells prompt from Round 2. It goes into dead ends, gets back out, and avoids the cells it has already been to. I'm going to need a bigger maze soon, this one has become a bit small:

<video src="/assets/images/ratatron-jev.mp4" autoplay loop muted playsinline style="width: 100%; height: auto;" aria-label="Ratatron driven by Jev in the 4x3 practice maze"></video>

# Conclusion

Jev can't drive Ratatron from raw sensors: it sees the walls, but it won't use them to decide. With the walls read by the code, it follows a rule as well as an `if`, and if you hand it the floodfill's distance, it becomes the floodfill. The interesting part came at the end: with only what the robot sees, and no rule at all, it found a sensible way to explore without being told one, and reached the centre in 7 of 9 mazes. Slower than Ratatron's own search, but with its own judgement. That's the job I'd give it in a robot: the code reads the world, Jev decides.
