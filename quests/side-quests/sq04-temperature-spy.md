```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — SIDE QUEST 04          ║
║  Temperature Spy                      [ ] COMPLETE   ║
╚══════════════════════════════════════════════════════╝
```

> **XP Reward:** +5 XP · **Unlocked by:** Q13 — Feel the World
> **Robot Upgrade:** NEXUS becomes a data logger

---

## PARTS NEEDED

- [ ] Arduino Uno + USB cable
- [ ] Breadboard
- [ ] LM35 temperature sensor (from Q13)
- [ ] Jumper wires

---

## LORE

The Engineer thinks about all the things NEXUS could track over time.

Not just the temperature *right now* — but the temperature over the last hour. The minimum it hit all night. The maximum it reached when the sun came through the window. A complete record.

Real scientists and engineers call this **data logging** — collecting measurements automatically over time and saving them for analysis. Weather stations do it. Satellites do it. Medical monitors do it. The tiny box in a car that records what happens before a crash does it.

NEXUS can do it too.

The trick is time. `delay()` is simple, but it *freezes* the whole program while it waits. A better approach uses `millis()` — the Arduino's built-in clock that counts every millisecond since power-on. The Engineer can check the clock, decide if enough time has passed, and only then take a reading — without ever pausing the whole program.

That's how professional systems work. And today, the Engineer builds one.

---

## THE LAW

**THE TIMING LAW (Side Quest Edition)**

`delay(1000)` pauses everything for 1 second. The whole program freezes. No buttons can be checked. No sensors can read. Nothing moves. It's like putting the Arduino in a coma.

`millis()` is different. It's a clock that runs in the background all the time, from the moment the Arduino powers on. It returns the number of milliseconds that have passed. The program never pauses — it just checks the clock and decides what to do.

**The kitchen timer analogy:**
> Imagine you're cooking pasta and also waiting for garlic bread. If you stand at the oven and stare at it for 10 minutes (that's `delay()`), you can't do anything else. You can't stir the pasta. You can't answer the door.
>
> But if you glance at a clock every few seconds (`millis()`), you can do many things at once. You stir the pasta. You check the bread. You answer the door. Every time you glance at the clock, you check: "Has 10 minutes passed yet?" If yes, take out the bread. If not, keep going.
>
> `millis()` is the clock. The `if` statement is the glance.

```cpp
unsigned long lastTime = 0;     // When did we last log?
unsigned long interval = 5000;  // 5000ms = 5 seconds

void loop() {
  unsigned long now = millis();         // Check the clock

  if (now - lastTime >= interval) {    // Has 5 seconds passed?
    lastTime = now;                    // Reset the timer
    // Take a reading here!
  }
  // Everything else runs normally between readings
}
```

`unsigned long` is a type of number that can count very high — up to about 49 days of milliseconds. `long` means it's a big number. `unsigned` means it's always positive (time doesn't go backwards).

---

## BLUEPRINT

Same circuit as Q13 — no changes needed:

```
LM35 (flat face toward you):

  Left leg  ──────────────── Arduino 5V
  Middle leg ─────────────── Arduino A0
  Right leg  ─────────────── Arduino GND
```

**Reminder:** Left leg = VCC, Middle leg = OUT, Right leg = GND. Flat face toward the Engineer.

---

## BUILD MISSION

Same wiring as Quest 13. If you already have it set up from that quest, you can plug it in as-is.

1. Push the LM35 into the breadboard — each leg in its own row.
2. Flat face of the LM35 toward you: Left leg → **5V**, Middle leg → **A0**, Right leg → **GND**.

**Check your work:**
- [ ] LM35 left leg → 5V
- [ ] LM35 middle leg → A0
- [ ] LM35 right leg → GND

---

## CODE CORE

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — SIDE QUEST 04
// Temperature Spy: NEXUS logs data over time!
// ============================================

int tempPin = A0;  // LM35 temperature sensor on analog pin A0

// NEXUS: "Setting up data logging timer..."
unsigned long lastLogTime = 0;       // Timestamp of the last log entry
unsigned long logInterval = 5000;    // Log every 5000ms = every 5 seconds

// NEXUS: "Setting up min/max trackers..."
// Start min very high and max very low — first real reading will replace them
float minTempC =  999.0;   // Will be replaced by the first real reading
float maxTempC = -999.0;   // Will be replaced by the first real reading
int   logCount = 0;        // Count how many readings have been logged

// ============ HELPER FUNCTION: Read temperature ============
// NEXUS: "Temperature reading function ready..."
float readTempC() {
  int rawValue = analogRead(tempPin);          // Raw 0-1023
  float voltage = rawValue * (5.0 / 1023.0);  // Convert to voltage
  float tempC   = voltage * 100.0;            // Convert to Celsius (LM35: 10mV/°C)
  return tempC;
}

void setup() {
  Serial.begin(9600);

  // NEXUS: "Printing data log header..."
  Serial.println("╔══════════════════════════════════════════════════════╗");
  Serial.println("║         NEXUS TEMPERATURE SPY — DATA LOG            ║");
  Serial.println("╚══════════════════════════════════════════════════════╝");
  Serial.println("");
  Serial.println("Logging every 5 seconds. Touch the sensor, breathe on");
  Serial.println("it, or hold something cold near it. Watch the log!");
  Serial.println("");

  // Print column headers for the data table
  Serial.println("Entry | Time (sec) | Temp C  | Temp F  | Status");
  Serial.println("------+------------+---------+---------+-------------");
}

void loop() {
  // NEXUS: "Checking the clock..."
  unsigned long now = millis();  // How many milliseconds since power-on?

  // NEXUS: "Has enough time passed to log another entry?"
  if (now - lastLogTime >= logInterval) {
    lastLogTime = now;   // Reset the timer to right now
    logCount++;          // Count this entry

    // NEXUS: "Taking temperature reading..."
    float tempC = readTempC();
    float tempF = (tempC * 9.0 / 5.0) + 32.0;  // Convert to Fahrenheit

    // NEXUS: "Updating min and max records..."
    if (tempC < minTempC) {
      minTempC = tempC;  // New coldest reading!
    }
    if (tempC > maxTempC) {
      maxTempC = tempC;  // New hottest reading!
    }

    // NEXUS: "Determining temperature status label..."
    String status;
    if      (tempC < 15.0) status = "COLD";
    else if (tempC < 20.0) status = "Cool";
    else if (tempC < 25.0) status = "Comfortable";
    else if (tempC < 30.0) status = "Warm";
    else                   status = "HOT!";

    // NEXUS: "Writing log entry to Engineer's Serial Monitor..."
    // Format: entry number, timestamp in seconds, Celsius, Fahrenheit, status
    if (logCount < 10) Serial.print(" ");   // Pad single-digit entry numbers
    Serial.print(logCount);
    Serial.print("     | ");

    // Convert milliseconds to seconds for easier reading
    float seconds = now / 1000.0;
    if (seconds < 100.0) Serial.print(" ");  // Padding for alignment
    Serial.print(seconds, 1);
    Serial.print("       | ");

    Serial.print(tempC, 1);
    Serial.print(" C  | ");

    Serial.print(tempF, 1);
    Serial.print(" F  | ");

    Serial.println(status);
  }

  // NEXUS: "Printing updated min/max summary every 10 entries..."
  if (logCount > 0 && logCount % 10 == 0) {
    // Print a summary line every 10 entries
    // But only once — use a flag variable to avoid repeating
    // (This version keeps it simple — the summary prints and then loop continues)
  }
}

// ============ BONUS: Press Ctrl+Shift+M in Serial Monitor to copy the log ============
// The whole table can be pasted into a spreadsheet to make a graph!
```

**BONUS — Min/Max Summary Version:**

After running the basic version, here's extra code to add a summary. Add this function before `loop()`:

```cpp
// NEXUS: "Min/Max summary function..."
void printSummary() {
  Serial.println("");
  Serial.println("╔════════════════════════════════╗");
  Serial.println("║     SESSION SUMMARY            ║");
  Serial.print  ("║  Readings logged:  ");
  if (logCount < 10) Serial.print(" ");
  Serial.print(logCount);
  Serial.println("           ║");
  Serial.print  ("║  Coldest reading: ");
  Serial.print(minTempC, 1); Serial.print(" C");
  Serial.println("         ║");
  Serial.print  ("║  Hottest reading: ");
  Serial.print(maxTempC, 1); Serial.print(" C");
  Serial.println("         ║");
  Serial.println("╚════════════════════════════════╝");
}
```

Then add this at the end of the `if (now - lastLogTime >= logInterval)` block, after logging the entry:

```cpp
// Print summary every 10 entries
if (logCount % 10 == 0) {
  printSummary();
}
```

---

## CHALLENGE MISSIONS

**Challenge 1 — The 5-Minute Experiment:**
Run the Temperature Spy for at least 5 minutes without touching anything. Then:
- Touch the sensor firmly with two fingers. How fast does the temperature rise?
- Let go. How long does it take to cool back down to room temperature?
- Breathe on the sensor from close range. Does your breath register?

**Challenge 2 — Cold vs. Warm:**
Hold something cold (ice pack, cold water bottle) close to — but not touching — the sensor. Does the air temperature drop? How close does it need to be before NEXUS detects the change?

**Challenge 3 — Change the Interval:**
Change `logInterval = 5000` to `logInterval = 1000` for readings every second, or `logInterval = 60000` for readings every minute. What's the right interval for watching a temperature change slowly over time?

**Challenge 4 — The Spreadsheet:**
Copy the table from Serial Monitor (highlight all the text, Ctrl+C). Paste it into a spreadsheet program and make a line graph of temperature over time. Engineers call this a **time series graph**. You just made one.

---

## XP REWARD

```
╔══════════════════════════════════════════════════════╗
║  SIDE QUEST 04 COMPLETE                              ║
║  +5 XP EARNED                                        ║
║  NEXUS CAN NOW LOG DATA OVER TIME                    ║
║  MIN/MAX TRACKING SYSTEM: ONLINE                     ║
╚══════════════════════════════════════════════════════╝
```
