╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 02               ║
║  FIRST LIGHT                       [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Light Module

---

## PARTS NEEDED

- [ ] Arduino Uno R3 (plugged into USB — power supply only, no code)
- [ ] Breadboard
- [ ] 1× Red LED (from Q01)
- [ ] 1× 220Ω resistor (Red-Red-Brown-Gold)
- [ ] 1× 1kΩ resistor (Brown-Black-Red-Gold)
- [ ] 1× 10kΩ resistor (Brown-Black-Orange-Gold)
- [ ] 2× Jumper wires (red and black)
- [ ] Pencil and this page — you will write down what you observe

---

## [LORE]

NEXUS has a Power Core, but its eye is just a dull red dot. The Engineer needs to calibrate the Light Module — adjusting exactly how much electricity flows to the eye so it glows at the right brightness. Too much current and the eye burns out. Too little and NEXUS can barely see. To get it right, the Engineer must learn one of the most powerful laws in all of electronics: Ohm's Law.

---

## [THE LAW]

**THE 2ND LAW: OHM'S LAW**

**V = I × R**

- **V** = Voltage (measured in Volts) — the electrical pressure pushing current through the circuit
- **I** = Current (measured in milliamps, mA) — how much electricity is actually flowing
- **R** = Resistance (measured in Ohms, Ω) — friction that slows the flow down

Think of electricity like water flowing through pipes. **Voltage** is the water pressure at the source — how hard the pump is pushing. **Current** is how much water is actually flowing through the pipe. **Resistance** is how narrow the pipe is — a narrow pipe (high resistance) slows the water down, a wide pipe (low resistance) lets it rush through.

Now here's the dangerous part: an LED is like a small, delicate nozzle. If you point a fire hose at it with no restriction, you'll blow it apart. The resistor is the narrow section of pipe you add to protect it. Without a resistor, too much current floods through the LED and burns it out in an instant.

**Ohm's Law proves it with math:**
- 5V source with a 220Ω resistor: I = 5 ÷ 220 = **about 23mA** (bright and safe)
- 5V source with a 1kΩ resistor: I = 5 ÷ 1000 = **about 5mA** (medium brightness)
- 5V source with a 10kΩ resistor: I = 5 ÷ 10000 = **about 0.5mA** (very dim)

You are about to SEE Ohm's Law with your own eyes.

---

## RESISTOR COLOR CODE CHEAT SHEET

Resistors use colored bands to tell you their value. Read the bands left to right. The gold band is always on the RIGHT — that's the tolerance band (ignore it for now).

```
  COLOR CODE TABLE

  Black  = 0       Green  = 5
  Brown  = 1       Blue   = 6
  Red    = 2       Violet = 7
  Orange = 3       Gray   = 8
  Yellow = 4       White  = 9

  HOW TO READ A 4-BAND RESISTOR:
  Band 1 = first digit
  Band 2 = second digit
  Band 3 = number of zeros to add
  Band 4 = tolerance (gold = ±5%, ignore for now)
```

**Your three resistors:**

```
  220Ω:   Red  - Red  - Brown - Gold
          (2)    (2)    (1 zero) = 220

  1kΩ:    Brown - Black - Red - Gold
          (1)     (0)    (2 zeros) = 1,000

  10kΩ:   Brown - Black - Orange - Gold
          (1)     (0)    (3 zeros) = 10,000
```

---

## [BLUEPRINT]

**Circuit Diagram (same as Q01, but you will swap the resistor):**

```
  [Arduino]
      |
     5V
      |
      +────────────────────────────+
      |                            |
      |                        (long leg +)
      |                          [LED]
      |                        (short leg -)
      |                            |
      |                      [RESISTOR] <-- swap this part
      |                            |
     GND ──────────────────────────+
      |
  [Arduino]
```

**Observation Table — fill this in as you go:**

```
  +──────────────────┬─────────────────────────────────+
  │ Resistor Used    │ LED Brightness (circle one)     │
  ├──────────────────┼─────────────────────────────────┤
  │ 220Ω             │ DIM    /   MEDIUM   /   BRIGHT  │
  ├──────────────────┼─────────────────────────────────┤
  │ 1kΩ              │ DIM    /   MEDIUM   /   BRIGHT  │
  ├──────────────────┼─────────────────────────────────┤
  │ 10kΩ             │ DIM    /   MEDIUM   /   BRIGHT  │
  +──────────────────+─────────────────────────────────+
```

---

**BREADBOARD WIRING**

This is the same wiring as Q01. The only thing that changes between each experiment is which resistor you plug in.

```
  Arduino 5V  --> RED rail (+)
  Arduino GND --> BLUE rail (-)

  LED long leg  (+) --> Row 10, hole A
  LED short leg (-) --> Row 11, hole A

  Resistor leg 1 --> Row 11, hole C   (same row as LED short leg)
  Resistor leg 2 --> Row 13, hole C

  Wire: Row 13, hole E --> BLUE rail (-)
  Wire: RED rail (+)   --> Row 10, hole E
```

When you swap resistors: pull the old resistor out of holes C11 and C13, then push the new resistor into the same holes.

---

## [BUILD MISSION]

**Round 1: 220Ω Resistor**

1. Build the Q01 circuit (or leave it wired from Q01).
2. Make sure the 220Ω resistor (Red-Red-Brown-Gold) is in the circuit.
3. Plug the Arduino into USB.
4. Look at the LED brightness.
5. Circle "BRIGHT" in the table above for 220Ω.
6. Unplug the Arduino from USB.

**Round 2: 1kΩ Resistor**

7. Pull the 220Ω resistor out of the breadboard.
8. Find the 1kΩ resistor (Brown-Black-Red-Gold).
9. Push the 1kΩ resistor into the same holes where the 220Ω was.
10. Plug the Arduino into USB.
11. Look at the LED. Is it brighter or dimmer than before?
12. Circle your answer in the table above for 1kΩ.
13. Unplug the Arduino from USB.

**Round 3: 10kΩ Resistor**

14. Pull the 1kΩ resistor out of the breadboard.
15. Find the 10kΩ resistor (Brown-Black-Orange-Gold).
16. Push the 10kΩ resistor into the same holes.
17. Plug the Arduino into USB.
18. Look at the LED closely — you may need to dim the room lights to see it.
19. Circle your answer in the table above for 10kΩ.
20. Unplug the Arduino from USB.

**If your circuit doesn't work:**

- If the LED doesn't light at all with 220Ω, check that it is not in backwards (long leg must face 5V).
- If the LED looks the same brightness with all three resistors, check that you are actually swapping the resistor — make sure the old one is fully out before inserting the new one.
- At 10kΩ the LED is extremely dim. Turn off the room lights and look closely — it should be a faint glow.
- Check color bands carefully — Orange and Red look similar under some lighting. Orange has a slightly warm reddish tone but is more clearly orange.

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Light Module

NEXUS's eye is now calibrated. The Engineer has proven with their own hands that more resistance means less current and less brightness — exactly what Ohm's Law predicts. This law governs every circuit ever built.

**Next Quest:** Q03 — The Blink

**Side Quest Unlocked:** SQ01 — RGB Rainbow *(Wire a three-color RGB LED and mix colors using Ohm's Law)*
