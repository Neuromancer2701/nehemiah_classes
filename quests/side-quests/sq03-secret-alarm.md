```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — SIDE QUEST 03          ║
║  Secret Alarm                         [ ] COMPLETE   ║
╚══════════════════════════════════════════════════════╝
```

> **XP Reward:** +5 XP · **Unlocked by:** Q11 — Eyes of the Robot
> **Robot Upgrade:** NEXUS becomes a guardian sentinel

---

## PARTS NEEDED

- [ ] Arduino Uno + USB cable
- [ ] Breadboard
- [ ] Photoresistor (LDR — from Q11)
- [ ] 10kΩ resistor (Brown–Black–Orange)
- [ ] Passive buzzer (or active buzzer)
- [ ] LED (optional — for a visual alarm indicator)
- [ ] 220Ω resistor (optional — for the LED)
- [ ] Jumper wires

---

## LORE

The Engineer looks around the room and has an idea.

NEXUS already has optical sensors — it can read the light level in a room. What if the Engineer used that skill as a *guard*? What if NEXUS could watch a doorway, a drawer, a shelf — and alert the Engineer the moment the light level changes?

A flashlight sweeping across the photoresistor. A light being turned on in a dark room. A hand passing over the sensor. Any of these changes the light level by more than a certain amount — the threshold.

Cross the threshold, and NEXUS sounds the alarm.

This is how real security systems work. Photoelectric sensors on doors. Motion detectors in hallways. Pressure plates under mats. They all do the same thing: compare a measurement to a threshold, and trigger an action when it's crossed.

Today, the Engineer builds a real alarm.

---

## THE LAW

**THE THRESHOLD LAW (Side Quest Edition)**

A threshold is a point of no return — a value that, once crossed, triggers a response.

**The thermostat analogy:**
> A home thermostat has one job: compare the room temperature to the temperature the homeowner set. If the room gets colder than the set temperature — the *threshold* — the thermostat triggers the heater. When it warms back up above the threshold, the heater turns off.
>
> It doesn't care what the exact temperature is. It only cares about one question: *has the threshold been crossed?*

In code, this is an `if` statement comparing a sensor reading to a fixed number:

```cpp
if (lightLevel < threshold) {
  // Threshold crossed — trigger the alarm!
} else {
  // All clear — stay silent
}
```

The key skill is choosing the right threshold — and that requires *calibration*: reading the actual sensor values in your real environment and picking a number that makes sense.

---

## BLUEPRINT

**Photoresistor voltage divider (from Q11):**

```
  5V ──── [Photoresistor] ──┬──── A0  (reads light level)
                            │
                         [10kΩ]
                            │
  GND ─────────────────────┘
```

**Passive buzzer:**

```
  Pin 8 ──── [Buzzer +]
  GND   ──── [Buzzer -]
```

**Optional LED indicator:**

```
  Pin 13 ──── [220Ω] ──── [LED +] [LED -] ──── GND
```

---

## BUILD MISSION

**STEP 1 — Build the light sensor (same as Q11)**

1. Push the photoresistor into the breadboard.
2. Connect one leg to **Arduino 5V**.
3. Connect the other leg to **Arduino A0** AND to one leg of the **10kΩ resistor**.
4. Connect the other leg of the 10kΩ resistor to **Arduino GND**.

**STEP 2 — Build the alarm buzzer**

5. Push the passive buzzer into the breadboard.
6. Connect the **+ leg** to **Arduino pin 8**.
7. Connect the **– leg** to **Arduino GND**.

**STEP 3 — Optional LED indicator**

8. Push the LED into the breadboard. Longer leg is +.
9. Connect the **short leg** (–) to **GND**.
10. Connect a **220Ω resistor** from the **long leg** (+) to **Arduino pin 13**.

**Check your work:**
- [ ] Photoresistor: one leg to 5V, other leg to A0 AND to 10kΩ
- [ ] 10kΩ resistor: from A0 node to GND
- [ ] Buzzer: pin 8 → + leg | – leg → GND
- [ ] LED (optional): pin 13 → 220Ω → LED+ | LED– → GND

**If your circuit doesn't work:**
- Read the Serial Monitor first. Is NEXUS printing light values? If not, check the photoresistor wiring from Q11.
- Is the buzzer silent when it should alarm? Try the active buzzer instead — change `tone(BUZZER, 880)` to `digitalWrite(BUZZER, HIGH)`.
- The alarm triggers constantly? The threshold is too high — lower it. The alarm never triggers? The threshold is too low — raise it.

---

## CALIBRATION — FIND YOUR THRESHOLD

Before setting the alarm, the Engineer must *calibrate* it.

**Calibration step:**
1. Upload the code below.
2. Open the **Serial Monitor** (Tools → Serial Monitor, 9600 baud).
3. Look at the numbers printing to the screen. This is your room's normal light level.
4. Note that number. Then cover the photoresistor with your hand and note how low it goes.
5. Pick a threshold number between your normal level and your covered level.

**Example calibration:**
```
Room light level:     650
Hand over sensor:     120
Good threshold:       400  (halfway — will trigger when noticeably darkened)
```

Then change `int threshold = 400;` in the code to your number.

---

## CODE CORE

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — SIDE QUEST 03
// Secret Alarm: NEXUS guards the perimeter!
// ============================================

int lightPin  = A0;   // Photoresistor on analog pin A0
int buzzerPin = 8;    // Passive buzzer on pin 8
int ledPin    = 13;   // Optional LED indicator on pin 13

// NEXUS: "Loading alarm threshold..."
// Change this number based on your calibration step above!
// Lower number = more sensitive (triggers in less darkness)
// Higher number = less sensitive (needs more darkness to trigger)
int threshold = 400;  // << CHANGE THIS after calibrating

// Track alarm state so NEXUS doesn't print the same message every loop
bool alarmActive = false;

void setup() {
  pinMode(buzzerPin, OUTPUT);
  pinMode(ledPin,    OUTPUT);

  Serial.begin(9600);
  Serial.println("╔════════════════════════════════╗");
  Serial.println("║  NEXUS GUARDIAN MODE ONLINE    ║");
  Serial.println("╚════════════════════════════════╝");
  Serial.print("Alarm threshold set to: ");
  Serial.println(threshold);
  Serial.println("Monitoring light levels...");
  Serial.println("");

  // NEXUS: "Running calibration read — showing live values..."
  Serial.println("=== CALIBRATION MODE (5 seconds) ===");
  Serial.println("Watch the numbers. Cover the sensor. Note the range.");
  long startTime = millis();
  while (millis() - startTime < 5000) {
    // Show light levels for 5 seconds before guarding
    int reading = analogRead(lightPin);
    Serial.print("Light level: ");
    Serial.println(reading);
    delay(250);
  }
  Serial.println("=== CALIBRATION DONE — GUARDING NOW ===");
  Serial.println("");
}

void loop() {
  // NEXUS: "Scanning optical sensor..."
  int lightLevel = analogRead(lightPin);

  // ---- ALARM STATE: light dropped below threshold ----
  if (lightLevel < threshold) {
    // NEXUS: "THRESHOLD CROSSED — INTRUDER ALERT!"

    if (!alarmActive) {
      // Only print the alert message once when alarm first triggers
      Serial.println("!!! ALARM TRIGGERED !!!");
      Serial.print("Light dropped to: ");
      Serial.println(lightLevel);
      alarmActive = true;
    }

    // Sound the alarm — alternating high and low tones
    tone(buzzerPin, 880, 100);  // High beep
    digitalWrite(ledPin, HIGH);
    delay(150);

    tone(buzzerPin, 440, 100);  // Low beep
    digitalWrite(ledPin, LOW);
    delay(150);

  // ---- CLEAR STATE: light is above threshold ----
  } else {
    // NEXUS: "All clear. No intrusion detected."

    if (alarmActive) {
      // Only print the all-clear message once when alarm resets
      Serial.println("All clear — alarm reset.");
      Serial.print("Light level: ");
      Serial.println(lightLevel);
      alarmActive = false;
    }

    noTone(buzzerPin);          // Make sure buzzer is off
    digitalWrite(ledPin, LOW);  // Make sure LED is off

    delay(100);  // Small delay when quiet
  }
}
```

---

## MISSION SCENARIOS

Once the alarm is built and calibrated, try these field tests:

**Mission A — The Flashlight Test:**
Set up the sensor in a normally dark room. Use a flashlight. Sweep the beam across the sensor without triggering the alarm. This is the opposite setup — the alarm triggers when light *appears* in darkness. Change the `if` condition to `if (lightLevel > threshold)` for this mode.

**Mission B — The Door Guardian:**
Place the sensor near a door gap. The alarm triggers when someone opens the door and lets in light (if the room is dark) or blocks the light (if you shine a flashlight on the sensor). Can someone sneak through without alerting NEXUS?

**Mission C — The Drawer Spy:**
Put the Arduino in a drawer with the photoresistor facing up. When the drawer opens, light floods in — NEXUS detects it and triggers. The Engineer is alerted whenever someone opens the drawer.

---

## XP REWARD

```
╔══════════════════════════════════════════════════════╗
║  SIDE QUEST 03 COMPLETE                              ║
║  +5 XP EARNED                                        ║
║  NEXUS IS NOW A GUARDIAN SENTINEL                    ║
╚══════════════════════════════════════════════════════╝
```
