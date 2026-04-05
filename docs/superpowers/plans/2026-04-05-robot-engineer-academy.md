# Robot Engineer Academy Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create the complete Robot Engineer Academy curriculum — 20 printable Markdown quest files teaching electronics fundamentals and Arduino programming to a 9-year-old, themed as an RPG where he builds his robot companion NEXUS piece by piece.

**Architecture:** One Markdown file per quest under `quests/`, a `README.md` Mission Control hub, and a `character-sheet.md` that unlocks at Level 3. All files follow a strict printable template (LORE / THE LAW / BLUEPRINT / BUILD MISSION / CODE CORE / XP REWARD). Act 1 (Q01–Q06) uses the Arduino as a 5V power supply only — no code. Act 2 (Q07–Q10) introduces the Arduino IDE and basic coding. Act 3 (Q11–Q13) adds sensors and analog I/O. Q14 is the final boss combining all systems (LED eyes, buzzer, photoresistor, button, servo motor).

**Tech Stack:** Markdown, Arduino C++ (quests 8+), ASCII diagrams, Elegoo Uno R3 Super Starter Kit

---

## File Map

| File | Responsibility |
|---|---|
| `README.md` | Mission Control — world map, XP table, links to all quests |
| `character-sheet.md` | Printable robot companion sheet — unlocks at Level 3 (40 XP) |
| `quests/q01-power-up.md` | Act 1: First Law — circuits need complete loops |
| `quests/q02-first-light.md` | Act 1: Ohm's Law — V=IR, resistors protect LEDs |
| `quests/q03-the-blink.md` | Act 1: Switches open/close circuits |
| `quests/q04-many-lights.md` | Act 1: Series vs parallel circuits |
| `quests/q05-push-the-button.md` | Act 1: Inputs vs outputs, button controls buzzer |
| `quests/q06-sound-off.md` | Act 1: Potentiometer as variable resistor |
| `quests/q07-meet-the-brain.md` | Act 2: Arduino tour + IDE setup |
| `quests/q08-first-words.md` | Act 2: digitalWrite/delay, LED blink |
| `quests/q09-talking-to-your-robot.md` | Act 2: Serial Monitor communication |
| `quests/q10-listen-up.md` | Act 2: digitalRead, button controls LED |
| `quests/q11-eyes-of-the-robot.md` | Act 3: analogRead, map(), analogWrite, photoresistor |
| `quests/q12-robot-voice.md` | Act 3: tone(), arrays, passive buzzer melody |
| `quests/q13-feel-the-world.md` | Act 3: LM35 temperature sensor, voltage math |
| `quests/q14-boss-the-living-robot.md` | Final Boss: full integration — all systems online |
| `quests/side-quests/sq01-rgb-rainbow.md` | Side: RGB LED color mixing |
| `quests/side-quests/sq02-morse-code.md` | Side: Functions, LED Morse code patterns |
| `quests/side-quests/sq03-secret-alarm.md` | Side: Threshold detection alarm |
| `quests/side-quests/sq04-temperature-spy.md` | Side: millis() data logging |

---

## Quest Template

Every quest file follows this exact printable structure:

```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST ##               ║
║  [QUEST NAME]                      [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

> XP Reward + Robot Part

## PARTS NEEDED       ← component checklist
## [LORE]             ← 2-3 sentence story, RPG flavor
## [THE LAW]          ← core concept + physical analogy
## [BLUEPRINT]        ← ASCII circuit + breadboard wiring steps
## [BUILD MISSION]    ← numbered steps, one action each + debug tips
## [CODE CORE]        ← quests 8+ only: full sketch, every line commented
## [XP REWARD]        ← XP, robot part, unlocks
```

---

## RPG Progression

| XP | Level | Title | Mechanic |
|---|---|---|---|
| 0 | 1 | Recruit | Checkboxes only |
| 20 | 2 | Technician | XP tracking |
| 40 | 3 | Engineer | character-sheet.md unlocks |
| 60 | 4 | Specialist | Side quest slots |
| 80 | 5 | Systems Expert | Robot parts inventory |
| 100 | 6 | Master Engineer | Full robot assembles |
| 130 | 7 | Robot Architect | Final Boss unlocks |

---

## Tasks

### Task 1: Infrastructure Files

**Files:**
- Create: `README.md`
- Create: `character-sheet.md`

- [ ] Write `README.md` — Mission Control hub with quest map, XP table, component list, getting started guide
- [ ] Write `character-sheet.md` — printable robot companion sheet with XP bar (10 boxes × 13 = 130 XP), ASCII robot body, parts checklist, side quest slots
- [ ] Verify both files have no placeholder text
- [ ] `git add README.md character-sheet.md && git commit -m "feat: add Mission Control and character sheet"`

---

### Task 2: Act 1 Quests (Q01–Q06) — Pure Electronics, No Code

**Files:** `quests/q01-power-up.md` through `quests/q06-sound-off.md`

**Power source note:** In all Act 1 quests, the Arduino is connected via USB and used as a 5V power source only. No code is uploaded.

- [ ] Write `q01-power-up.md` — basic circuit loop, LED + 220Ω resistor, First Law
- [ ] Write `q02-first-light.md` — Ohm's Law, swap 220Ω/1kΩ/10kΩ, resistor color code chart
- [ ] Write `q03-the-blink.md` — push button in series with LED, switch law
- [ ] Write `q04-many-lights.md` — 2 LEDs in series vs parallel, observe brightness difference
- [ ] Write `q05-push-the-button.md` — button controls active buzzer, inputs vs outputs
- [ ] Write `q06-sound-off.md` — potentiometer as variable resistor dims LED, analog control concept
- [ ] Verify each quest has: header box, PARTS NEEDED, LORE, THE LAW, BLUEPRINT, BUILD MISSION, XP REWARD
- [ ] `git add quests/q0{1..6}*.md && git commit -m "feat: add Act 1 quests Q01-Q06"`

---

### Task 3: Act 2 Quests (Q07–Q10) — Arduino Introduction

**Files:** `quests/q07-meet-the-brain.md` through `quests/q10-listen-up.md`

- [ ] Write `q07-meet-the-brain.md` — Arduino Uno labeled diagram, Arduino IDE install steps, no wiring
- [ ] Write `q08-first-words.md` — LED blink sketch, `setup()`/`loop()`/`digitalWrite()`/`delay()` explained
- [ ] Write `q09-talking-to-your-robot.md` — Serial Monitor, `Serial.begin()`/`Serial.println()`
- [ ] Write `q10-listen-up.md` — button on pin 2 controls LED, `digitalRead()`/`INPUT_PULLUP`/`if` statements
- [ ] Verify CODE CORE section in each quest: complete sketch, every line commented, comments sound like NEXUS narrating
- [ ] `git add quests/q{07..10}*.md && git commit -m "feat: add Act 2 quests Q07-Q10"`

---

### Task 4: Act 3 Quests (Q11–Q13) — Sensors and Analog

**Files:** `quests/q11-eyes-of-the-robot.md` through `quests/q13-feel-the-world.md`

- [ ] Write `q11-eyes-of-the-robot.md` — photoresistor voltage divider, `analogRead()`/`map()`/`analogWrite()`
- [ ] Write `q12-robot-voice.md` — passive buzzer, `tone()`/`noTone()`, arrays, Ode to Joy melody
- [ ] Write `q13-feel-the-world.md` — LM35 sensor, voltage-to-temperature math, `float` variables
- [ ] Verify circuit diagrams: Q11 voltage divider formula shown, Q13 LM35 pin order clearly labeled
- [ ] `git add quests/q1{1..3}*.md && git commit -m "feat: add Act 3 quests Q11-Q13"`

---

### Task 5: Final Boss (Q14)

**File:** `quests/q14-boss-the-living-robot.md`

**Components:** LED eyes (pins 7, 8), passive buzzer (pin 6), button (pin 2, INPUT_PULLUP), photoresistor (A0 with 10kΩ divider), servo (pin 9)

**NEXUS Behaviors:**
1. Boot sequence: 4-note melody + eye flash × 3 + servo sweep + Serial boot log
2. Dark mode (light < 300): both eyes steady ON
3. Alert mode (button pressed): eyes alternate + alarm tones + servo waves
4. Normal mode: slow eye blink

- [ ] Write `q14-boss-the-living-robot.md` — epic lore, full wiring diagram for all 6 components, complete integration sketch with `#include <Servo.h>`, boot sequence function, three behavior modes
- [ ] Verify: `bootSequence()` function defined before `loop()`, servo library included, all pin constants defined at top
- [ ] Include "NEXUS IS ALIVE" celebration section at the end
- [ ] `git add quests/q14-boss-the-living-robot.md && git commit -m "feat: add Final Boss quest Q14"`

---

### Task 6: Side Quests (SQ01–SQ04)

**Files:** `quests/side-quests/sq0{1..4}*.md`

- [ ] Write `sq01-rgb-rainbow.md` — RGB LED, 3 PWM pins, `analogWrite()` color mixing, color recipe table
- [ ] Write `sq02-morse-code.md` — `dot()`/`dash()` functions, full Morse alphabet chart, spell NEXUS
- [ ] Write `sq03-secret-alarm.md` — light threshold detection, calibration step via Serial Monitor
- [ ] Write `sq04-temperature-spy.md` — `millis()` non-blocking timing, MIN/MAX tracker, formatted Serial table
- [ ] `git add quests/side-quests/ && git commit -m "feat: add side quests SQ01-SQ04"`

---

### Task 7: Final Push

- [ ] `git log --oneline -10` — verify all commits present
- [ ] `git push origin main`
- [ ] Confirm all 20 quest files exist under `quests/`
