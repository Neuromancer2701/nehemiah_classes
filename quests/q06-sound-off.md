╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 06               ║
║  SOUND OFF                         [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Basic Voice Module

---

## PARTS NEEDED

- [ ] Arduino Uno R3 (plugged into USB — power supply only, no code)
- [ ] Breadboard
- [ ] 1× Potentiometer (10kΩ, the dial component with 3 legs)
- [ ] 1× Red LED
- [ ] 1× 220Ω resistor (Red-Red-Brown-Gold)
- [ ] 1× Active buzzer (from Quest 05)
- [ ] Jumper wires (red and black)
- [ ] Pencil — you will record observations

---

## [LORE]

NEXUS has a voice — but it only knows one volume: LOUD. A good robot companion needs to whisper when the Engineer is hiding and shout when danger is near. The Engineer must install the Basic Voice Module: a component that gives NEXUS a dial, a knob, a faucet for electricity. This is NEXUS's first taste of something beyond simple on and off. This is ANALOG control — and it changes everything.

---

## [THE LAW]

**THE 6TH LAW: VARIABLE RESISTANCE AND ANALOG CONTROL**

So far every circuit in these quests has been **digital** — either ON or OFF. Full power or no power. The light is either glowing or dark. The buzzer is either buzzing or silent.

But the real world is not digital. The real world has shades, levels, volumes, brightnesses, speeds — infinite points between zero and maximum. That kind of control is called **analog**.

A **potentiometer** (say it: po-TEN-shee-AH-meh-ter) is a variable resistor. It is a resistor whose resistance you can change by turning a knob. On the inside, it is a long strip of resistive material with a sliding contact (called the **wiper**) that moves along the strip as you turn the dial.

Think of a faucet in a sink. A light switch is digital — it is only ever fully on or fully off. But a faucet is analog — you can have it fully off, a tiny trickle, half on, almost full, or completely open. Every position gives a different flow. A potentiometer is the electronics faucet. Turn it one way and resistance goes UP (less current, dimmer light, quieter buzz). Turn it the other way and resistance goes DOWN (more current, brighter light, louder buzz).

```
  DIGITAL:   OFF ──────────────────── ON
             (only two choices)

  ANALOG:    OFF ───────────────────── ON
              0%  25%  50%  75%  100%
             (infinite choices in between)
```

The potentiometer gives the Engineer smooth, continuous control over electricity — not just a switch, but a dial.

---

## HOW A POTENTIOMETER WORKS

A potentiometer has **3 pins (legs)**:

```
  POTENTIOMETER (top view, knob facing up):

        ┌─────────────────────────┐
        │                         │
      PIN 1               PIN 3  │
  (one end of strip)  (other end of strip)
        │                         │
        └──────────┬──────────────┘
                   │
                 PIN 2
               (WIPER — the middle pin,
                moves as you turn the knob)

  Internal structure:

  PIN 1 ──[━━━━━━━━━━━━━━━━━━━━━]── PIN 3
                 resistive strip
                       ↑
                    [WIPER]
                (PIN 2 — slides along
                 the strip as you turn)
```

**How to use it as a variable resistor in this quest:**

- Connect **PIN 1** to **5V**
- Connect **PIN 2** (wiper/middle) to your circuit
- Connect **PIN 3** to **GND**

As you turn the knob:
- Knob all the way one direction: WIPER is near PIN 1 (5V side) → very low resistance between wiper and PIN 1 → maximum current → brightest/loudest
- Knob all the way other direction: WIPER is near PIN 3 (GND side) → maximum resistance between wiper and PIN 1 → minimum current → dimmest/quietest
- Knob in the middle: medium resistance → medium brightness/volume

---

## [BLUEPRINT]

**EXPERIMENT A — Potentiometer controlling LED brightness:**

```
  [Arduino]
      |
     5V
      |
      +──────────────────────────────────────+
      |                                      |
      |                               [POT PIN 1]
      |                                      |
      |                           ┌─[resistive strip]─┐
      |                           │                   │
      |                         PIN 1               PIN 3 ── GND
      |                           │        
      |                        [WIPER / PIN 2]
      |                               |
      |                          (long leg +)
      |                            [LED]
      |                          (short leg -)
      |                               |
      |                       [220Ω RESISTOR]
      |                               |
     GND ───────────────────────────+
      |
  [Arduino]

  Simplified view:
  5V → POT (variable resistance) → LED (+) → LED (-) → 220Ω → GND
                                 ↑
                       turning the knob changes
                       resistance from 0Ω to 10kΩ
```

**EXPERIMENT B — Potentiometer controlling buzzer volume:**

```
  Replace the LED + 220Ω resistor with the Active Buzzer:

  5V → POT PIN 1
  POT PIN 2 (wiper) → Active Buzzer (+)
  Active Buzzer (-) → GND
  POT PIN 3 → GND
```

---

**BREADBOARD WIRING — Experiment A (LED)**

```
  Arduino 5V  --> RED rail (+)
  Arduino GND --> BLUE rail (-)

  Potentiometer: place it across 3 rows, straddling the center gap is NOT needed
    PIN 1 (left leg)   --> Row 5, hole A
    PIN 2 (middle leg) --> Row 5, hole B  (or it may go into Row 5, hole C
                           depending on your pot's leg spacing — check yours)
    PIN 3 (right leg)  --> Row 5, hole C  (or D — legs 1 apart from pin 2)

  Note: The 3 legs of a potentiometer are usually in a straight line.
  Place them in 3 consecutive holes in the SAME column section.
  Example: holes A5, A6, A7 if the legs are spaced one row apart.

  Wire: RED rail (+)  --> Row of PIN 1
  Wire: BLUE rail (-) --> Row of PIN 3

  Wire: Row of PIN 2 (wiper) --> Row 10, hole C  (going to LED)

  LED long leg  (+) --> Row 10, hole A
  LED short leg (-) --> Row 11, hole A

  220Ω Resistor leg 1 --> Row 11, hole C
  220Ω Resistor leg 2 --> Row 13, hole C

  Wire: Row 13, hole E --> BLUE rail (-)
```

**Key wiring rule:** The path goes: 5V → PIN 1 → [strip] → WIPER (PIN 2) → LED → Resistor → GND. PIN 3 also connects to GND to complete the resistive strip inside the pot.

---

## [BUILD MISSION]

**Part 1: Control LED Brightness with the Potentiometer**

1. Start with a clear breadboard.
2. Connect Arduino 5V to the red rail and GND to the blue rail.
3. Find the potentiometer. Look at the 3 legs on the bottom. The middle leg is the wiper (PIN 2).
4. Place the potentiometer on the breadboard so each leg is in its own row.
5. Connect a red jumper wire from the red (+) rail to the row of **PIN 1** (one outer leg).
6. Connect a black jumper wire from the blue (-) rail to the row of **PIN 3** (the other outer leg).
7. Connect a jumper wire from the row of **PIN 2** (middle/wiper) to a new empty row further down the board.
8. Place the LED's long (+) leg in that same new row (same row the PIN 2 wire goes to).
9. Place the LED's short (-) leg in the next row down.
10. Place the 220Ω resistor: one leg in the LED's short (-) leg row, other leg 2 rows further down.
11. Connect a wire from the bottom leg of the resistor to the blue (-) GND rail.
12. Plug the Arduino into USB power.
13. Look at the LED — it should be glowing.
14. Slowly turn the potentiometer knob in one direction.
15. Watch the LED get brighter or dimmer.
16. Turn it the other direction.
17. Turn all the way — observe maximum brightness.
18. Turn all the way back — observe minimum brightness (may go nearly off).
19. Find the middle — medium brightness.
20. Unplug the Arduino from USB.

**Part 2: Control Buzzer Volume with the Potentiometer**

21. Remove the LED and the 220Ω resistor from the board. Leave the potentiometer and its wires in place.
22. Find the active buzzer. Identify the + and - legs.
23. Place the active buzzer's + leg in the same row that was connected to the wiper (PIN 2) wire.
24. Place the active buzzer's - leg in the next row down.
25. Connect a wire from the buzzer's - leg row to the blue GND rail.
26. Plug the Arduino into USB power.
27. The buzzer should be making a sound.
28. Slowly turn the potentiometer knob.
29. Listen carefully — the volume should change as you turn the knob.
30. Note: the volume change may be subtle. At high resistance, the buzzer may stop entirely.
31. Unplug the Arduino from USB.

**Observation Notes — fill these in:**

```
  POT turned all the way LEFT:

    LED brightness: _________________________________

    Buzzer volume:  _________________________________

  POT turned to the MIDDLE:

    LED brightness: _________________________________

    Buzzer volume:  _________________________________

  POT turned all the way RIGHT:

    LED brightness: _________________________________

    Buzzer volume:  _________________________________
```

**If your circuit doesn't work:**

- If the LED doesn't change brightness when you turn the knob, check that the wiper (middle pin, PIN 2) is what connects to the LED — not PIN 1 or PIN 3.
- If PIN 3 is not connected to GND, turning the knob may have no effect — the voltage divider needs both outer pins connected.
- If the LED is always off, check the LED is not backwards (long leg must face the wiper wire side).
- If the buzzer produces no sound at any knob position, make sure it is the active buzzer and confirm + leg is on the wiper side.
- If you cannot tell which leg is the wiper, the middle leg of the 3-leg row is always the wiper on standard potentiometers.

---

## ACT 2 PREVIEW

Right now, the potentiometer changes brightness and volume by directly changing how much current flows. That is purely physical — no thinking involved.

In **Act 2**, the Arduino brain wakes up. When the Arduino runs code, it can **READ** the wiper position as a number from **0 to 1023**. Zero means the knob is all the way in one direction. 1023 means all the way in the other. 512 is exactly in the middle.

With that number, the Engineer can program NEXUS to:
- Change LED color based on knob position
- Control motor speed
- Set volume levels precisely
- Build a fully programmable control panel

The knob you just wired will become NEXUS's first programmable input. That is when things get really powerful.

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Basic Voice Module

NEXUS now has a voice with VOLUME CONTROL. The Engineer has crossed a major threshold — from digital (on/off) thinking to analog (smooth, continuous) thinking. This is how real-world control systems work: thermostats, volume knobs, speed controllers, joysticks. All of them use variable resistance and analog signals. The Engineer now speaks both languages.

**Next Quest:** Q07 — The Brain Awakens *(Act 2 begins — the Arduino starts running code)*
