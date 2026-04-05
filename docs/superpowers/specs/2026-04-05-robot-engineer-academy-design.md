# Robot Engineer Academy — Curriculum Design Spec
**Date:** 2026-04-05
**Project:** nehemiah_classes
**Audience:** Nehemiah, age 9 — hands-on learner, total beginner in electronics and coding

---

## Overview

An electronics and Arduino curriculum themed as a Robot Engineer RPG. Nehemiah plays the role of a young Robot Engineer building his robot companion piece by piece. Each quest teaches a fundamental electronics or programming concept, builds a physical circuit, and rewards him with XP and robot parts. The curriculum lives in the `nehemiah_classes` repo as one Markdown file per quest, printable and usable away from the screen at the workbench.

---

## Target Learner Profile

- Age 9
- No prior electronics or coding experience
- Very hands-on — learns by building physical things
- Session style: short "theory" reads (5–10 min), longer build sessions (45–90 min)
- Motivated by RPG progression and tangible rewards

---

## Hardware

**Elegoo Super Starter Kit Uno R3** — components used across the curriculum:
- Arduino Uno R3 + USB cable
- Breadboard
- LEDs (red, green, yellow, RGB)
- Resistors (220Ω, 1kΩ, 10kΩ)
- Push buttons
- Buzzer (active and passive)
- Potentiometer
- Photoresistor (LDR)
- Temperature sensor (LM35 or thermistor)
- Jumper wires
- 9V battery + connector (Act 1 only)
- LCD display (final boss)
- Servo motor (final boss)

---

## File Structure

```
nehemiah_classes/
├── README.md                          ← Mission Control (world map + progress tracker)
├── character-sheet.md                 ← Robot companion sheet (unlocks at Level 3)
├── quests/
│   ├── q01-power-up.md
│   ├── q02-first-light.md
│   ├── q03-the-blink.md
│   ├── q04-many-lights.md
│   ├── q05-push-the-button.md
│   ├── q06-sound-off.md
│   ├── q07-meet-the-brain.md
│   ├── q08-first-words.md
│   ├── q09-talking-to-your-robot.md
│   ├── q10-listen-up.md
│   ├── q11-eyes-of-the-robot.md
│   ├── q12-robot-voice.md
│   ├── q13-feel-the-world.md
│   ├── q14-boss-the-living-robot.md
│   └── side-quests/
│       ├── sq01-rgb-rainbow.md
│       ├── sq02-morse-code.md
│       ├── sq03-secret-alarm.md
│       └── sq04-temperature-spy.md
└── docs/
    └── superpowers/specs/
        └── 2026-04-05-robot-engineer-academy-design.md
```

---

## RPG Progression System

### Approach
Mechanics start minimal and grow richer as Nehemiah levels up, mirroring his learning curve.

### XP Rewards
| Action | XP |
|---|---|
| Main Quest completed | +10 XP |
| Side Quest completed | +5 XP |
| Boss Quest completed | +25 XP |
| Build works first try (bonus) | +5 XP |

### Level Thresholds
| Level | XP Required | Title | Mechanic Unlocked |
|---|---|---|---|
| 1 | 0 | Recruit | Checkbox completion only |
| 2 | 20 | Technician | XP tracking begins |
| 3 | 40 | Engineer | `character-sheet.md` unlocks |
| 4 | 60 | Specialist | Side quest slots appear on sheet |
| 5 | 80 | Systems Expert | Robot parts inventory on sheet |
| 6 | 100 | Master Engineer | Full ASCII robot assembles on sheet |
| 7 | 130 | Robot Architect | Final boss unlocked |

### Character Sheet (unlocks at Level 3)
- Robot name (chosen by Nehemiah)
- Pencil/pen XP bar
- Parts Collected list (components used)
- Side quest lock/unlock slots
- ASCII robot body that gains parts each level

---

## Quest Map

### Act 1 — Power Up (Pure Electronics, No Arduino)
| Quest | Core Law | Build |
|---|---|---|
| Q01: Power Up | Electricity needs a complete loop | LED + battery + wire on breadboard |
| Q02: First Light | Voltage, Current, Resistance (V=IR) | LED with correct resistor |
| Q03: The Blink | Switches interrupt circuits | Button toggles LED |
| Q04: Many Lights | Series vs. parallel circuits | 3 LEDs wired both ways |
| Q05: Push the Button | Inputs vs. outputs | Button controls buzzer |
| Q06: Sound Off | Frequency makes sound | Buzzer tones with different resistors |

### Act 2 — The Brain Awakens (Arduino Intro)
| Quest | Core Law | Build |
|---|---|---|
| Q07: Meet the Brain | What a microcontroller is | Arduino tour, no wiring |
| Q08: First Words | `digitalWrite` / `delay` | Blink LED with code |
| Q09: Talking to Your Robot | Serial monitor | Print messages to screen |
| Q10: Listen Up | `digitalRead` | Button input controls LED in code |

### Act 3 — Robot Systems Online (Sensors + Advanced Output)
| Quest | Core Law | Build |
|---|---|---|
| Q11: Eyes of the Robot | Analog signals, `analogRead` | Light sensor dims/brightens LED |
| Q12: Robot Voice | PWM, `tone()` | Buzzer plays a melody |
| Q13: Feel the World | Sensor libraries | Temperature sensor reads the room |

### Final Boss
| Quest | Build |
|---|---|
| Q14: The Living Robot | Full integration: button + LED eyes + buzzer voice + sensor + servo movement + LCD display — robot companion comes alive |

### Side Quests (unlockable)
| Quest | Unlocked By | Build |
|---|---|---|
| SQ01: RGB Rainbow | Q02 | Mix colors with RGB LED |
| SQ02: Morse Code | Q08 | Blink secret messages with code |
| SQ03: Secret Alarm | Q11 | Light-triggered buzzer alarm |
| SQ04: Temperature Spy | Q13 | Log temperature to Serial Monitor |

---

## Quest File Template

Every quest file follows this exact structure (printable, no dependencies on screen):

```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST ##               ║
║  [QUEST NAME]                      [ ] COMPLETE      ║
╚══════════════════════════════════════════════════════╝

[PARTS NEEDED]        ← component checklist at top

[LORE]                ← 1 short story paragraph (2–3 min read)

[THE LAW]             ← 1 core concept, plain language + analogy

[BLUEPRINT]           ← ASCII circuit diagram

[BUILD MISSION]       ← numbered steps, one action each

[CODE CORE]           ← quests 8+ only: full sketch, every line commented

[XP REWARD]           ← XP earned, robot part unlocked, next quest/side quest
```

### Diagram Styles
1. **Simple inline** — `(+) ── LED ── Resistor ── (-)` for basic concepts
2. **Breadboard grid** — ASCII grid showing exact hole positions
3. **Component legend** — table of parts at top of each quest

---

## Tone & Writing Style

- Nehemiah is always "the Engineer" — never a student
- Electronics rules are "The Laws" — discovered, not taught
- Failures are "debugging" — part of the job, not mistakes
- Every concept uses a physical analogy first (water pipes for voltage/current, etc.)
- Code comments are written as the robot "thinking out loud"
- Encouragement is matter-of-fact: "Engineers debug. Let's find it."

---

## Success Criteria

- A 9-year-old with zero background can pick up Quest 01 and complete it independently
- Each quest is printable and usable without a screen (except Code Core quests which need the Arduino IDE)
- Diagrams are clear enough to wire from without a photo
- By Quest 14, Nehemiah has built a working multi-component Arduino project entirely from his own hands
- The RPG mechanics feel rewarding without requiring a parent to manage them
