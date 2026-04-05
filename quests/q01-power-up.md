╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 01               ║
║  POWER UP                          [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Power Core

---

## PARTS NEEDED

- [ ] Arduino Uno R3
- [ ] USB cable (connects Arduino to computer or USB charger)
- [ ] Breadboard
- [ ] 1× Red LED
- [ ] 1× 220Ω resistor (Red-Red-Brown-Gold bands)
- [ ] 2× Jumper wires (one red, one black)

---

## [LORE]

Deep in the workshop, the Robot Engineer stares at a pile of parts. Somewhere in that pile is NEXUS — but NEXUS has no power. No heartbeat. No light. Before any robot can think, move, or speak, it needs one thing above all else: a Power Core. The Engineer's first mission is to make a single light glow — proof that electricity is flowing and NEXUS is alive.

---

## [THE LAW]

**THE 1ST LAW: THE COMPLETE LOOP**

Electricity needs a complete loop — called a **circuit** — to flow. If the loop is broken anywhere, electricity stops completely. No loop means no flow. No flow means no light, no sound, no movement.

Think of it like a roller coaster. The cart only moves if the tracks make a complete circle back to where they started. If there is a gap in the tracks anywhere — even a tiny one — the cart stops and goes nowhere. Electricity works exactly the same way. It leaves the power source, travels through your components, and must return to the power source to complete the loop.

Your job as a Robot Engineer is to build loops that electricity can travel through.

---

## [BLUEPRINT]

**Circuit Diagram:**

```
  [Arduino]
     |
    5V pin
     |
     +──────────────────────────────+
     |                              |
     |                           (long leg = +)
     |                            [ LED ]
     |                           (short leg = -)
     |                              |
     |                         [220Ω resistor]
     |                              |
    GND pin ───────────────────────+
     |
  [Arduino]
```

**LED Leg Guide:**

```
      LED (side view)
      
    ──(+)──┐
           │  <-- longer leg = POSITIVE (+) faces toward 5V
          ( )
           │  <-- shorter leg = NEGATIVE (-) faces toward GND
    ──(-)──┘
```

**IMPORTANT — Arduino Power Supply Note:**

The Arduino Uno is being used as a **power supply only** in this quest. You will plug it into a USB port on your computer or a USB phone charger. You are NOT uploading any code. You do NOT need to open any software. The Arduino simply converts USB power into a clean 5V output on its 5V pin. Think of it like plugging in a battery — the Arduino just happens to have USB on one end and labeled pins on the other.

**DO NOT** upload any code for this quest. Just plug in the USB cable and the circuit will work on its own.

---

**BREADBOARD WIRING**

The breadboard has rows of holes connected underground. Each short row (A–E and F–J) shares a connection. The long blue and red rails on the sides are also connected the whole length.

```
  BREADBOARD (top view, simplified)

  RED rail   (+) ════════════════════════  <-- connect 5V wire here
  BLUE rail  (-) ════════════════════════  <-- connect GND wire here

  Row 10:  [A10]──[B10]──[C10]──[D10]──[E10]
  Row 11:  [A11]──[B11]──[C11]──[D11]──[E11]
  Row 12:  [A12]──[B12]──[C12]──[D12]──[E12]
  Row 13:  [A13]──[B13]──[C13]──[D13]──[E13]
```

Wire plan for this quest:

```
  Arduino 5V  --> RED rail (+)
  Arduino GND --> BLUE rail (-)

  LED long leg  (+) --> Row 10, hole A
  LED short leg (-) --> Row 11, hole A

  Resistor leg 1 --> Row 11, hole C
  Resistor leg 2 --> Row 13, hole C

  Wire: Row 13, hole E --> BLUE rail (-)
  Wire: RED rail (+)   --> Row 10, hole E
```

---

## [BUILD MISSION]

1. Place the breadboard flat on your workbench in front of you.
2. Find the red LED. Hold it up — notice one leg is longer than the other.
3. Push the LED's LONG leg (+) into hole **A10** on the breadboard.
4. Push the LED's SHORT leg (-) into hole **A11** on the breadboard.
5. Find the 220Ω resistor (Red-Red-Brown-Gold bands). Resistors have no direction — either leg goes in first.
6. Push one leg of the resistor into hole **C11** on the breadboard.
7. Push the other leg of the resistor into hole **C13** on the breadboard.
8. Take a red jumper wire. Push one end into hole **E10**. Push the other end into the RED (+) rail of the breadboard.
9. Take another jumper wire. Push one end into hole **E13**. Push the other end into the BLUE (-) rail of the breadboard.
10. Take a red jumper wire. Connect the Arduino's **5V pin** to the RED (+) rail on the breadboard.
11. Take a black jumper wire. Connect the Arduino's **GND pin** to the BLUE (-) rail on the breadboard.
12. Plug the USB cable into the Arduino Uno.
13. Plug the other end of the USB cable into a computer USB port or USB phone charger.
14. Watch the LED. It should glow red.

**If your circuit doesn't work:**

- Check that the LED's LONG leg faces toward the 5V side (toward the red rail). LEDs only work in one direction.
- Check that every wire and resistor leg is fully pushed into the breadboard hole until it clicks in snugly.
- Check that the resistor connects the SAME row as the LED's short leg on one end.
- Check that your 5V wire goes to the 5V pin on the Arduino — NOT the 3.3V pin next to it.
- Try a different hole on the breadboard — sometimes one hole is damaged.
- Make sure the USB cable is fully inserted into both the Arduino and the power source.

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Power Core

NEXUS now has a beating heart. The red glow you see is proof that electricity is flowing through a complete loop — a loop YOU built. Every robot, every computer, every electronic device on Earth runs on this same idea. You have learned The 1st Law.

**Next Quest:** Q02 — First Light
