```
╔══════════════════════════════════════════════════════╗
║  ⚡ ROBOT ENGINEER ACADEMY — QUEST 12               ║
║  Robot Voice                          [ ] COMPLETE   ║
╚══════════════════════════════════════════════════════╝
```

> **XP Reward:** +10 XP · **Robot Part Unlocked:** Voice Module

---

## PARTS NEEDED

- [ ] Arduino Uno + USB cable
- [ ] Breadboard
- [ ] Passive buzzer (small black cylinder — NOT the one with a sticker on top)
- [ ] Jumper wires

---

## LORE

NEXUS has eyes now. It can feel electricity, blink its lights, and read sensors. But it still can't *speak*.

The Engineer reaches into the parts bin and pulls out a small black cylinder — the passive buzzer. It looks almost identical to the active buzzer from an earlier quest, but it works very differently. The active buzzer has its own internal circuit that makes it beep at one fixed pitch. The passive buzzer is just a tiny speaker — it needs the Arduino to tell it *exactly* how fast to vibrate.

And that means the Engineer can make it play *any note*. Any pitch. Any melody.

"Time to give NEXUS a voice," the Engineer says, and gets to work.

---

## THE LAW

**THE 12th LAW: THE VIBRATION LAW**

Sound is vibration. When something vibrates, it pushes and pulls the air around it, creating pressure waves that travel to your ears. Your ears convert those waves into signals your brain hears as sound.

What makes a note sound *high* or *low* is how *fast* it vibrates — its **frequency**, measured in Hz (Hertz, or vibrations per second).

**The guitar string analogy:**
> Hold a guitar string loosely and pluck it — it vibrates slowly and makes a LOW pitch.
> Tighten it and pluck it again — it vibrates fast and makes a HIGH pitch.
>
> The passive buzzer works the same way. The Arduino sends rapid on/off pulses to the buzzer. Fast pulses = high pitch. Slow pulses = low pitch.

`tone(pin, frequency, duration)` tells the Arduino exactly how fast to pulse the buzzer pin:
- `pin` — which pin the buzzer is on
- `frequency` — how many times per second to vibrate (in Hz)
- `duration` — how many milliseconds to play before stopping

`noTone(pin)` stops the buzzer immediately.

**Arrays — lists of things:**
An **array** is a list of values stored under one name. Instead of 8 separate variables for 8 notes, you make one list:
```cpp
int melody[] = {262, 330, 392, 523};
```
`melody[0]` is the first item (262). `melody[3]` is the fourth (523). Arrays always count from 0, not 1.

This makes it easy to loop through every note in a melody with a `for` loop.

**Note frequencies:**

| Note | Frequency |
|------|-----------|
| C4   | 262 Hz    |
| D4   | 294 Hz    |
| E4   | 330 Hz    |
| F4   | 349 Hz    |
| G4   | 392 Hz    |
| A4   | 440 Hz    |
| B4   | 494 Hz    |
| C5   | 523 Hz    |

Middle C on a piano is C4 = 262 Hz. Concert A (what orchestras tune to) is A4 = 440 Hz.

---

## BLUEPRINT

The passive buzzer has two legs. One leg is longer (positive) and one is shorter (negative) — or one leg may be marked with a `+` symbol.

```
  Arduino pin 8 ──── [Buzzer + leg]
  Arduino GND   ──── [Buzzer - leg]
```

That's it — no resistor needed for the buzzer.

**How to tell active vs. passive buzzer:**
- Active buzzer: usually has a white sticker or label on top. Plug it into power and GND — it beeps on its own.
- Passive buzzer: plain black cylinder, no label. Needs the Arduino to drive it with `tone()`.

If `tone()` doesn't work, try swapping to the other buzzer in your kit. If it beeps when you just plug it to power, that's the active one — use the other one for this quest.

---

## BUILD MISSION

1. Push the passive buzzer into the breadboard so its two legs are in different rows.
2. Connect the **longer leg** (+) of the buzzer to **Arduino pin 8** with a wire.
3. Connect the **shorter leg** (–) of the buzzer to **Arduino GND** with a wire.

**Check your work:**
- [ ] Buzzer + leg → pin 8
- [ ] Buzzer – leg → GND

That's a two-wire circuit. Simple build, powerful result.

**If your circuit doesn't work:**
- Is it the *passive* buzzer? Active buzzers won't work with `tone()` — they'll just make a faint clicking noise.
- Try swapping the two legs (buzzer polarity sometimes doesn't matter, but trying is worth it).
- Upload the code and listen closely — the melody might be very quiet if the buzzer is held loose in the breadboard. Push it in firmly.
- Try a different pin. Change `buzzerPin = 8` to `buzzerPin = 9` in the code, and rewire accordingly.

---

## CODE CORE

```cpp
// ============================================
// ROBOT ENGINEER ACADEMY — QUEST 12
// Robot Voice: NEXUS plays its first melody!
// ============================================

int buzzerPin = 8;  // Passive buzzer on pin 8

// Note frequencies in Hz (vibrations per second)
// #define creates a named constant — like a permanent label
#define NOTE_C4  262
#define NOTE_D4  294
#define NOTE_E4  330
#define NOTE_F4  349
#define NOTE_G4  392

// NEXUS: "Loading my melody data..."
// The melody: Ode to Joy (first 8 notes)
// An array is a list — melody[0] is the first note, melody[7] is the last
int melody[]    = {NOTE_E4, NOTE_E4, NOTE_F4, NOTE_G4,
                   NOTE_G4, NOTE_F4, NOTE_E4, NOTE_D4};

// How long each note plays (in milliseconds — 400ms = almost half a second)
int durations[] = {400, 400, 400, 400,
                   400, 400, 400, 600};  // Last note is longer

void setup() {
  pinMode(buzzerPin, OUTPUT);   // Buzzer pin is an output
  Serial.begin(9600);
  Serial.println("NEXUS VOICE MODULE ONLINE");
  Serial.println("Melody data loaded: ODE TO JOY");
}

void loop() {
  // NEXUS: "Playing startup melody — here we go!"
  Serial.println("Playing melody...");

  // Loop through all 8 notes in the melody array
  // i starts at 0 (first note), counts up to 7 (last note)
  for (int i = 0; i < 8; i++) {

    // NEXUS: "Playing note number [i]..."
    Serial.print("Note ");
    Serial.print(i + 1);        // Print 1-8 (not 0-7) so it reads naturally
    Serial.print(": ");
    Serial.print(melody[i]);    // Print the frequency in Hz
    Serial.println(" Hz");

    // Play note i at frequency melody[i] for durations[i] milliseconds
    tone(buzzerPin, melody[i], durations[i]);

    // Wait for the note to finish, plus a small gap between notes
    delay(durations[i] + 50);   // 50ms silence between notes keeps them separate
  }

  // NEXUS: "Melody complete. Entering rest mode..."
  noTone(buzzerPin);   // Make sure buzzer is off between loops
  Serial.println("Melody complete. Resting 3 seconds.");
  delay(3000);         // Wait 3 seconds before playing again
}
```

**What you should hear:** Ode to Joy's first eight notes playing on repeat with a 3-second pause between each loop. It'll sound a bit like a music box — simple but unmistakably musical.

---

## CHALLENGE MISSIONS

**Challenge 1 — Write Your Own Melody:**
Change the `melody[]` array to any notes you want! Here are the frequencies to use:

| Note | Hz  | Note | Hz  |
|------|-----|------|-----|
| C4   | 262 | C5   | 523 |
| D4   | 294 | D5   | 587 |
| E4   | 330 | E5   | 659 |
| F4   | 349 | F5   | 698 |
| G4   | 392 | G5   | 784 |
| A4   | 440 | A5   | 880 |
| B4   | 494 | B5   | 988 |

Try: `{262, 262, 392, 392, 440, 440, 392}` — that's Twinkle Twinkle Little Star!

Don't forget: if you change the number of notes in `melody[]`, update `durations[]` to have the same number of values, and change `i < 8` to match your new count.

**Challenge 2 — Button-Activated Melody:**
Add a button (from a previous quest) on pin 2 with `INPUT_PULLUP`. Wrap the melody `for` loop inside `if (digitalRead(2) == LOW)`. Now NEXUS only plays when the Engineer presses the button — like a real greeting sequence!

**Challenge 3 — Faster or Slower:**
Change all the values in `durations[]` to smaller numbers (like 200) for a fast, urgent-sounding melody. Or larger numbers (like 800) for slow and dramatic. What does Ode to Joy sound like at robot speed?

---

## XP REWARD

```
╔══════════════════════════════════════════════════════╗
║  QUEST 12 COMPLETE                                   ║
║  +10 XP EARNED                                       ║
║  ROBOT PART UNLOCKED: *** VOICE MODULE ***           ║
║                                                      ║
║  NEXUS HAS FOUND ITS VOICE.                          ║
╚══════════════════════════════════════════════════════╝
```

**Next quest unlocked:**
- **Q13 — Feel the World** (NEXUS gets its Environment Sensor)
