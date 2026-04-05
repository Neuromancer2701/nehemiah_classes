```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — SIDE QUEST 02          ║
║  Morse Code Transmitter               [ ] COMPLETE   ║
╚══════════════════════════════════════════════════════╝
```

> **XP Reward:** +5 XP · **Unlocked by:** Q10 — Listen Up
> **Robot Upgrade:** NEXUS can transmit secret messages

---

## PARTS NEEDED

- [ ] Arduino Uno + USB cable
- [ ] Breadboard
- [ ] LED (any color)
- [ ] 220Ω resistor (Red–Red–Brown)
- [ ] Jumper wires

---

## LORE

Before radio had voices. Before phones had screens. Before the internet carried words across the world in milliseconds — there was Morse code.

Ships at sea, soldiers in the field, and telegraph operators in every city used it: a system of short blinks and long blinks that spelled out letters. Dots and dashes. Simple. Reliable. Unstoppable.

NEXUS can do the same thing. Not with sound waves across an ocean, but with an LED blinking on a breadboard. The Engineer programs it once — and NEXUS can transmit any message the Engineer writes, in the same code that kept the world connected for over a hundred years.

Today, the Engineer teaches NEXUS to spell its own name in light.

---

## THE LAW

**THE FUNCTION LAW (Side Quest Edition)**

The Engineer has been writing code in one long sequence — setup at the top, loop in the middle, everything in order. But what happens when you need to do the same task over and over in different parts of the code?

You write a **function**.

A function is a named, reusable block of code. You write it once, give it a name, and *call* it anywhere you need it — just by using that name.

**The recipe card analogy:**
> Imagine you're baking and you need to make a sauce. You could write out all the sauce instructions every time you need sauce — in the middle of the pasta recipe, the middle of the pizza recipe, the middle of the lasagna recipe.
>
> Or you could write the sauce recipe on its own card, call it "MAKE SAUCE," and just write "see MAKE SAUCE card" whenever you need it.
>
> Functions work exactly like that. `dot()` is one recipe card. `dash()` is another. Whenever you want a dot, you just call `dot()`.

```cpp
void dot() {
  // This is the recipe for one dot
  digitalWrite(ledPin, HIGH);  // light on
  delay(200);                  // for 200ms
  digitalWrite(ledPin, LOW);   // light off
  delay(200);                  // brief gap after
}
```

Once defined, `dot()` can be called anywhere in the code. Write it once, use it a thousand times.

---

## BLUEPRINT

```
  Arduino pin 13 ──── [220Ω] ──── [LED +] [LED -] ──── GND
```

Pin 13 has a built-in LED on the Arduino board itself — so this quest works even without an external LED if needed. But wiring your own makes it easier to see.

---

## BUILD MISSION

1. Push the LED into the breadboard. Longer leg is + (anode).
2. Connect the **shorter leg** (–) to **Arduino GND**.
3. Connect a **220Ω resistor** from the **longer leg** (+) to **Arduino pin 13**.

**Check your work:**
- [ ] LED short leg → GND
- [ ] LED long leg → 220Ω → pin 13

**If your circuit doesn't work:**
- Is the LED backwards? Flip it.
- Try changing `ledPin = 13` to `ledPin = 12` in the code, then rewire to pin 12.
- Pin 13 on an Arduino also has its own built-in onboard LED — if the LED on the board is blinking but your external one isn't, check the resistor and polarity.

---

## MORSE CODE REFERENCE CHART

Keep this at the workbench. Every letter, every number.

```
A  .-      N  -.
B  -...    O  ---
C  -.-.    P  .--.
D  -..     Q  --.-
E  .       R  .-.
F  ..-.    S  ...
G  --.     T  -
H  ....    U  ..-
I  ..      V  ...-
J  .---    W  .--
K  -.-     X  -..-
L  .-..    Y  -.--
M  --      Z  --..

1  .----   6  -....
2  ..---   7  --...
3  ...--   8  ---..
4  ....-   9  ----.
5  .....   0  -----

SOS (emergency):  ... --- ...
```

**NEXUS in Morse code:** `-.  .  -..-  ..-  ...`

| Letter | Morse  |
|--------|--------|
| N      | -.     |
| E      | .      |
| X      | -..-   |
| U      | ..-    |
| S      | ...    |

---

## CODE CORE

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — SIDE QUEST 02
// Morse Code: NEXUS transmits its own name!
// ============================================

int ledPin = 13;  // LED on pin 13 (also the onboard LED)

// NEXUS: "Loading timing constants for Morse code..."
// Morse code timing is all based on one unit (200ms here)
int DOT_TIME    = 200;  // A dot lasts 200ms
int DASH_TIME   = 600;  // A dash lasts 3x as long as a dot (600ms)
int GAP_TIME    = 200;  // Gap between signals within the same letter
int LETTER_GAP  = 400;  // Longer gap between letters
int WORD_GAP    = 800;  // Even longer gap between words

// ============ FUNCTION: dot() — one short blink ============
// NEXUS: "Executing dot signal..."
void dot() {
  digitalWrite(ledPin, HIGH);  // LED on
  delay(DOT_TIME);             // Hold for dot duration
  digitalWrite(ledPin, LOW);   // LED off
  delay(GAP_TIME);             // Brief pause after signal
}

// ============ FUNCTION: dash() — one long blink ============
// NEXUS: "Executing dash signal..."
void dash() {
  digitalWrite(ledPin, HIGH);  // LED on
  delay(DASH_TIME);            // Hold for dash duration (3x longer)
  digitalWrite(ledPin, LOW);   // LED off
  delay(GAP_TIME);             // Brief pause after signal
}

// ============ FUNCTION: letterGap() — pause between letters ============
// NEXUS: "Inserting inter-letter gap..."
void letterGap() {
  delay(LETTER_GAP);  // Pause so letters don't blur together
}

// ============ FUNCTION: wordGap() — pause between words ============
// NEXUS: "Inserting word gap..."
void wordGap() {
  delay(WORD_GAP);  // Longer pause between words
}

// ============ LETTER FUNCTIONS — each letter is a recipe ============

// N = -.
void morse_N() {
  dash(); dot();
  letterGap();
}

// E = .
void morse_E() {
  dot();
  letterGap();
}

// X = -..-
void morse_X() {
  dash(); dot(); dot(); dash();
  letterGap();
}

// U = ..-
void morse_U() {
  dot(); dot(); dash();
  letterGap();
}

// S = ...
void morse_S() {
  dot(); dot(); dot();
  letterGap();
}

// ============ SETUP ============
void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
  Serial.println("NEXUS MORSE TRANSMITTER ONLINE");
  Serial.println("Transmission: N-E-X-U-S");
}

// ============ MAIN LOOP ============
void loop() {
  // NEXUS: "Beginning transmission... spelling N-E-X-U-S in Morse code..."
  Serial.println("Transmitting: NEXUS");
  Serial.println("  N = -.");
  morse_N();

  Serial.println("  E = .");
  morse_E();

  Serial.println("  X = -..-");
  morse_X();

  Serial.println("  U = ..-");
  morse_U();

  Serial.println("  S = ...");
  morse_S();

  // NEXUS: "Transmission complete. Pausing before repeat..."
  Serial.println("Transmission complete. Pausing 3 seconds.");
  wordGap();
  delay(2000);  // Extra pause before repeating
}
```

---

## CHALLENGE MISSIONS

**Challenge 1 — Spell Your Name:**
Look up each letter of your name in the Morse code chart. Write a function for each letter (like `morse_N()`, `morse_E()`, etc.), then call them in order in the loop. Now NEXUS can transmit your name.

**Challenge 2 — SOS Signal:**
SOS is the international emergency signal: `... --- ...` (three dots, three dashes, three dots). Write a `morse_SOS()` function and have NEXUS repeat it with a long pause between transmissions. What happens if you speed it up by changing `DOT_TIME` to 100?

**Challenge 3 — Secret Message:**
Write out any short word in Morse code using the chart. Program NEXUS to transmit it. Challenge a friend or family member: can they decode it using just the chart?

**Challenge 4 — Speed Control:**
The `DOT_TIME` constant controls the speed of the whole transmission (since everything else is based on it). Change it to 100 for fast, urgent-sounding Morse. Change it to 500 for slow and deliberate. Real telegraph operators could send and receive 20–30 words per minute. What's your best speed?

---

## XP REWARD

```
╔══════════════════════════════════════════════════════╗
║  SIDE QUEST 02 COMPLETE                              ║
║  +5 XP EARNED                                        ║
║  NEXUS CAN NOW TRANSMIT SECRET MESSAGES              ║
╚══════════════════════════════════════════════════════╝
```
