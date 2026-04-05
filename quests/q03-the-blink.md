╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 03               ║
║  THE BLINK                         [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Switch Panel

---

## PARTS NEEDED

- [ ] Arduino Uno R3 (plugged into USB — power supply only, no code)
- [ ] Breadboard
- [ ] 1× Red LED
- [ ] 1× 220Ω resistor (Red-Red-Brown-Gold)
- [ ] 1× Push button (tactile switch, 4 legs)
- [ ] Jumper wires (red and black)

---

## [LORE]

NEXUS has a Power Core and a calibrated Light Module — but its eye stays on all the time. A real robot needs to blink, to signal, to communicate with flashes. The Engineer must install a Switch Panel so NEXUS can send on/off signals with the press of a button. This is how robots begin to respond to the world around them.

---

## [THE LAW]

**THE 3RD LAW: OPEN AND CLOSED CIRCUITS**

A switch **opens** or **closes** a circuit. When the circuit is **closed**, electricity flows and things happen. When the circuit is **open**, the loop is broken and everything stops.

Think of a drawbridge over a river. When the drawbridge is **down** (closed), traffic can cross from one side to the other — the road is complete. When the drawbridge is **up** (open), there is a gap in the road and nothing can cross. Cars pile up on both sides going nowhere.

A push button is a tiny drawbridge built into your circuit. When you press it, the bridge comes down and electricity flows. When you release it, the bridge goes back up and electricity stops. It is that simple — and that powerful.

This is called a **momentary switch** — it only stays closed while you are pressing it. The switches on video game controllers, keyboards, and TV remotes are all the same idea.

---

## HOW A PUSH BUTTON WORKS

The push button in your kit has **4 legs**. This confuses a lot of engineers the first time they see it. Here is the secret:

```
  PUSH BUTTON (top view):

       LEG A ──┐     ┌── LEG B
               │     │
               └──[BRIDGE]──┘   <-- this bridge closes when pressed
               │     │
       LEG C ──┘     └── LEG D

  INTERNAL CONNECTIONS:
  Leg A and Leg C are ALWAYS connected to each other (same side).
  Leg B and Leg D are ALWAYS connected to each other (same side).

  When you PRESS the button:
  The bridge connects the LEFT side (A/C) to the RIGHT side (B/D).
  Current can now flow from one side to the other.

  When you RELEASE the button:
  The bridge lifts. The left side and right side are disconnected.
  Current stops.
```

**Placing the button on the breadboard:**

The button must STRADDLE the center gap of the breadboard. The two legs on the left go into the left half. The two legs on the right go into the right half. This is the only way the button works correctly.

```
  BREADBOARD CENTER GAP:

  [A B C D E]  ← left half
              (GAP)
  [F G H I J] ← right half

  Button placement:
  LEFT legs  → columns D and E (or C and D)
  RIGHT legs → columns F and G (or G and H)
  The button body sits over the gap.
```

---

## [BLUEPRINT]

**Circuit Diagram:**

The button is wired **in series** with the LED. In series means they are on the SAME single path — electricity must pass through the button AND the LED AND the resistor to complete the loop.

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
      |                            (long leg +)
      |                              [LED]
      |                            (short leg -)
      |                                  |
      |                           [220Ω RESISTOR]
      |                                  |
     GND ───────────────────────────────+
      |
  [Arduino]

  When button is OPEN:  5V ---X--- LED (nothing flows)
  When button is CLOSED: 5V ----> LED ----> GND (LED glows!)
```

---

**BREADBOARD WIRING**

```
  Arduino 5V  --> RED rail (+)
  Arduino GND --> BLUE rail (-)

  Push button: straddle the center gap of the breadboard
    Left legs  in rows 5 and 7, columns D and E
    Right legs in rows 5 and 7, columns F and G

  Wire: RED rail (+) --> Row 5, hole A    (connects to left side of button)

  LED long leg  (+) --> Row 10, hole A
  LED short leg (-) --> Row 11, hole A

  Wire: Row 7, hole A --> Row 10, hole C  (right side of button to LED +)

  Resistor leg 1 --> Row 11, hole C
  Resistor leg 2 --> Row 13, hole C

  Wire: Row 13, hole E --> BLUE rail (-)
```

*(Your exact row numbers may vary — what matters is the ORDER: 5V → button → LED long leg → LED short leg → resistor → GND)*

---

## [BUILD MISSION]

1. Start with a clear breadboard. Remove any wires from Q01 or Q02.
2. Find the push button. Look at it from the top — the two pairs of legs form a small rectangle.
3. Place the push button so it **straddles the center gap** of the breadboard. The legs should snap in with a slight click.
4. Place the LED long leg (+) into a row a few rows BELOW the button on the breadboard.
5. Place the LED short leg (-) into the very next row down.
6. Place one leg of the 220Ω resistor in the same row as the LED's short leg.
7. Place the other leg of the 220Ω resistor two rows below that.
8. Use a jumper wire to connect the **5V red rail** to the **left side of the push button** (same row as one of the left legs).
9. Use a jumper wire to connect the **right side of the push button** to the **same row as the LED's long leg (+)**.
10. Use a jumper wire to connect the **bottom leg of the resistor** to the **GND blue rail**.
11. Use a red jumper wire to connect the Arduino **5V pin** to the **red rail** on the breadboard.
12. Use a black jumper wire to connect the Arduino **GND pin** to the **blue rail** on the breadboard.
13. Plug the USB cable into the Arduino and then into USB power.
14. Look at the LED. It should be **off**.
15. Press and hold the push button.
16. The LED should **light up** while you hold the button.
17. Release the button.
18. The LED should **turn off**.

**If your circuit doesn't work:**

- If the LED stays on all the time (never turns off), the button is not in the circuit path — check that your wire from 5V goes through the button before reaching the LED.
- If the LED never turns on when you press the button, check that the button is straddling the center gap of the breadboard — if both leg pairs are on the same side, the button cannot work.
- Check that the LED is not in backwards (long leg must face the button side, which is toward 5V).
- Try pressing the button on all four corners — the button sometimes needs to be pressed firmly in the center.
- Check that all wires are fully inserted into the breadboard holes.

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Switch Panel

NEXUS can now blink on command. The Engineer controls when electricity flows — and when it stops. This is the fundamental idea behind every button, keyboard key, touchscreen tap, and sensor in the world: something opens or closes a circuit, and that change is information.

**Next Quest:** Q04 — Many Lights
