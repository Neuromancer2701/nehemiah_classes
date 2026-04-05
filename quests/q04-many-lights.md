╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 04               ║
║  MANY LIGHTS                       [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Multi-Eye Array

---

## PARTS NEEDED

- [ ] Arduino Uno R3 (plugged into USB — power supply only, no code)
- [ ] Breadboard
- [ ] 2× LEDs (any color — using 2 of the same color makes the brightness comparison easiest)
- [ ] 2× 220Ω resistors (Red-Red-Brown-Gold) — needed for parallel circuit
- [ ] 1× 100Ω resistor (Brown-Black-Brown-Gold) — needed for series circuit
- [ ] Jumper wires (red and black)
- [ ] Pencil — you will fill in the observation table

---

## [LORE]

NEXUS has one eye — but robots are supposed to have two. The Engineer must install the Multi-Eye Array: a pair of glowing sensors that let NEXUS see in stereo. But wiring two LEDs is not as simple as adding a second one to the same wire. The Engineer is about to discover that HOW you connect components changes everything about how they behave. Two completely different circuits. Two completely different results.

---

## [THE LAW]

**THE 4TH LAW: SERIES AND PARALLEL**

There are two ways to connect components in a circuit:

**SERIES** — one single path. Every component is on the same road, one after another. Current has no choice — it must pass through every single component in order.

**PARALLEL** — multiple paths branching off from the same source. Each component gets its own road. Current splits up and each branch gets some.

Think of a hallway in a school. If there is only ONE narrow hallway and every student must walk through it single-file, everyone slows each other down. That is **series** — one path shared by everyone.

Now imagine three hallways side by side. Each student picks their own hallway and walks at full speed with no crowding. That is **parallel** — each branch gets full access.

In series, the voltage gets split between the LEDs, so each one gets less. In parallel, each LED gets the full 5V on its own branch — so they glow brighter and independently.

**The key difference you will see:**

- **Series:** both LEDs share the voltage — they may be dimmer, and if one is removed the other goes out too.
- **Parallel:** each LED gets full voltage — they glow bright, and each one is independent.

---

## [BLUEPRINT]

**CIRCUIT A — SERIES (one path):**

Both LEDs are on the same single wire path. The current must travel through LED1, then LED2, then the resistor.

```
  [Arduino]
      |
     5V
      |
      +─────────────────────────────────+
      |                                 |
      |                           (long leg +)
      |                             [LED 1]
      |                           (short leg -)
      |                                 |
      |                           (long leg +)
      |                             [LED 2]
      |                           (short leg -)
      |                                 |
      |                          [100Ω RESISTOR]
      |                                 |
     GND ────────────────────────────── +
      |
  [Arduino]

  One path: 5V → LED1 → LED2 → Resistor → GND
```

Why 100Ω instead of 220Ω for series? Each LED uses up some voltage (about 2V each). With 2 LEDs sharing 5V, there's only about 1V left for the resistor to work with. A smaller resistor lets enough current through so both LEDs actually glow. At 220Ω with 2 LEDs in series, the LEDs would be too dim or not light at all.

**CIRCUIT B — PARALLEL (two paths):**

Each LED has its OWN path from 5V to GND. Each gets a separate resistor.

```
  [Arduino]
      |
     5V
      |
      +─────────────┬──────────────────+
      |             |                  |
      |       (long leg +)       (long leg +)
      |          [LED 1]            [LED 2]
      |       (short leg -)      (short leg -)
      |             |                  |
      |       [220Ω RES.]        [220Ω RES.]
      |             |                  |
     GND ──────────┴──────────────────+
      |
  [Arduino]

  Path 1: 5V → LED1 → 220Ω → GND
  Path 2: 5V → LED2 → 220Ω → GND
```

---

**BREADBOARD WIRING — SERIES**

```
  Arduino 5V  --> RED rail (+)
  Arduino GND --> BLUE rail (-)

  Wire: RED rail (+) --> Row 5, hole A

  LED1 long leg  (+) --> Row 5, hole C
  LED1 short leg (-) --> Row 6, hole C

  Wire: Row 6, hole E --> Row 8, hole A   (bridge between LED1 and LED2)

  LED2 long leg  (+) --> Row 8, hole C
  LED2 short leg (-) --> Row 9, hole C

  100Ω Resistor leg 1 --> Row 9, hole E
  100Ω Resistor leg 2 --> Row 11, hole E

  Wire: Row 11, hole A --> BLUE rail (-)
```

**BREADBOARD WIRING — PARALLEL**

```
  Arduino 5V  --> RED rail (+)
  Arduino GND --> BLUE rail (-)

  -- Branch 1 (left side of board) --
  Wire: RED rail (+) --> Row 5, hole A
  LED1 long leg  (+) --> Row 5, hole C
  LED1 short leg (-) --> Row 6, hole C
  220Ω Resistor #1 leg 1 --> Row 6, hole E
  220Ω Resistor #1 leg 2 --> Row 8, hole E
  Wire: Row 8, hole A --> BLUE rail (-)

  -- Branch 2 (right side of board) --
  Wire: RED rail (+) --> Row 12, hole A
  LED2 long leg  (+) --> Row 12, hole C
  LED2 short leg (-) --> Row 13, hole C
  220Ω Resistor #2 leg 1 --> Row 13, hole E
  220Ω Resistor #2 leg 2 --> Row 15, hole E
  Wire: Row 15, hole A --> BLUE rail (-)
```

*(Both branches connect to the same red and blue rails, which is how they share the same 5V and GND source.)*

---

## [BUILD MISSION]

**Part 1: Build the Series Circuit**

1. Start with a clear breadboard.
2. Connect Arduino 5V to the red rail and GND to the blue rail.
3. Place LED1 on the breadboard. Long leg (+) faces toward the red rail.
4. Place LED2 directly below LED1. Long leg (+) faces the same direction as LED1.
5. Connect a wire from the short leg (-) of LED1 to the long leg (+) row of LED2.
6. Place the 100Ω resistor below LED2, connecting to LED2's short leg (-).
7. Connect the bottom of the resistor to the blue GND rail.
8. Connect the 5V red rail to the long leg (+) row of LED1.
9. Plug the Arduino into USB.
10. Look at both LEDs. Note the brightness.
11. Fill in "Series" row in the table below.
12. Unplug the Arduino from USB.

**Part 2: Build the Parallel Circuit**

13. Remove all wires and components from the breadboard.
14. Place LED1 on the left side of the board. Long leg faces the red rail.
15. Place a 220Ω resistor below LED1.
16. Connect a wire from the bottom of resistor #1 to the blue GND rail.
17. Connect a wire from the red rail to the long leg (+) row of LED1.
18. Place LED2 on a different section of the board (away from LED1), long leg facing the red rail.
19. Place a second 220Ω resistor below LED2.
20. Connect the bottom of resistor #2 to the blue GND rail.
21. Connect a wire from the red rail to the long leg (+) row of LED2.
22. Plug the Arduino into USB.
23. Look at both LEDs. Compare brightness to what you saw in the series circuit.
24. Fill in "Parallel" row in the table below.
25. Unplug the Arduino from USB.

**Observation Table — fill this in:**

```
  +───────────────┬──────────────────────────────────────────+
  │ Circuit Type  │ LED Brightness (circle one)              │
  ├───────────────┼──────────────────────────────────────────┤
  │ SERIES        │ DIM      /     MEDIUM     /     BRIGHT   │
  ├───────────────┼──────────────────────────────────────────┤
  │ PARALLEL      │ DIM      /     MEDIUM     /     BRIGHT   │
  +───────────────+──────────────────────────────────────────+

  In SERIES, if I unplug one LED, the other LED: STAYS ON  /  GOES OUT

  In PARALLEL, if I unplug one LED, the other LED: STAYS ON  /  GOES OUT
```

*(Try the unplug test! Carefully pull one LED out of the breadboard while powered and see what happens.)*

**If your circuit doesn't work:**

- **Series:** If both LEDs are off, check that the wire between LED1's short leg and LED2's long leg is in the correct rows. The short leg of one must connect to the long leg of the next.
- **Series:** If only one LED glows, one LED may be in backwards — check both long legs point toward 5V.
- **Parallel:** If one branch works but the other doesn't, check the non-working LED is not in backwards, and check its resistor is connected from its short leg to GND.
- **Parallel:** Make sure each branch has its own 220Ω resistor — do not share one resistor between both LEDs in parallel.

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Multi-Eye Array

NEXUS now has two eyes, wired in parallel — each one bright, each one independent. The Engineer has learned one of the most important lessons in electronics: it is not just WHAT you connect, but HOW you connect it that determines what happens. Every circuit in existence uses combinations of series and parallel connections.

**Next Quest:** Q05 — Push the Button
