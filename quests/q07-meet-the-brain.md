╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 07               ║
║  MEET THE BRAIN                    [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> **XP Reward:** +10 XP · **Robot Part:** Brain Module

---

## PARTS NEEDED

- [ ] Arduino Uno R3 board
- [ ] USB cable (USB-A to USB-B — the one that came with your kit)
- [ ] This quest sheet
- [ ] A pencil to check off parts as you find them

*No wiring. No code. This quest is pure exploration.*

---

## [LORE]

The transmission crackled through the static. A message, encoded in pulses of light, arrived at the Engineer's workbench:

*"NEXUS construction initiated. Unit designation: NEXUS-01. Priority component required: Brain Module. Without the Brain Module, NEXUS cannot think, cannot act, cannot become. The Brain Module is the beginning of everything."*

The Engineer picked up a small blue board covered in pins and chips and a single black rectangle at the center. It felt light — almost too light for something so powerful. But inside that black rectangle, electricity was already waiting to think.

This is the Arduino Uno R3. This is NEXUS's brain.

Before the Engineer can give NEXUS instructions, the Engineer must understand every part of the brain — what it is, what it does, and how it connects to the world. No robot is built without first understanding its own mind.

Study this board. Know it completely. Then NEXUS can begin.

---

## [THE LAW]

**THE 7TH LAW: THE BRAIN FOLLOWS THE RECIPE**

A microcontroller is a tiny computer that follows instructions one line at a time, over and over, incredibly fast — 16 million times per second on the Arduino Uno.

**Analogy:** Imagine a recipe card for making a sandwich. A chef reads the recipe line by line, in order: "Get two slices of bread. Add peanut butter. Add jelly. Put the slices together." When the recipe is done, the chef starts over from the very top — forever, if told to.

The Arduino is that chef. Your code is the recipe card. The Arduino reads it line by line, in exact order, without skipping anything. If the recipe says "wait 1 second," the Arduino waits exactly 1 second — not 0.9 seconds, not 1.1 seconds. Exactly 1.

This is what makes the Arduino so useful: it does exactly what you tell it, every single time, without getting tired or distracted. But it also means if you make a mistake in the recipe, the Arduino will follow the mistake perfectly. That is why the Engineer must write instructions carefully.

---

## [BLUEPRINT]

### THE ARDUINO UNO R3 — LABELED DIAGRAM

```
                    ┌─────────────────────────────────────────┐
                    │              ARDUINO UNO R3              │
                    │                                          │
  DIGITAL PINS ──▶  │  [13][12][11][10][ 9][ 8]              │
  (0 to 13)         │  [ 7][ 6][ 5][ 4][ 3][ 2][TX][RX]     │
                    │   ~       ~  ~       ~   ~  ~            │
                    │  (~ = PWM pins)                          │
                    │                                          │
                    │  [RST]        ┌──────────┐              │
                    │  Reset        │ATmega328P│  ◀── THE BRAIN│
                    │  Button       │  (black  │               │
                    │               │rectangle)│               │
                    │               └──────────┘               │
                    │                                          │
                    │  [PWR LED]  [TX LED]  [RX LED]          │
                    │  (green,    (blinks   (blinks            │
                    │  always on) sending)  receiving)         │
                    │                              [PIN 13 LED]│
                    │                              (built-in   │
                    │                               test LED)  │
                    │                                          │
  POWER PINS ───▶   │  [3.3V][5V][GND][GND][VIN]            │
                    │                                          │
  ANALOG PINS ───▶  │  [A0][A1][A2][A3][A4][A5]             │
                    │                                          │
  USB PORT ──────▶  │  [===USB===]      [DC POWER JACK]      │
                    └─────────────────────────────────────────┘
```

---

### EVERY PART — WHAT IT IS AND WHAT IT DOES

Find each part on your actual Arduino board and check it off.

---

**[ ] USB PORT**
The rectangular silver port at the bottom edge of the board.
- Connects to your computer with the USB cable
- Does two things at once: powers the Arduino AND sends code from the computer to the brain
- When you upload a program, data travels through this port

---

**[ ] ATmega328P MICROCONTROLLER CHIP**
The large black rectangle near the center of the board.
- This is THE BRAIN — the most important chip on the board
- Contains the processor, memory, and everything needed to run your code
- Runs at 16 MHz — 16 million clock ticks per second
- Every instruction in your code happens inside this chip

> **FUN FACT:** The ATmega328P can execute 16 million instructions per second. If YOU did one math problem every second, it would take you 185 days — non-stop, no sleeping — to do what the Arduino does in a single second.

---

**[ ] DIGITAL PINS 0 through 13**
The row of numbered pins along the top edge of the board.
- Each pin can be set as INPUT (reading electricity coming in) or OUTPUT (sending electricity out)
- Each pin is either HIGH (electricity flowing, about 5 volts) or LOW (no electricity, 0 volts)
- Pin 0 and Pin 1 are special — they handle communication (TX/RX), so avoid them for now
- Pin 13 has a built-in LED on the board, great for testing

---

**[ ] PWM PINS (marked with ~ tilde symbol)**
Pins: 3, 5, 6, 9, 10, 11 — look for the ~ symbol printed next to them.
- PWM stands for Pulse Width Modulation
- Regular digital pins are only fully ON or fully OFF
- PWM pins can fake an in-between signal by turning on and off very rapidly
- This lets you dim an LED, control motor speed, and more
- You will use these in later quests

---

**[ ] ANALOG PINS A0 through A5**
The row of pins along the bottom-left edge, labeled A0, A1, A2, A3, A4, A5.
- Unlike digital pins (only HIGH or LOW), analog pins can read a whole range of values
- They return a number from 0 to 1023, representing how much voltage is coming in
- Used with sensors — like a light sensor or a potentiometer (a knob)
- You will use A0 in a future quest with a sensor

---

**[ ] POWER PINS**
The group of pins labeled: 3.3V, 5V, GND, GND, VIN — on the bottom-left area.
- **5V** — sends out 5 volts of electricity. Used to power components.
- **3.3V** — sends out 3.3 volts. Some components need less power.
- **GND** — Ground. The return path for electricity. Every circuit needs a ground connection to work. (There are two GND pins — they are both the same ground.)
- **VIN** — Voltage In. Lets you power the Arduino from a battery or power supply instead of USB.

---

**[ ] RESET BUTTON**
The small button near the top-left of the board.
- Pressing it restarts the Arduino's program from the very beginning
- It does NOT erase your code — it just starts the recipe over from line 1
- Useful when you want to restart without unplugging

---

**[ ] TX LED and RX LED**
Two small LEDs near the digital pins, labeled TX and RX.
- **TX** = Transmit — blinks when the Arduino is SENDING data to the computer
- **RX** = Receive — blinks when the Arduino is RECEIVING data from the computer
- You will see these blink when you upload code, and again later when you use the Serial Monitor

---

**[ ] POWER LED**
The green LED near the power pins.
- Always ON when the Arduino is receiving power
- If this LED is off, the Arduino is not getting electricity
- First thing to check if something is wrong: is the power LED on?

---

**[ ] PIN 13 LED**
A small LED on the board itself, usually near pin 13.
- This LED is physically wired to digital pin 13
- When you set pin 13 to HIGH in your code, this LED turns on
- Great for testing — you do not need any extra wires to use it
- In Quest 08, you will make this LED blink with your first program

---

## [BUILD MISSION]

No wiring today. No code today.

**Your mission:** Explore your Arduino board. Find each part labeled in the diagram above. Check off each one as you find it.

Work through the list in order:

- [ ] Found the USB Port
- [ ] Found the ATmega328P chip (the large black rectangle)
- [ ] Found digital pin 13 (top row, far left)
- [ ] Found digital pin 0 (top row, far right)
- [ ] Found the PWM pins — located the ~ symbol on pins 3, 5, 6, 9, 10, 11
- [ ] Found the analog pins A0 through A5 (bottom-left row)
- [ ] Found the 5V power pin
- [ ] Found the GND pin
- [ ] Found the Reset button
- [ ] Found the TX LED
- [ ] Found the RX LED
- [ ] Found the green Power LED
- [ ] Found the pin 13 built-in LED

When every box is checked: the Engineer has fully mapped the brain of NEXUS.

**There is nothing to break. There is nothing to wire. Just look, find, and understand.**

---

## [CODE CORE]

No code this quest. The Engineer is learning the hardware first.

But here is a preview of what code will look like in Quest 08:

```cpp
// This is what a comment looks like — the Arduino ignores this line
// Comments are notes for the Engineer (and for NEXUS to "think out loud")

void setup() {
  // This runs once at the start
}

void loop() {
  // This runs over and over, forever
}
```

The `//` symbol means "this is a note, not an instruction." The Arduino skips it completely. Notes are for humans — and for NEXUS.

---

## BEFORE NEXT QUEST — INSTALL THE ARDUINO IDE

The Arduino IDE is the software on your computer where you will write code and send it to the Arduino board. Without it, you cannot give NEXUS any instructions.

**Ask a parent to help with these steps.**

1. [ ] Open a web browser and go to: **arduino.cc/en/software**
2. [ ] Download the Arduino IDE for your computer (Windows, Mac, or Linux)
3. [ ] Install it by running the downloaded file and following the on-screen steps
4. [ ] Plug your Arduino into the computer using the USB cable
5. [ ] Open the Arduino IDE
6. [ ] Go to the menu: **Tools → Board → Arduino AVR Boards → Arduino Uno**
7. [ ] Go to the menu: **Tools → Port → select the port that has "Arduino" in the name**
     - On Windows it might say something like COM3 or COM4
     - On Mac it might say something like /dev/cu.usbmodem...
     - If you see more than one, try the one with "Arduino" in the name
8. [ ] You are ready to write code!

**How to know it worked:** When you open the Arduino IDE, you should see a white text area where you can type. At the top of the screen, the board name "Arduino Uno" should appear. If you see that — setup is complete.

If something goes wrong during setup, that is completely normal. It is a debugging step. Ask a parent to help check each step again — one at a time.

---

## [XP REWARD]

**+10 XP earned!**

**Robot Part Unlocked:** Brain Module

*NEXUS status: Brain Module installed. The Engineer has mapped every circuit and pin. NEXUS knows its own mind. Now it is time to give NEXUS its first instructions.*

**Next Quest:** Q08 — First Words
