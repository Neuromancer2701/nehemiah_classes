```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 11               ║
║  Eyes of the Robot                    [ ] COMPLETE   ║
╚══════════════════════════════════════════════════════╝
```

> **XP Reward:** +10 XP · **Robot Part Unlocked:** Optical Sensor

---

## PARTS NEEDED

- [ ] Arduino Uno + USB cable
- [ ] Breadboard
- [ ] Photoresistor (LDR — the squiggly-line disc)
- [ ] 10kΩ resistor (Brown–Black–Orange stripes)
- [ ] LED (any color)
- [ ] 220Ω resistor (Red–Red–Brown stripes)
- [ ] Jumper wires

---

## LORE

The Engineer stares at the workbench. NEXUS has a brain, a voice, a heartbeat — but it still can't *see* the world around it.

"Every great robot needs eyes," the Engineer says, picking up a tiny disc with a squiggly line etched on its face. This is the photoresistor — a sensor that changes its resistance based on how much light hits it. In bright light, electricity flows easily. In darkness, it resists.

It isn't a digital signal — HIGH or LOW. It's something richer. It's *analog*.

Today, the Engineer installs NEXUS's first Optical Sensor and teaches the robot to sense light — and respond to it.

---

## THE LAW

**THE 11th LAW: THE SPECTRUM LAW**

So far, NEXUS has only known two states: ON and OFF. HIGH and LOW. 1 and 0. That's *digital* — like a regular light switch. It can only be on or it can only be off.

But the real world doesn't work that way.

Temperature isn't just "hot" or "cold" — it's 72.4 degrees. Sound isn't just "loud" or "quiet" — it's a thousand different volumes. Light isn't just "on" or "off" — it's everywhere in between.

That's *analog*. Analog signals can be any value along a range — not just two states, but an entire spectrum.

**The Light Switch vs. The Dimmer Switch:**
> A regular light switch is digital — flip it, and the light is fully ON or fully OFF. Nothing in between.
>
> A dimmer switch is analog — you can slide it to 10% brightness, 50% brightness, 87% brightness, or anywhere you want.

The Arduino reads analog signals with `analogRead(pin)`. It takes the voltage coming in (from 0V to 5V) and converts it to a number from **0** (complete darkness / 0V) to **1023** (full brightness / 5V). That's 1,024 possible values instead of just 2.

**Reading a thermometer vs. asking "is it hot?"**
> If you only asked "is it hot?" you'd get YES or NO. That's digital.
> If you read the thermometer, you get 98.6°F. That's analog.
> `analogRead()` is like reading the thermometer — it gives you the exact number, not just a guess.

Then, to *output* an analog-style signal, the Arduino uses **PWM** (Pulse Width Modulation). It can't truly output in-between voltages, so it cheats — it switches the pin ON and OFF so fast (thousands of times per second) that the LED *looks* like it's dim instead of blinking. `analogWrite(pin, 0-255)` controls how much of the time the pin is ON. 0 = always off. 255 = always on. 128 = half and half, which *looks* like half-brightness.

PWM pins on the Arduino are marked with a tilde: **~**. Pin 9 has one.

---

## BLUEPRINT

**How the photoresistor circuit works — the Voltage Divider:**

The photoresistor and the 10kΩ resistor are connected in a chain between 5V and GND. The Arduino reads the voltage at the junction between them (pin A0). As light hits the photoresistor, its resistance drops, so more voltage reaches A0. In darkness, its resistance rises, so less voltage reaches A0. This "divides" the voltage based on light level — that's why it's called a **voltage divider**.

```
  5V ──────── [Photoresistor] ──┬──── A0  (Arduino reads voltage here)
                                │
                             [10kΩ]
                                │
  GND ────────────────────────┘

  Pin 9 (~) ──── [220Ω resistor] ──── [LED +] [LED -] ──── GND
```

**Component identification:**
- Photoresistor (LDR): small disc with wavy lines. No + or - — it works either way.
- The 10kΩ resistor: Brown–Black–Orange stripes. This is the "bottom half" of the voltage divider.

---

## BUILD MISSION

**PHOTORESISTOR VOLTAGE DIVIDER (A0)**

1. Push the photoresistor into the breadboard so its two legs are in different rows.
2. Connect one leg of the photoresistor to the Arduino **5V** pin with a wire.
3. Connect the other leg of the photoresistor to the Arduino **A0** pin with a wire. (This is the "middle" of the voltage divider — where the reading happens.)
4. From that same row (the A0 row), connect one leg of the **10kΩ resistor** (Brown–Black–Orange).
5. Connect the other leg of the 10kΩ resistor to the Arduino **GND** pin.

**LED (Pin 9)**

6. Push the LED into the breadboard. The longer leg is + (anode).
7. Connect the **shorter leg** (–, cathode) to **GND** on the Arduino.
8. Connect one leg of the **220Ω resistor** (Red–Red–Brown) to the **longer leg** (+) of the LED.
9. Connect the other leg of the 220Ω resistor to **Arduino pin 9** (look for the ~ symbol next to it — that means PWM).

**Check your work:**
- [ ] Photoresistor leg 1 → 5V
- [ ] Photoresistor leg 2 → A0 AND to 10kΩ resistor
- [ ] 10kΩ resistor other leg → GND
- [ ] LED short leg → GND
- [ ] LED long leg → 220Ω → pin 9 (~)

**If your circuit doesn't work:**
- Is the LED in backwards? Flip it around.
- Is the LED connected to pin 9? It must be a PWM pin (has ~ next to it). Pins 3, 5, 6, 9, 10, 11 are PWM pins.
- Is the 10kΩ resistor connected to GND? Without it, the voltage divider doesn't work.
- Open the Serial Monitor (magnifying glass icon, top right of Arduino IDE, set to 9600 baud). What numbers is NEXUS reporting? If they're all 0 or all 1023, check the photoresistor wiring.

---

## CODE CORE

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — QUEST 11
// Eyes of the Robot: NEXUS sees light levels!
// ============================================

int lightPin = A0;  // Photoresistor connected to analog pin A0
int ledPin   = 9;   // LED connected to pin 9 (must be a PWM ~ pin)

void setup() {
  pinMode(ledPin, OUTPUT);     // LED pin is an output
  Serial.begin(9600);          // Start communication with the computer
  Serial.println("NEXUS OPTICAL SENSOR ONLINE");
}

void loop() {
  // NEXUS: "Reading light level with my optical sensor..."
  int lightLevel = analogRead(lightPin);  // Returns 0 (dark) to 1023 (bright)

  // NEXUS: "Converting light level to brightness command..."
  // map() converts the 0-1023 range to 0-255 range (what analogWrite needs)
  // map(value, fromLow, fromHigh, toLow, toHigh)
  int brightness = map(lightLevel, 0, 1023, 0, 255);

  // NEXUS: "Setting eye brightness to match surroundings..."
  analogWrite(ledPin, brightness);  // 0 = off, 255 = full brightness

  // NEXUS: "Reporting to Engineer..."
  Serial.print("Light sensor: ");
  Serial.print(lightLevel);
  Serial.print("  |  Eye brightness: ");
  Serial.println(brightness);

  delay(100);  // Wait a little before reading again (100ms = 10 times per second)
}
```

**Upload steps:**
1. Plug in the Arduino with USB.
2. Select the right board: Tools → Board → Arduino Uno.
3. Select the right port: Tools → Port → (the one with "Arduino" in the name).
4. Click the Upload button (right-pointing arrow).
5. Open **Serial Monitor** (Tools → Serial Monitor, or the magnifying glass). Set baud rate to 9600.

**What you should see:** Numbers scrolling in the Serial Monitor. Cover the photoresistor with your hand — the numbers drop. Shine a flashlight on it — numbers climb. The LED brightness should change to match.

---

## CHALLENGE MISSIONS

**Challenge 1 — Night Light Mode:**
Right now the LED gets brighter when it's bright outside. Flip it! Change this line:
```cpp
int brightness = map(lightLevel, 0, 1023, 0, 255);
```
To this:
```cpp
int brightness = map(lightLevel, 0, 1023, 255, 0);
```
Now the LED gets BRIGHTER in the dark, like a real night light. NEXUS's eye glows when it needs to see in darkness.

**Challenge 2 — Threshold Alert:**
Can you make the LED turn fully ON (not dim — full blast) when the room gets very dark, and fully OFF when it's bright? Hint: use `if (lightLevel < 300)` and `digitalWrite()` instead of `analogWrite()`. What number works best for your room?

---

## XP REWARD

```
╔══════════════════════════════════════════════════════╗
║  QUEST 11 COMPLETE                                   ║
║  +10 XP EARNED                                       ║
║  ROBOT PART UNLOCKED: *** OPTICAL SENSOR ***         ║
║                                                      ║
║  NEXUS CAN NOW SEE THE WORLD.                        ║
╚══════════════════════════════════════════════════════╝
```

**Next quests unlocked:**
- **Q12 — Robot Voice** (NEXUS learns to speak in melody)
- **SQ03 — Secret Alarm** (side quest: use NEXUS's eyes to guard a room)
