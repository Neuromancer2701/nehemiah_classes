```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 13               ║
║  Feel the World                       [ ] COMPLETE   ║
╚══════════════════════════════════════════════════════╝
```

> **XP Reward:** +10 XP · **Robot Part Unlocked:** Environment Sensor

---

## PARTS NEEDED

- [ ] Arduino Uno + USB cable
- [ ] Breadboard
- [ ] LM35 temperature sensor (small black component, 3 legs, flat face on one side)
- [ ] Jumper wires

---

## LORE

The Engineer holds the LM35 up to the light. It's tiny — barely larger than a thumbnail — with three silver legs pointing downward and a flat black face. To anyone else it might look like a boring chip. But to the Engineer, it's something amazing: a component that can feel temperature and convert it into a voltage the Arduino can read.

NEXUS already has eyes. It has a voice. Now it needs to *feel* the world around it.

"With this sensor," the Engineer says quietly, "NEXUS will know if it's hot or cold. It can track the temperature of a room. It can warn us about overheating. It can monitor an environment for hours without stopping."

A doctor uses a thermometer to measure a patient's temperature. Today, the Engineer builds something better — a thermometer that reads itself and reports the results every single second.

The Environment Sensor goes online.

---

## THE LAW

**THE 13th LAW: THE CONVERSION LAW**

Sensors don't "know" temperature, pressure, or light — they just change their electrical behavior based on those things. The job of the Engineer is to *convert* that electrical behavior into real-world numbers using math.

**The doctor's thermometer analogy:**
> A glass thermometer contains liquid mercury. Heat makes the mercury expand and rise in the tube. The numbers printed on the glass convert that expansion into a temperature reading.
>
> The LM35 works the same way — except instead of mercury expanding, it outputs *voltage*. Heat it up, and the voltage at its output leg rises. The Arduino reads that voltage, and math turns it into degrees.

Here's the full conversion chain:

```
Temperature → LM35 chip → Voltage → analogRead() → Raw number → Math → Degrees °C → More math → Degrees °F
```

**The LM35's rule:** For every 1 degree Celsius, the output voltage increases by exactly **10 millivolts** (0.01 volts). This is the sensor's promise to the Engineer.

- At 0°C → output is 0.00V
- At 25°C → output is 0.25V
- At 100°C → output is 1.00V

**The math chain:**
1. `analogRead()` returns a number from 0 to 1023 (representing 0V to 5V)
2. Convert to voltage: `voltage = rawValue × (5.0 / 1023.0)`
3. Convert to Celsius: `tempC = voltage × 100.0` (because 0.01V per degree → multiply by 100)
4. Convert to Fahrenheit: `tempF = (tempC × 9.0 / 5.0) + 32.0`

Each step builds on the last. The Engineer doesn't guess — the Engineer calculates.

---

## BLUEPRINT

**IMPORTANT — Read this before wiring!**

The LM35 has three legs. The *order* of the legs matters. Getting this wrong can damage the sensor.

Hold the LM35 with the **flat face pointing toward you** and the legs pointing downward:

```
     [ FLAT FACE toward you ]

    Left leg    Middle leg    Right leg
      VCC (5V)    OUT (A0)     GND
```

**Double-check:** The flat face of the LM35 always faces the Engineer when reading the legs left to right as: VCC, OUT, GND.

> **Warning:** Some component bags label the legs differently. Always check the bag or the small print on the sensor itself. If NEXUS reports a wildly wrong temperature (like 0°C always, or over 150°C), the wiring may be backwards. Power it off immediately, check the datasheet, and rewire.

**Wiring diagram:**

```
LM35 (flat face toward you):

  Left leg  ──────────────── Arduino 5V
  Middle leg ─────────────── Arduino A0
  Right leg  ─────────────── Arduino GND
```

No resistors needed. No voltage divider. The LM35 outputs a clean voltage on its own.

---

## BUILD MISSION

1. Push the LM35 into the breadboard. Make sure each leg lands in a **different row** (not the same row — that would short the legs together).
2. Hold the LM35 with the **flat face toward you** and identify the three legs: Left (VCC), Middle (OUT), Right (GND).
3. Connect the **left leg** (VCC) to **Arduino 5V** with a wire.
4. Connect the **middle leg** (OUT) to **Arduino A0** with a wire.
5. Connect the **right leg** (GND) to **Arduino GND** with a wire.

**Check your work:**
- [ ] LM35 flat face identified (facing Engineer)
- [ ] Left leg → 5V
- [ ] Middle leg → A0
- [ ] Right leg → GND

**If your circuit doesn't work:**
- Is the sensor reading 0.0°C constantly? The OUT leg might not be connected to A0, or the sensor might be powered incorrectly.
- Is the sensor reading a number way too high (like 150°C)? The sensor might be wired backwards — power it off and check.
- Are you getting a reasonable number but it seems slightly off? That's normal — LM35 sensors are accurate to about ±1°C. That's fine.
- Make sure you're using the right Serial Monitor baud rate: **9600**.

---

## CODE CORE

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — QUEST 13
// Feel the World: NEXUS reads temperature!
// ============================================

int tempPin = A0;  // LM35 temperature sensor on analog pin A0

void setup() {
  Serial.begin(9600);    // Start talking to the computer at 9600 baud
  Serial.println("================================");
  Serial.println("  NEXUS ENVIRONMENT SENSOR ON  ");
  Serial.println("================================");
}

void loop() {
  // NEXUS: "Reading environment sensor — collecting raw voltage data..."
  int rawValue = analogRead(tempPin);  // Returns 0 to 1023

  // NEXUS: "Step 1: Converting raw reading to voltage..."
  // The Arduino's 5V supply is divided into 1024 steps (0 to 1023)
  // Each step = 5V / 1024 = about 0.00488 volts
  float voltage = rawValue * (5.0 / 1023.0);

  // NEXUS: "Step 2: Converting voltage to Celsius..."
  // LM35 outputs 10 millivolts (0.01V) per degree Celsius
  // Flip it: divide voltage by 0.01, OR multiply by 100.0
  float tempC = voltage * 100.0;

  // NEXUS: "Step 3: Converting Celsius to Fahrenheit..."
  // Formula every Engineer should know: F = (C * 9/5) + 32
  float tempF = (tempC * 9.0 / 5.0) + 32.0;

  // NEXUS: "Reporting environment data to Engineer..."
  Serial.print("Temperature: ");
  Serial.print(tempC, 1);    // Print with 1 decimal place (e.g., 23.4)
  Serial.print(" C  /  ");
  Serial.print(tempF, 1);    // Print Fahrenheit with 1 decimal place
  Serial.println(" F");

  delay(1000);  // Wait 1 full second before reading again
}
```

**What you should see in Serial Monitor:** Temperature readings updating once per second. At room temperature, expect somewhere around 20–26°C (68–78°F).

---

## CHALLENGE MISSIONS

**Challenge 1 — Touch Test:**
Open the Serial Monitor and watch the numbers. Now wrap your fingers around the LM35 sensor — hold it tight in your fist. Watch what happens to the temperature over the next 30 seconds. How warm is your hand? When you let go, how fast does it cool down?

**Challenge 2 — Cold Test:**
Put something cold (a water bottle, an ice pack, even a cold desk surface) near the sensor without touching it directly. How does the temperature in the air change? Can NEXUS detect the chill from a distance?

**Challenge 3 — Alert Light:**
Add an LED to pin 13. Add this code inside the loop:
```cpp
if (tempC > 30.0) {
  digitalWrite(13, HIGH);  // Warning! Too hot!
} else {
  digitalWrite(13, LOW);
}
```
Now NEXUS warns the Engineer when the temperature gets too warm. What threshold makes sense for your room?

---

## XP REWARD

```
╔══════════════════════════════════════════════════════╗
║  QUEST 13 COMPLETE                                   ║
║  +10 XP EARNED                                       ║
║  ROBOT PART UNLOCKED: *** ENVIRONMENT SENSOR ***     ║
║                                                      ║
║  NEXUS CAN NOW FEEL THE WORLD AROUND IT.             ║
╚══════════════════════════════════════════════════════╝
```

**Next quests unlocked:**
- **Q14 — The Living Robot** (FINAL BOSS — bring NEXUS fully online!)
- **SQ04 — Temperature Spy** (side quest: log data over time with min/max tracking)
