```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — SIDE QUEST 01          ║
║  RGB Rainbow                          [ ] COMPLETE   ║
╚══════════════════════════════════════════════════════╝
```

> **XP Reward:** +5 XP · **Unlocked by:** Q02 — First Light
> **Robot Upgrade:** NEXUS gets a full-color status light

---

## PARTS NEEDED

- [ ] Arduino Uno + USB cable
- [ ] Breadboard
- [ ] RGB LED (4 legs — longer leg is the common ground)
- [ ] 3x 220Ω resistors (Red–Red–Brown) — one for each color channel
- [ ] Jumper wires

---

## LORE

The Engineer stares at the parts bin and spots something unusual: an LED with *four legs* instead of two. Most LEDs are simple — on or off, one color. But this one is different. This is an **RGB LED**.

Inside this tiny component live three separate LEDs: one red, one green, one blue — all sharing a single package. By mixing how bright each one shines, the Engineer can make almost any color imaginable.

"Every color you've ever seen on a screen," the Engineer says, "was made the same way. Red, green, and blue mixed in different amounts. Phones, TVs, monitors — they all use this trick."

Time to give NEXUS a full-color status indicator.

---

## THE LAW

**THE MIXING LAW (Side Quest Edition)**

Light mixing is different from paint mixing. With paint, mixing all the colors together makes brown mud. With *light*, mixing all the colors together makes **white**.

This is called **additive color mixing** — you're adding light together. Red + Green + Blue at full brightness = White. Turn them all off = Black (no light).

**The TV screen analogy:**
> Every pixel on a TV screen is actually three tiny dots: one red, one green, one blue. To make yellow, the TV turns the red and green dots all the way up and leaves the blue dot off. To make purple, it mixes red and blue. To make white, all three dots glow at full brightness.
>
> Your RGB LED is one pixel. You're the TV.

`analogWrite(pin, 0-255)` controls each channel from 0 (off) to 255 (full brightness). Mix the three channels to paint with light.

---

## BLUEPRINT

**Identifying the RGB LED legs:**

Hold the RGB LED so the **longest leg is second from the left**. The longest leg is the **common cathode** — it connects to GND.

```
  Left to right:
  Leg 1 (R) — Red channel
  Leg 2     — Longest! This is GND (common cathode)
  Leg 3 (G) — Green channel
  Leg 4 (B) — Blue channel
```

> If your LED has a flat edge on one side, that flat edge is usually nearest to the Red leg.

**Wiring diagram:**

```
  Arduino pin 11 (~) ──── [220Ω] ──── Leg 1 (RED)
  Arduino GND        ──────────────── Leg 2 (GND — longest leg)
  Arduino pin 10 (~) ──── [220Ω] ──── Leg 3 (GREEN)
  Arduino pin 9  (~) ──── [220Ω] ──── Leg 4 (BLUE)
```

All three color pins must be **PWM pins** (marked with ~) to use `analogWrite()`. Pins 9, 10, and 11 all have PWM.

---

## BUILD MISSION

1. Push the RGB LED into the breadboard. Count the legs — there should be 4. The longest leg is GND.
2. Connect **Leg 2** (longest, GND) to **Arduino GND**.
3. Connect a 220Ω resistor from **Leg 1** (Red) to **Arduino pin 11**.
4. Connect a 220Ω resistor from **Leg 3** (Green) to **Arduino pin 10**.
5. Connect a 220Ω resistor from **Leg 4** (Blue) to **Arduino pin 9**.

**Check your work:**
- [ ] Longest leg (GND) → Arduino GND
- [ ] Red leg → 220Ω → pin 11
- [ ] Green leg → 220Ω → pin 10
- [ ] Blue leg → 220Ω → pin 9

**If your circuit doesn't work:**
- Is the LED showing only one color? One or two channel connections might be loose.
- Is the LED not lighting at all? Check that the GND leg (longest) is properly grounded.
- Getting unexpected colors? The leg order might be different on your specific RGB LED — try swapping the R and B connections.

---

## COLOR RECIPE TABLE

The Engineer's color mixing reference. Print this and keep it at the workbench.

| Color      | Red (pin 11) | Green (pin 10) | Blue (pin 9) |
|------------|:------------:|:--------------:|:------------:|
| Red        | 255          | 0              | 0            |
| Orange     | 255          | 128            | 0            |
| Yellow     | 255          | 255            | 0            |
| Lime Green | 128          | 255            | 0            |
| Green      | 0            | 255            | 0            |
| Cyan       | 0            | 255            | 255          |
| Sky Blue   | 0            | 128            | 255          |
| Blue       | 0            | 0              | 255          |
| Purple     | 128          | 0              | 255          |
| Pink       | 255          | 0              | 128          |
| White      | 255          | 255            | 255          |
| Off        | 0            | 0              | 0            |

---

## CODE CORE

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — SIDE QUEST 01
// RGB Rainbow: NEXUS cycles through all colors!
// ============================================

// Pin assignments for each color channel (all must be PWM ~ pins)
int redPin   = 11;  // Red channel on pin 11
int greenPin = 10;  // Green channel on pin 10
int bluePin  = 9;   // Blue channel on pin 9

// NEXUS: "Creating a helper function to set my status light color..."
// This function takes R, G, B values (0-255 each) and applies them
void setColor(int r, int g, int b) {
  analogWrite(redPin,   r);  // Set red brightness
  analogWrite(greenPin, g);  // Set green brightness
  analogWrite(bluePin,  b);  // Set blue brightness
}

void setup() {
  pinMode(redPin,   OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin,  OUTPUT);

  Serial.begin(9600);
  Serial.println("NEXUS STATUS LIGHT ONLINE");
  Serial.println("Initiating color test sequence...");
}

void loop() {
  // NEXUS: "Testing individual color channels..."
  Serial.println("RED");
  setColor(255, 0, 0);    // Full red, no green, no blue
  delay(1000);

  Serial.println("GREEN");
  setColor(0, 255, 0);    // No red, full green, no blue
  delay(1000);

  Serial.println("BLUE");
  setColor(0, 0, 255);    // No red, no green, full blue
  delay(1000);

  // NEXUS: "Testing color mixing — combining channels..."
  Serial.println("YELLOW (red + green)");
  setColor(255, 255, 0);
  delay(1000);

  Serial.println("CYAN (green + blue)");
  setColor(0, 255, 255);
  delay(1000);

  Serial.println("PURPLE (red + blue)");
  setColor(128, 0, 255);
  delay(1000);

  Serial.println("ORANGE (red + a little green)");
  setColor(255, 128, 0);
  delay(1000);

  Serial.println("WHITE (all channels on)");
  setColor(255, 255, 255);
  delay(1000);

  // NEXUS: "Now running smooth rainbow fade..."
  Serial.println("Rainbow fade starting...");

  // Smooth fade: Red → Yellow → Green → Cyan → Blue → Purple → Red
  // Each step changes one channel while keeping others stable

  // Red to Yellow: increase green while red stays full
  for (int g = 0; g <= 255; g++) {
    setColor(255, g, 0);
    delay(5);
  }

  // Yellow to Green: decrease red while green stays full
  for (int r = 255; r >= 0; r--) {
    setColor(r, 255, 0);
    delay(5);
  }

  // Green to Cyan: increase blue while green stays full
  for (int b = 0; b <= 255; b++) {
    setColor(0, 255, b);
    delay(5);
  }

  // Cyan to Blue: decrease green while blue stays full
  for (int g = 255; g >= 0; g--) {
    setColor(0, g, 255);
    delay(5);
  }

  // Blue to Purple: increase red while blue stays full
  for (int r = 0; r <= 255; r++) {
    setColor(r, 0, 255);
    delay(5);
  }

  // Purple to Red: decrease blue while red stays full
  for (int b = 255; b >= 0; b--) {
    setColor(255, 0, b);
    delay(5);
  }

  // NEXUS: "Rainbow cycle complete. Starting again..."
  Serial.println("Rainbow cycle complete.");
}
```

---

## CHALLENGE MISSIONS

**Challenge 1 — Custom Status Colors:**
Make NEXUS use the RGB LED as a real status indicator. For example:
- Green = everything OK
- Yellow = standby/warning
- Red = alert/problem

Can you wire it up so a button press cycles through the three status states?

**Challenge 2 — Sunrise Simulator:**
Write a loop that starts with the LED at dark red (5, 0, 0) and slowly brightens to full orange (255, 128, 0) over 10 seconds. That's what a sunrise looks like — very slowly brightening from near-dark to warm orange.

**Challenge 3 — Color by Name:**
Can you write a `for` loop that reads through the color recipe table above and shows each color for 2 seconds, printing the color name to Serial Monitor each time?

---

## XP REWARD

```
╔══════════════════════════════════════════════════════╗
║  SIDE QUEST 01 COMPLETE                              ║
║  +5 XP EARNED                                        ║
║  NEXUS STATUS LIGHT: FULL COLOR UNLOCKED             ║
╚══════════════════════════════════════════════════════╝
```
