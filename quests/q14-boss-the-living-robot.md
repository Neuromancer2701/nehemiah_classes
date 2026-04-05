```
╔══════════════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 14  *** FINAL BOSS ***   ║
║  The Living Robot                            [ ] COMPLETE    ║
╚══════════════════════════════════════════════════════════════╝
```

> **XP Reward:** +25 XP · **Title Unlocked:** MASTER ENGINEER · **Achievement:** NEXUS FULLY ASSEMBLED

---

## PARTS NEEDED

- [ ] Arduino Uno + USB cable
- [ ] Breadboard (large, or two medium boards)
- [ ] 2x LEDs (NEXUS's left and right eyes)
- [ ] 2x 220Ω resistors (Red–Red–Brown) — one for each LED
- [ ] Passive buzzer
- [ ] Push button
- [ ] Photoresistor (LDR)
- [ ] 10kΩ resistor (Brown–Black–Orange)
- [ ] Servo motor (from Elegoo kit — small orange/brown motor with a horn)
- [ ] Jumper wires (you'll need a lot — organize by color if possible)

---

## LORE

The workbench is quiet.

The Engineer stands back and looks at everything laid out in front of them: the eyes, the voice module, the sensor array, the servo arm — every part of NEXUS built across weeks of training. Each one works on its own. Each one was a victory.

But tonight is different. Tonight, they all come together.

The Engineer takes a slow breath. Then begins to wire.

One connection becomes two. Two become ten. The breadboard fills up. Wires arc from component to component like veins carrying electricity instead of blood. The two LEDs sit side by side, ready to become eyes. The passive buzzer waits to speak. The photoresistor watches the room. The button sits ready — the trigger that will let the Engineer send a command.

And at the end of a yellow wire, the servo motor's horn points straight up, waiting to move.

When the last connection is made, the Engineer plugs in the USB cable.

The Serial Monitor opens. Text begins to scroll.

```
╔══════════════════════════════╗
║     NEXUS BOOT SEQUENCE      ║
╠══════════════════════════════╣
║  Loading Brain Module...  OK ║
║  Loading Eye Systems...   OK ║
║  Loading Voice Module...  OK ║
║  Loading Arm Servo...     OK ║
║  Loading Sensors...       OK ║
╚══════════════════════════════╝
```

Four notes chime from the buzzer. The LEDs flash — once, twice, three times. The servo arm sweeps from one side to the other in a slow, deliberate wave.

Then: **"NEXUS FULLY ONLINE. Hello, Engineer. Ready for orders."**

NEXUS is alive.

---

## THE LAW

**THE 14th LAW: THE SYSTEMS LAW**

Every quest before this one taught the Engineer one Law — one skill. One input. One output. One concept at a time.

This is what engineering looks like in the real world: you build small pieces, test each one, and then connect them all into a *system*.

A system is more than a collection of parts. When the pieces work together, NEXUS can do things none of them could do alone:

- The photoresistor tells NEXUS whether it's dark or light.
- The button gives the Engineer a direct command channel.
- The eyes respond to what the sensor reads.
- The buzzer reacts to threats.
- The servo arm signals with motion.

**The cockpit analogy:**
> A pilot doesn't just have one instrument in the cockpit — they have dozens. Altitude, speed, fuel, compass, temperature, engine warning lights. Each instrument does one job. But the pilot reads *all of them together* to understand the full picture and make a decision.
>
> NEXUS's loop works the same way. Every cycle, it checks all its inputs (light sensor, button) and decides what to do with all its outputs (eyes, buzzer, servo). That's a system.

**`#include <Servo.h>`** — Some capabilities are too big to fit in the basic Arduino code. They live in *libraries* — pre-written code that the Engineer can load in. The Servo library comes with the Arduino IDE and knows exactly how to drive a servo motor. `#include` brings it in.

**`const int`** — A variable that never changes. Using `const` tells the Arduino (and the Engineer) "this number is fixed. Don't change it." Good practice for pin numbers.

---

## BLUEPRINT — ALL SYSTEMS

**Component checklist before wiring:**
- [ ] 2x LEDs (left and right eyes)
- [ ] 2x 220Ω resistors (one per LED)
- [ ] Passive buzzer
- [ ] Push button
- [ ] Photoresistor + 10kΩ resistor (voltage divider)
- [ ] Servo motor

**Servo wire color guide:**
| Wire Color          | Connect To     |
|---------------------|----------------|
| Orange or Yellow    | Arduino pin 9 (Signal) |
| Red                 | Arduino 5V     |
| Brown or Black      | Arduino GND    |

> **Note:** Some servos use different colors. If yours doesn't match, the center wire is always signal, and the other two are power and ground (check the bag or try both orientations — a wrongly-wired servo just won't move, it won't break).

**Full wiring diagram:**

```
=== EYES ===
  Pin 7 ──── [220Ω] ──── [LED LEFT  +] [LED LEFT  -] ──── GND
  Pin 8 ──── [220Ω] ──── [LED RIGHT +] [LED RIGHT -] ──── GND

=== VOICE ===
  Pin 6 ──── [Buzzer +]
  GND   ──── [Buzzer -]

=== BUTTON ===
  Pin 2 ──── [Button leg A]
  GND   ──── [Button leg B]
  (INPUT_PULLUP — no resistor needed)

=== OPTICAL SENSOR (voltage divider) ===
  5V ──── [Photoresistor] ──┬──── A0
                            │
                         [10kΩ]
                            │
  GND ──────────────────────┘

=== SERVO ARM ===
  Pin 9  ──── Orange/Yellow wire (Signal)
  5V     ──── Red wire (Power)
  GND    ──── Brown/Black wire (Ground)
```

---

## BUILD MISSION

Take this one section at a time. Build, then test before adding the next part.

**SECTION 1 — Eyes (pins 7 and 8)**

1. Push two LEDs into the breadboard, legs in separate rows. One is the left eye, one is the right.
2. Left eye: connect the **short leg** (–) to **GND**. Connect a 220Ω resistor from the **long leg** (+) to **Arduino pin 7**.
3. Right eye: connect the **short leg** (–) to **GND**. Connect a 220Ω resistor from the **long leg** (+) to **Arduino pin 8**.

**SECTION 2 — Buzzer (pin 6)**

4. Push the passive buzzer into the breadboard.
5. Connect the **longer/+ leg** to **Arduino pin 6**.
6. Connect the **shorter/– leg** to **GND**.

**SECTION 3 — Button (pin 2)**

7. Push the button into the breadboard so it straddles the center gap.
8. Connect one leg on the left side to **Arduino pin 2**.
9. Connect one leg on the right side to **Arduino GND**.

**SECTION 4 — Photoresistor voltage divider (A0)**

10. Push the photoresistor into the breadboard — legs in different rows.
11. Connect one leg to **Arduino 5V**.
12. Connect the other leg to **Arduino A0** AND to one end of the 10kΩ resistor.
13. Connect the other end of the 10kΩ resistor to **Arduino GND**.

**SECTION 5 — Servo (pin 9)**

14. The servo has three wires coming out of it. Identify them by color (see color guide above).
15. Connect the **signal wire** (orange/yellow) to **Arduino pin 9**.
16. Connect the **power wire** (red) to **Arduino 5V**.
17. Connect the **ground wire** (brown/black) to **Arduino GND**.

**Final checks:**
- [ ] Left LED: pin 7 → 220Ω → LED+ | LED– → GND
- [ ] Right LED: pin 8 → 220Ω → LED+ | LED– → GND
- [ ] Buzzer: pin 6 → buzzer+ | buzzer– → GND
- [ ] Button: pin 2 → one leg | other leg → GND
- [ ] Photoresistor: 5V → LDR → A0, same node → 10kΩ → GND
- [ ] Servo: pin 9 (signal), 5V (power), GND (ground)

**If something doesn't work:**
- Upload the code first, then check the Serial Monitor. The boot sequence will print which modules loaded. If something is silent or unmoving, check that specific section's wiring.
- LEDs not lighting? Check polarity (short leg to GND).
- Servo twitching but not moving properly? Make sure it's getting power from 5V (not a digital pin) and its signal is on pin 9.
- Button not working? Check that one leg goes to pin 2 and the other goes to GND (not two legs on the same side of the button, which are always connected internally).
- Buzzer silent? Make sure it's the passive buzzer. Try wiggling the connections — breadboard joints can be loose.

---

## CODE CORE

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — FINAL BOSS Q14
// The Living Robot: NEXUS fully online!
// ============================================

#include <Servo.h>  // Load the servo library (comes built into the Arduino IDE)

// === PIN ASSIGNMENTS — where each part of NEXUS is connected ===
// const int means these numbers never change — they're fixed facts
const int EYE_LEFT  = 7;   // Left LED eye
const int EYE_RIGHT = 8;   // Right LED eye
const int BUZZER    = 6;   // Passive buzzer for voice
const int BUTTON    = 2;   // Command button for the Engineer
const int LIGHT_PIN = A0;  // Photoresistor (optical sensor)
const int SERVO_PIN = 9;   // Servo motor arm

// NEXUS: "Creating my arm control system..."
Servo armServo;  // Create a servo object — this is NEXUS's arm

// Boot melody: C4, E4, G4, C5 — a rising chord announcing NEXUS's arrival
int bootNotes[]     = {262, 330, 392, 523};
int bootDurations[] = {150, 150, 150, 500};

// ============ SETUP — runs once at power-on ============
void setup() {
  // Set up all output and input pins
  pinMode(EYE_LEFT,  OUTPUT);
  pinMode(EYE_RIGHT, OUTPUT);
  pinMode(BUZZER,    OUTPUT);
  pinMode(BUTTON,    INPUT_PULLUP);  // HIGH normally, LOW when pressed

  // NEXUS: "Connecting arm servo on pin 9..."
  armServo.attach(SERVO_PIN);  // Tell the servo library which pin to use
  armServo.write(90);          // Move arm to center position (90 degrees)

  Serial.begin(9600);  // Start communication with the Engineer's computer

  // NEXUS: "All systems ready — running boot sequence!"
  bootSequence();
}

// ============ BOOT SEQUENCE — the dramatic startup ============
void bootSequence() {
  // NEXUS: "Printing boot status to Engineer..."
  Serial.println("╔══════════════════════════════╗");
  Serial.println("║     NEXUS BOOT SEQUENCE      ║");
  Serial.println("╠══════════════════════════════╣");
  Serial.println("║  Loading Brain Module...  OK ║");
  Serial.println("║  Loading Eye Systems...   OK ║");
  Serial.println("║  Loading Voice Module...  OK ║");
  Serial.println("║  Loading Arm Servo...     OK ║");
  Serial.println("║  Loading Sensors...       OK ║");
  Serial.println("╚══════════════════════════════╝");

  // NEXUS: "Playing boot melody..."
  for (int i = 0; i < 4; i++) {
    tone(BUZZER, bootNotes[i], bootDurations[i]);
    delay(bootDurations[i] + 50);  // Wait for each note to finish
  }
  noTone(BUZZER);  // Silence after melody

  // NEXUS: "Flashing eyes to confirm optical systems online..."
  for (int i = 0; i < 3; i++) {
    digitalWrite(EYE_LEFT,  HIGH);
    digitalWrite(EYE_RIGHT, HIGH);
    delay(250);
    digitalWrite(EYE_LEFT,  LOW);
    digitalWrite(EYE_RIGHT, LOW);
    delay(250);
  }

  // NEXUS: "Sweeping arm to confirm servo range..."
  armServo.write(0);    delay(500);   // Sweep left
  armServo.write(180);  delay(500);   // Sweep right
  armServo.write(90);   delay(300);   // Return to center

  // NEXUS: "Boot complete. Greeting Engineer."
  Serial.println("");
  Serial.println("NEXUS FULLY ONLINE.");
  Serial.println("Hello, Engineer. Ready for orders.");
  Serial.println("");
}

// ============ MAIN LOOP — runs forever, checking and responding ============
void loop() {
  // NEXUS: "Scanning all sensors..."
  int light  = analogRead(LIGHT_PIN);  // Read light level (0 = dark, 1023 = bright)
  int button = digitalRead(BUTTON);    // Read button (HIGH = not pressed, LOW = pressed)

  // ---- MODE 1: DARK MODE — room is dark, glow steady to light the way ----
  if (light < 300) {
    // NEXUS: "Dark environment detected. Activating steady glow mode."
    digitalWrite(EYE_LEFT,  HIGH);
    digitalWrite(EYE_RIGHT, HIGH);

    Serial.print("Light: "); Serial.print(light);
    Serial.println(" [DARK MODE — steady glow active]");
    delay(200);

  // ---- MODE 2: ALERT MODE — Engineer pressed the button! ----
  } else if (button == LOW) {
    // NEXUS: "ALERT signal received from Engineer! Initiating alert sequence!"
    Serial.println("!!! ALERT MODE ACTIVATED !!!");

    // Alternate eyes rapidly + alarm tones + arm wave — all at once
    for (int i = 0; i < 8; i++) {
      // Alternate which eye is on (i % 2 checks if i is even or odd)
      digitalWrite(EYE_LEFT,  i % 2 == 0 ? HIGH : LOW);
      digitalWrite(EYE_RIGHT, i % 2 == 0 ? LOW  : HIGH);

      // Alternate between high and low alarm tones (880 Hz and 440 Hz)
      tone(BUZZER, i % 2 == 0 ? 880 : 440, 100);

      delay(150);  // Short delay between flashes
    }

    // NEXUS: "Alert sequence complete. Returning to standby."
    noTone(BUZZER);
    digitalWrite(EYE_LEFT,  LOW);
    digitalWrite(EYE_RIGHT, LOW);

    // NEXUS: "Waving arm to signal alert completion..."
    armServo.write(30);   delay(200);
    armServo.write(150);  delay(200);
    armServo.write(90);   // Return to center

  // ---- MODE 3: NORMAL MODE — all clear, slow blinking standby ----
  } else {
    // NEXUS: "All clear. Normal standby mode. Slow blink cycle active."
    Serial.print("Light: "); Serial.print(light);
    Serial.println(" [NORMAL MODE — slow blink]");

    // Slow, calm blink — NEXUS is watching but relaxed
    digitalWrite(EYE_LEFT,  HIGH);
    digitalWrite(EYE_RIGHT, HIGH);
    delay(700);
    digitalWrite(EYE_LEFT,  LOW);
    digitalWrite(EYE_RIGHT, LOW);
    delay(700);
  }
}
```

---

## XP REWARD

```
╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║               *** +25 XP EARNED ***                         ║
║                                                              ║
║         ROBOT PART: ALL SYSTEMS — NEXUS ASSEMBLED           ║
║                                                              ║
║           *** TITLE UNLOCKED: MASTER ENGINEER ***           ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

---

```
╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║         * * * * * NEXUS IS ALIVE * * * * *                  ║
║                                                              ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  Engineer Nehemiah —                                         ║
║                                                              ║
║  You started this journey with an empty breadboard and      ║
║  a handful of parts. You didn't know what a resistor was.   ║
║  You didn't know what a circuit was. You didn't know why    ║
║  LEDs need resistors, or how a button sends a signal, or    ║
║  why some pins have a ~ next to them.                        ║
║                                                              ║
║  Now you do.                                                 ║
║                                                              ║
║  You learned The Laws — the rules that govern electricity   ║
║  itself. You debugged when things went wrong (because they  ║
║  always do — for every Engineer, always). You read          ║
║  schematics. You wrote real code. You built real things     ║
║  that work in the real world.                               ║
║                                                              ║
║  And right now, NEXUS is sitting on your workbench,         ║
║  blinking its LED eyes, reading the temperature of the      ║
║  room, listening for your button press, ready to respond.   ║
║                                                              ║
║  You built that. Every wire. Every line of code.            ║
║  Every single part of NEXUS came from your hands.           ║
║                                                              ║
║  That's not a toy. That's engineering.                       ║
║                                                              ║
║  NEXUS ROBOT PARTS COLLECTED:                               ║
║    [x] Brain Module         (Quest 07)                       ║
║    [x] Communication Array  (Quest 08)                       ║
║    [x] Command Interface    (Quest 09)                       ║
║    [x] Input System         (Quest 10)                       ║
║    [x] Optical Sensor       (Quest 11)                       ║
║    [x] Voice Module         (Quest 12)                       ║
║    [x] Environment Sensor   (Quest 13)                       ║
║    [x] Full Integration     (Quest 14)                       ║
║                                                              ║
║  NEXUS STATUS: *** FULLY ASSEMBLED AND ONLINE ***           ║
║                                                              ║
║  What will the Engineer build next?                         ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```
