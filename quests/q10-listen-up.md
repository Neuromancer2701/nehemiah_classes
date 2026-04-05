╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 10               ║
║  LISTEN UP                         [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Input Processor

---

## PARTS NEEDED

- [ ] Arduino Uno R3 board
- [ ] USB cable (connected to your computer)
- [ ] Arduino IDE installed and open
- [ ] 1x push button (from the Elegoo kit)
- [ ] 1x LED (any color)
- [ ] 1x 220Ω resistor (red-red-brown-gold stripes)
- [ ] Breadboard
- [ ] 3x jumper wires

---

## [LORE]

The Comm Link was active. NEXUS could speak. But the conversation was one-sided.

NEXUS sent messages. NEXUS blinked. NEXUS reported status. But NEXUS could not listen. NEXUS could not receive a command from the Engineer and respond to it. Every interaction flowed in one direction only: from NEXUS to the Engineer.

A robot that cannot receive commands is not a companion — it is just a machine running a program. NEXUS was designed to work with the Engineer, not just beside them.

The Input Processor changes everything. It is the part of NEXUS that listens. With it installed, the Engineer can press a button and NEXUS will respond. The Engineer gives a command. NEXUS hears it. NEXUS acts on it.

This is the moment where NEXUS stops just performing and starts responding. This is the moment the connection goes both ways.

NEXUS: *"Input terminal detected. Ready to receive commands, Engineer."*

---

## [THE LAW]

**THE 10TH LAW: THE GUARD AT THE DOOR**

`digitalRead(pin)` reads whether a pin is receiving electricity — HIGH means yes, LOW means no. With `INPUT_PULLUP`, the pin reads HIGH normally and LOW when the button is pressed. `if` statements let the Arduino make decisions: "IF this is true, do this. OTHERWISE, do that."

**Analogy:** Imagine a guard standing at a door. The guard has one job: check if a visitor arrives.

- `digitalRead(buttonPin)` is the guard looking at the door right now. Is someone there?
- The `if` statement is the guard's rulebook: "**IF** someone is at the door, open it. **OTHERWISE**, keep it closed."
- `INPUT_PULLUP` is a special setting — it means the pin is connected to 5V inside the Arduino by default. This keeps the reading stable at HIGH when the button is not pressed. When you press the button and connect the pin to GND, the reading drops to LOW. So: **button NOT pressed = HIGH. Button pressed = LOW.** This seems backwards, but it is the most reliable way to read a button.

The Arduino checks the button every single time the loop runs — millions of times per second. So when the button is pressed even briefly, the Arduino catches it immediately.

---

## [BLUEPRINT]

### CIRCUIT DIAGRAM

```
Arduino Board
┌─────────────────────────────────────┐
│                                     │
│  Pin 2  ────────────────────────────┼──── Button leg 1
│                                     │         │
│                                     │    [BUTTON]
│                                     │         │
│  GND ───────────────────────────────┼──── Button leg 2 (diagonal corner)
│                                     │
│  Pin 13 ────────────────────────────┼──── LED long leg (+)
│                                     │         │
│                                     │     LED short leg (-)
│                                     │         │
│  GND ───────────────────────────────┼──── [220Ω resistor] ────┘
│                                     │
└─────────────────────────────────────┘
```

---

### BUTTON LEG GUIDE

A push button from your kit has 4 legs. This is confusing at first — here is how to read it:

```
  Button — top view:

  Leg A ──┐     ┌── Leg B
          │     │
          │ BTN │      ← pressing the button connects A-side to B-side
          │     │
  Leg C ──┘     └── Leg D

  Leg A and Leg C are ALREADY connected to each other (same side).
  Leg B and Leg D are ALREADY connected to each other (same side).
  Pressing the button connects the A/C side TO the B/D side.
```

**For this circuit you need ONE leg from each side:**
- One wire goes from Pin 2 to Leg A (or Leg C — same thing)
- One wire goes from GND to Leg B (or Leg D — same thing)

The button sits across the middle gap of the breadboard — one set of legs on each side of the gap. This is the correct way to place it.

**How to place it on the breadboard:**

```
BREADBOARD CENTER GAP:

     columns:  1   2   3   4   5  │  6   7   8   9  10
           a  [ ] [A] [ ] [ ] [ ] │ [ ] [B] [ ] [ ] [ ]
           b  [ ] [C] [ ] [ ] [ ] │ [ ] [D] [ ] [ ] [ ]
                                  │
                              CENTER GAP

Push the button so legs A and C are on the LEFT side of the gap,
and legs B and D are on the RIGHT side of the gap.
```

Connect Pin 2 to row A (left side). Connect GND to row B (right side).

---

### BREADBOARD WIRING — STEP BY STEP

**Button wiring:**

1. Push the button across the center gap of the breadboard. One pair of legs on each side of the gap. Press firmly until the button clicks into place.
2. Connect a jumper wire from **Arduino Pin 2** to the same breadboard row as Leg A of the button (left side of gap).
3. Connect a jumper wire from **Arduino GND** to the same breadboard row as Leg B of the button (right side of gap).

**LED wiring (same as Quest 08):**

4. Push the LED into the breadboard. Long leg (+) in one hole, short leg (-) in the next hole.
5. Push one leg of the 220Ω resistor into the same row as the LED's short leg (-).
6. Push the other resistor leg into a new empty row.
7. Connect a jumper wire from the LED's long leg (+) row to **Arduino Pin 13**.
8. Connect a jumper wire from the far resistor leg row to **Arduino GND**.

---

## [BUILD MISSION]

1. Unplug the Arduino from the computer before wiring.
2. Place the push button across the center gap of the breadboard.
3. Wire the button: Pin 2 to one side, GND to the other side (see the button leg guide above).
4. Wire the LED with the 220Ω resistor: Pin 13 to LED long leg, short leg to resistor, resistor to GND.
5. Plug the USB cable back in. Check that the green power LED is on.
6. Open the Arduino IDE and type the code from the CODE CORE section.
7. Click Verify (checkmark). Fix any errors. Click Upload (right arrow).
8. Wait for "Done uploading."
9. Open the Serial Monitor. Set speed to 9600 baud.
10. Press the button. Watch the LED and the Serial Monitor at the same time.

**If your circuit doesn't work:**
- Is the button placed across the center gap? Both sides of the gap must each have one leg. If all 4 legs are on the same side of the gap, the button will not work.
- Is Pin 2 connected to the correct side of the button? Try swapping the two button wires.
- Is the LED in backwards? Flip it around.
- Is the resistor connected between the LED's short leg and GND?
- Try pressing the Reset button on the Arduino and watching the Serial Monitor — does "NEXUS INPUT PROCESSOR ONLINE" appear? If yes, the code uploaded correctly and the problem is only in the wiring.
- Try holding the button for a full second — sometimes a quick tap gets missed during debugging.

---

## [CODE CORE]

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — QUEST 10
// Listen Up: NEXUS responds to commands!
// ============================================

int buttonPin = 2;   // Button is connected to pin 2
int ledPin    = 13;  // LED (NEXUS eye) is on pin 13
// These variables give our pins friendly names
// so we can use the names instead of numbers throughout the code

void setup() {
  // NEXUS: "Configuring input terminal..."
  // Button is an INPUT — it sends information TO the Arduino
  // INPUT_PULLUP means: pin is connected to 5V inside the Arduino by default
  // This keeps the reading at HIGH when the button is NOT pressed
  // When the button IS pressed, it connects pin 2 to GND, pulling it LOW
  // Result: NOT pressed = HIGH, Pressed = LOW
  pinMode(buttonPin, INPUT_PULLUP);

  // NEXUS: "Configuring output eye..."
  // LED is an OUTPUT — Arduino sends electricity TO it
  pinMode(ledPin, OUTPUT);

  // NEXUS: "Opening comm channel..."
  Serial.begin(9600);                            // Start serial communication at 9600 baud

  // NEXUS: "Sending startup message..."
  Serial.println("NEXUS INPUT PROCESSOR ONLINE");    // Print startup line 1
  Serial.println("Press button to activate eye.");    // Print startup line 2
}

void loop() {
  // NEXUS: "Checking input terminal..."
  // digitalRead() checks if the pin is receiving electricity right now
  // It returns HIGH (electricity) or LOW (no electricity)
  // We store the result in a variable called buttonState
  int buttonState = digitalRead(buttonPin);
  // buttonState is LOW when pressed, HIGH when not pressed
  // (This is because we used INPUT_PULLUP — see setup() above)

  if (buttonState == LOW) {
    // NEXUS: "Command received! Activating eye!"
    // The == means "is equal to" — we are asking: is buttonState equal to LOW?
    // If YES, run the code inside these curly braces { }
    digitalWrite(ledPin, HIGH);                    // Turn the LED ON
    Serial.println("BUTTON PRESSED — Eye ON");     // Report to Engineer
  } else {
    // NEXUS: "No command. Eye standing by."
    // If the button is NOT pressed (buttonState is HIGH), run this instead
    digitalWrite(ledPin, LOW);  // Turn the LED OFF
    // No Serial message here — we don't print anything when nothing is pressed
    // (Printing every loop when not pressed would flood the monitor with messages)
  }

  // loop() runs this whole block over and over
  // The Arduino checks the button millions of times per second
  // So it catches every single button press, no matter how quick
}
```

---

### UNDERSTANDING THE CODE

**`int buttonState = digitalRead(buttonPin);`**
This creates a variable called `buttonState` and immediately fills it with the reading from pin 2. `digitalRead()` returns either the value `HIGH` or the value `LOW`. The variable stores that answer so the `if` statement can use it.

**`if (buttonState == LOW) { ... } else { ... }`**
This is a decision. The Arduino asks: "Is buttonState equal to LOW?" If yes, it runs the code inside the first set of curly braces. If no, it runs the code inside the `else` curly braces. The Arduino picks one path or the other — never both.

**Why `==` and not `=`?**
One equals sign `=` means "put this value into this variable." Two equals signs `==` means "is this value equal to that value?" They look similar but do completely different things. This is one of the most common mistakes in all of programming. The Engineer must remember: `=` assigns, `==` compares.

**Why does pressing the button give LOW instead of HIGH?**
Because `INPUT_PULLUP` connects the pin to 5V (HIGH) by default. When the button is pressed, it connects the pin to GND (LOW) instead. The button does not add electricity — it removes it. LOW means "the button is closing the circuit to ground." This is the standard, reliable way to wire a button.

---

### CHALLENGE

**Challenge 1 — Delayed response:** Can you make the LED stay ON for 2 seconds after the button is released? Try adding `delay(2000)` inside the `if (buttonState == LOW)` block, after the `digitalWrite`. Upload and test.

**Challenge 2 — Two LEDs:** Add a second LED on pin 12. Wire it the same way as pin 13 (with its own 220Ω resistor to GND). In the code, add `pinMode(12, OUTPUT);` in setup. Then make the second LED do the OPPOSITE: light up when the button is NOT pressed, turn off when the button IS pressed. Put `digitalWrite(12, LOW);` inside the `if` block and `digitalWrite(12, HIGH);` inside the `else` block.

This means one LED is your "command received" light and the other is your "standing by" light — like the green and red lights on a control panel.

**Challenge 3 — Count the presses:** What if NEXUS counted how many times the button was pressed and reported the total? This requires a new concept called a counter variable. Try this structure:

```cpp
int pressCount = 0;  // Start the counter at zero (put this at the very top, outside setup and loop)

// Then inside the if block:
pressCount = pressCount + 1;        // Add 1 to the counter
Serial.print("Press count: ");      // Print the label (no new line)
Serial.println(pressCount);         // Print the number (with new line)
delay(300);                         // Short pause to avoid counting one press multiple times
```

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Input Processor

*NEXUS status: Input Processor installed. NEXUS can now receive commands from the Engineer. The connection is no longer one-way. The Engineer acts. NEXUS responds. That is the difference between a machine and a companion.*

**Next Quest:** Q11 — Bright Ideas (LED brightness control with PWM)
**Side Quest Unlocked:** SQ02 — Morse Code (Use what you know to blink messages in Morse code)
