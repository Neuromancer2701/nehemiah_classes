╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 08               ║
║  FIRST WORDS                       [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Program Core

---

## PARTS NEEDED

- [ ] Arduino Uno R3 board
- [ ] USB cable (connected to your computer)
- [ ] Arduino IDE installed and set up (from Quest 07)
- [ ] 1x LED (any color)
- [ ] 1x 220Ω resistor (red-red-brown-gold stripes)
- [ ] Breadboard
- [ ] 2x jumper wires

---

## [LORE]

The Brain Module was in place. The Engineer held the Arduino board in both hands and stared at the ATmega328P chip at the center.

*"You understand what this is,"* the transmission said. *"Now teach it what to do."*

A robot with a brain but no instructions is like a chef handed a blank recipe card. The brain is ready — it is waiting. The very first instruction any engineer gives a new robot is the simplest one possible: blink.

One eye. On. Off. On. Off.

It seems small. But this is the first time electricity will flow because of words the Engineer wrote. This is the first time NEXUS will do something because the Engineer told it to. Every complex program ever written — every robot, every video game, every app on every phone — started here. With a single light turning on and off.

When that LED blinks for the first time, something changes. The Engineer is no longer just studying circuits. The Engineer is now a programmer.

NEXUS: *"Awaiting first instruction..."*

---

## [THE LAW]

**THE 8TH LAW: THE RECIPE CARD**

Code is a list of instructions. The Arduino runs `setup()` once at the very start, then runs `loop()` over and over forever. `digitalWrite(pin, HIGH)` sends electricity to a pin. `delay(ms)` pauses for that many milliseconds. 1000 milliseconds equals exactly 1 second.

**Analogy:** Think of a robot chef following a recipe card. The recipe has two sections:

- **"Prepare your workspace"** — this is `setup()`. The robot reads this section once, gets everything ready, and never reads it again.
- **"Repeat this recipe forever"** — this is `loop()`. The robot reads this section, does every step in order, reaches the end, then immediately jumps back to the top and starts again. Forever.

Inside the loop, `delay(1000)` is the recipe saying: "Wait 1 second before the next step." The robot waits exactly 1 second — not a moment more, not a moment less — and then continues.

`digitalWrite(ledPin, HIGH)` means: "Send electricity out through this pin." HIGH = electricity on. LOW = electricity off.

The Arduino does not guess. It does not improvise. It follows the recipe card exactly, every single time.

---

## [BLUEPRINT]

### CIRCUIT DIAGRAM

```
Arduino Board
┌─────────────────────────────────┐
│                                 │
│  Pin 13 ────────────────────────┼──── LED long leg (+)
│                                 │         │
│                                 │     LED short leg (-)
│                                 │         │
│  GND ───────────────────────────┼──── [220Ω resistor] ────┘
│                                 │
└─────────────────────────────────┘
```

**Current path:** Pin 13 → LED (+) → LED (-) → 220Ω resistor → GND

The resistor is a safety device — it slows the electricity down so it does not burn out the LED. The 220Ω resistor is the right size for a 5V Arduino powering a standard LED. Always use a resistor with an LED.

---

### BREADBOARD WIRING — STEP BY STEP

A breadboard is a plastic block full of tiny metal clips. Wires plugged into the same row are connected to each other. Use this to build your circuit without soldering.

```
BREADBOARD (top view, rows A through J, columns 1-30)

      1   2   3   4   5   6   7   8 ...
  a [ ] [ ] [ ] [ ] [ ] [ ] [ ] [ ]
  b [ ] [ ] [ ] [ ] [ ] [ ] [ ] [ ]
  c [ ] [W] [ ] [+] [-] [R] [ ] [ ]   ← your components
  d [ ] [W] [ ] [ ] [ ] [R] [ ] [ ]
  e [ ] [ ] [ ] [ ] [ ] [W] [ ] [ ]

  W = wire connection
  + = LED long leg (positive)
  - = LED short leg (negative)
  R = resistor leg
```

**Step 1:** Push the LED into the breadboard. Long leg (+) in one hole, short leg (-) in the hole right next to it. (Leave one empty column between the long and short leg.)

**Step 2:** Push one leg of the 220Ω resistor into the same row as the LED's short leg (-). Push the other resistor leg into a different row (it will connect to GND).

**Step 3:** Use a jumper wire to connect the LED's long leg (+) row to **digital pin 13** on the Arduino.

**Step 4:** Use a jumper wire to connect the far end of the resistor to any **GND** pin on the Arduino.

**Double-check:** Electricity will travel: Pin 13 → wire → LED long leg → through LED → LED short leg → resistor → wire → GND.

> **NOTE:** Pin 13 also has a tiny built-in LED directly on the Arduino board. Even if you do not wire an external LED, you will still see the board's own LED blink when pin 13 goes HIGH. You can test the code with just the board if you prefer.

---

## [BUILD MISSION]

1. Make sure the Arduino is NOT plugged in yet. Always wire first, then power.
2. Push the LED into the breadboard — long leg in row C3, short leg in row C4 (or wherever you have space).
3. Push one leg of the 220Ω resistor into the same row as the LED's short leg.
4. Push the other resistor leg into a new empty row.
5. Connect a jumper wire from the LED's long leg row to **pin 13** on the Arduino.
6. Connect a jumper wire from the far resistor leg row to a **GND** pin on the Arduino.
7. Plug the USB cable into the Arduino and into the computer.
8. Check that the green power LED on the Arduino is lit — power is on.
9. Open the Arduino IDE on the computer.
10. Type the code from the CODE CORE section below exactly as written (or paste it).
11. Click the **checkmark button** (Verify) at the top-left. Wait for "Done compiling" at the bottom. If there are red error messages, read them carefully and check for typos.
12. Click the **right-arrow button** (Upload). Wait for "Done uploading" at the bottom.
13. Watch the LED. It should blink on for 1 second, off for 1 second, on for 1 second... forever.

**If your circuit doesn't work:**
- Is the power LED on? If not, the Arduino is not getting power — check the USB cable.
- Is the LED in backwards? LEDs only work one direction. Try flipping it around.
- Is the resistor connected between the LED's short leg and GND? Check every connection.
- Did the IDE say "Done uploading"? If not, go to Tools → Board and Tools → Port and check both are set correctly.
- Is there a red squiggly line in the code? That means a typo — look for a missing semicolon `;` or a missing bracket `}`.
- When in doubt, unplug the USB cable, remove every wire, and rebuild the circuit one step at a time.

---

## [CODE CORE]

Type this exactly into the Arduino IDE. Every line has a comment explaining what it does.

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — QUEST 08
// First Words: Making NEXUS blink!
// ============================================

// Tell the Arduino: NEXUS's eye is on pin 13
int ledPin = 13;

void setup() {
  // NEXUS: "Setting up my eye..."
  // Set pin 13 as OUTPUT — it will SEND electricity out
  pinMode(ledPin, OUTPUT);
}

void loop() {
  // NEXUS: "Eye ON!"
  digitalWrite(ledPin, HIGH);  // Send electricity to pin 13 (LED turns ON)
  delay(1000);                  // Wait 1000 milliseconds (1 second)

  // NEXUS: "Eye OFF!"
  digitalWrite(ledPin, LOW);   // Stop electricity to pin 13 (LED turns OFF)
  delay(1000);                  // Wait 1000 milliseconds (1 second)

  // (Now loop() starts over from the top — forever!)
}
```

### HOW TO UPLOAD YOUR CODE

1. Type the code into Arduino IDE (or copy it in)
2. Click the **checkmark button** (Verify) — it checks for mistakes. Wait for "Done compiling."
3. If there are red error messages: find the typo, fix it, click Verify again.
4. Click the **right-arrow button** (Upload) — this sends the code to the Arduino.
5. Wait for "Done uploading" to appear at the bottom of the screen.
6. Watch your LED blink!

---

### UNDERSTANDING THE CODE

**`int ledPin = 13;`**
This creates a variable named `ledPin` and gives it the value 13. A variable is like a labeled box that holds a number. Now whenever the code says `ledPin`, the Arduino knows it means pin 13. This makes the code easier to read and easier to change later.

**`void setup() { ... }`**
Everything inside the curly braces `{ }` runs once when the Arduino first turns on or resets. Setup happens first, every time.

**`pinMode(ledPin, OUTPUT);`**
This tells the Arduino: "Pin 13 is going to SEND electricity out — it is an OUTPUT." Every pin must be told whether it is an input or an output before you use it.

**`void loop() { ... }`**
Everything inside runs over and over, forever. When the Arduino reaches the closing `}`, it immediately jumps back to the opening `{` and starts again.

**`digitalWrite(ledPin, HIGH);`**
Sends 5 volts of electricity out through pin 13. HIGH = electricity on. The LED lights up.

**`delay(1000);`**
Pauses everything for 1000 milliseconds (1 second). The Arduino does nothing during a delay — it just waits.

**`digitalWrite(ledPin, LOW);`**
Turns off pin 13. LOW = no electricity. The LED goes dark.

---

### CHALLENGE

The Engineer has proven the circuit and the code work. Now experiment:

**Challenge 1 — Fast Blink:** Change both `delay(1000)` values to `delay(100)`. Upload the code. What happens?

**Challenge 2 — Slow Blink:** Change both delays to `delay(2000)`. Upload again. How does it feel different?

**Challenge 3 — Uneven Blink:** Make the ON delay different from the OFF delay. Try `delay(200)` for ON and `delay(1000)` for OFF. What does it look like? Does it look like a heartbeat?

**Challenge 4 — Your Own Pattern:** Pick any two delay values. Upload. Show someone else and describe what you did to make it happen.

There are no wrong answers in the challenge section. All of these work — you are experimenting like a real engineer.

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Program Core

*NEXUS status: Program Core installed. NEXUS is now running code written by the Engineer. The eye blinks. Instructions are being followed. The brain is alive.*

**Next Quest:** Q09 — Talking to Your Robot
