╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 05               ║
║  PUSH THE BUTTON                   [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Input Terminal

---

## PARTS NEEDED

- [ ] Arduino Uno R3 (plugged into USB — power supply only, no code)
- [ ] Breadboard
- [ ] 1× Push button (tactile switch, 4 legs)
- [ ] 1× Active buzzer (the one with a sticker or marking on top showing + and -)
- [ ] Jumper wires (red and black)

---

## [LORE]

NEXUS has eyes, a Power Core, and a Switch Panel — but it cannot make a sound. A silent robot can't warn the Engineer of danger, can't celebrate a victory, can't signal that a mission is complete. The Engineer must install the Input Terminal: a system that reads a button press and triggers NEXUS's first sound. This is the moment NEXUS stops being a glowing prop and starts being something that actually RESPONDS.

---

## [THE LAW]

**THE 5TH LAW: INPUTS AND OUTPUTS**

Every circuit has two kinds of components: **INPUTS** and **OUTPUTS**.

- An **INPUT** is something that controls or sends information into the circuit. It does not make things happen by itself — it decides WHEN things happen.
- An **OUTPUT** is something that does something — it lights up, makes sound, moves, heats up, or sends a signal.

Think of a doorbell. The **button** on the wall is the INPUT. It does not make any sound on its own. It is just a switch you press. The **chime** inside the house is the OUTPUT. It makes the sound, but it has no idea whether you pressed anything — it just responds to the electricity that the button let through.

The button does not know about the chime. The chime does not know about the button. Electricity is the messenger that connects them. When you press the button (INPUT), the circuit closes, electricity flows to the chime (OUTPUT), and it buzzes.

In this quest, your **INPUT** is the push button. Your **OUTPUT** is the active buzzer. You press the button, the buzzer sounds. You release the button, silence returns.

---

## ACTIVE BUZZER vs. PASSIVE BUZZER

Your kit has TWO types of buzzers. They look almost identical from the outside. It is very important to use the RIGHT one for this quest.

```
  ACTIVE BUZZER                    PASSIVE BUZZER
  ─────────────────────────────    ─────────────────────────────
  Has an internal oscillator       No internal oscillator
  (a tiny circuit inside that      (just a vibrating disk —
  generates the buzzing sound)     needs an oscillating signal)

  Just needs POWER to buzz         Needs a pulsing ON/OFF signal
                                   from the Arduino brain

  Works WITHOUT any code           Will NOT buzz without code

  USUALLY has a sticker            Usually has no sticker and
  or "+" marking on top            you can see the disk inside
                                   through a small hole

  USE THIS ONE FOR QUEST 5!        Save this for Act 2 (with code)
```

**How to tell them apart:** The active buzzer usually has a smooth top with a sticker covering the hole, and the + and - legs are often labeled. If you are unsure, try connecting each one briefly — the active buzzer will make a continuous tone with just power, the passive buzzer will make no sound or just a single click.

```
  ACTIVE BUZZER (side view):

         + (longer leg or labeled leg) → connects toward 5V
        ┌─────┐
        │  +  │  <-- label or sticker on top
        └──┬──┘
           │
         - (shorter leg or negative leg) → connects toward GND
```

---

## [BLUEPRINT]

**Circuit Diagram:**

```
  [Arduino]
      |
     5V
      |
      +──────────────────────────────────+
      |                                  |
      |                            [PUSH BUTTON]
      |                            (press to close)
      |                                  |
      |                         [ACTIVE BUZZER (+)]
      |                          (positive/longer leg)
      |                         [ACTIVE BUZZER (-)]
      |                          (negative/shorter leg)
      |                                  |
     GND ───────────────────────────────+
      |
  [Arduino]

  No resistor needed — the active buzzer has internal resistance built in.

  When button is OPEN:   5V ---X--- Buzzer (silence)
  When button is CLOSED: 5V ----> Buzzer ----> GND (BUZZ!)
```

---

**BREADBOARD WIRING**

```
  Arduino 5V  --> RED rail (+)
  Arduino GND --> BLUE rail (-)

  Push button: straddle the center gap of the breadboard
    Left legs  in rows 5 and 7, columns D and E
    Right legs in rows 5 and 7, columns F and G

  Wire: RED rail (+) --> Row 5, hole A    (left side of button, toward 5V)

  Active Buzzer (+) long/positive leg --> Row 10, hole C
  Active Buzzer (-) short/negative leg --> Row 11, hole C

  Wire: Row 7, hole A --> Row 10, hole A  (right side of button to buzzer +)

  Wire: Row 11, hole E --> BLUE rail (-)  (buzzer - to GND)
```

**Order of electricity travel:**

```
  5V rail → Button left side → [press!] → Button right side
         → Buzzer (+) → Buzzer (-) → GND rail
```

---

## [BUILD MISSION]

1. Start with a clear breadboard.
2. Connect a red jumper wire from the Arduino **5V pin** to the **red (+) rail** of the breadboard.
3. Connect a black jumper wire from the Arduino **GND pin** to the **blue (-) rail** of the breadboard.
4. Find the push button and place it so it straddles the center gap of the breadboard. Press it in firmly until all 4 legs are seated.
5. Connect a jumper wire from the **red (+) rail** to the **same row as one of the left legs** of the button.
6. Find the active buzzer. Look for the + marking or the longer leg — this is the positive side.
7. Place the active buzzer's **+ (positive) leg** into a row a few rows below the button.
8. Place the active buzzer's **- (negative) leg** into the very next row below.
9. Connect a jumper wire from the **right side of the button** to the **same row as the buzzer's + leg**.
10. Connect a jumper wire from the **buzzer's - leg row** to the **blue (-) GND rail**.
11. Plug the USB cable into the Arduino Uno.
12. Plug the other end into a USB port or USB charger.
13. Do NOT press the button yet. There should be silence.
14. Press and hold the push button.
15. The buzzer should make a continuous tone.
16. Release the button.
17. The buzzer should stop.
18. Press and release several times. Listen to the buzzer respond to your input.

**If your circuit doesn't work:**

- If the buzzer makes noise ALL the time (even without pressing), check that the wire from 5V is going to the BUTTON first — it should not connect directly to the buzzer.
- If pressing the button produces no sound, check that the buzzer is oriented correctly: the + leg should be on the 5V side (coming from the button), the - leg toward GND.
- Make sure you are using the ACTIVE buzzer, not the passive one. The passive buzzer will not make a continuous tone with just DC power.
- Check that the button is straddling the center gap — if both sides are on the same half of the breadboard, the button cannot bridge the gap when pressed.
- Check all wire and component legs are fully inserted into the breadboard.

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Input Terminal

NEXUS can hear you now — or at least, NEXUS responds to your touch. The Engineer has installed the first true input/output system: a button (input) that triggers a buzzer (output). This is the foundation of every interactive device ever made. Every time you press a key on a keyboard, tap a touchscreen, or trigger a sensor — an input is sending a signal to an output.

**Next Quest:** Q06 — Sound Off
