<!-- motionforge style · © 2026 motionforge contributors, MIT -->
# Countdown Reveal

> A premium top-ten countdown: giant outlined rank numerals in a deep stage, each entry arriving as a lit card on a slow camera dolly, a stat that counts up, and number one held back behind a curtain of light until the last beat.

| Category | Engine | Best for | Effort |
|---|---|---|---|
| Data rankings & races | hyperframes + three.js (card stack and dolly; flat HTML fallback) | "top 10" lists with data, best-sellers of a year, richest, fastest, most-streamed, "ranked by" episodes | high |

## 1. Essence
- In one sentence: every rank feels earned, and the viewer stays to the end because number one is visibly withheld.
- Three adjectives: dramatic, premium, paced.
- Signature move: the rank numeral. A 520 px outlined numeral fills the left of the frame, its outline draws on in 0.6 s, then it fills with the entry's colour from bottom to top as the stat counts up.

## 2. Use it for / avoid it for
- Use for: ranked lists of 5 to 10 items with one measurable stat each; 16:9 long-form segments of 8 to 15 s per entry; Shorts with 3 to 5 entries.
- Avoid for: rankings that change over time (use `race-broadcast`), opinion lists without a measure (the style promises data), more than 10 entries.
- Honesty: every entry shows its number, unit and year; ties share a rank and say so; the source sits under each stat, not only at the end.

## 3. Palette
| Token | Hex | Job |
|---|---|---|
| background | #07080C | deep stage |
| ink | #F5F3EE | entry name, stat, body |
| accent | #E9C46A | number one only: its numeral, its light curtain, its final frame |
| support | #2B2F3A | outlined numerals before they fill, card edges, the countdown rail |
| support-2 | #9A9EA8 | stat labels, source lines, the rank rail labels |

Entry colours are data: each entry uses its brand colour or a ramp colour for its numeral fill and card rim light; rank 1 always uses the accent regardless of brand.

Rules: gold is never used before number one appears; a lit card gets its rim light in the entry colour at 60 % and a 4 % tinted floor reflection.

## 4. Type
- Display: Anton (OFL) 400 for rank numerals, 520 px at 1920×1080 (380 px at 1080×1920), tracking −0.01 em, drawn as a 3 px outline before filling.
- Entry name: Inter (OFL) 800, 72 px, tracking −0.035 em; one qualifier in Instrument Serif (OFL) italic.
- Stat: Inter 800, 96 px with tabular figures; unit Inter 500, 36 px, muted.
- Labels: JetBrains Mono (OFL) 500, 18 px, uppercase, +0.12 em ("RANK 07 / 10", "SOURCE").
- Language coverage: Anton, Inter, Instrument Serif and JetBrains Mono all ship latin-ext on Fontsource.

## 5. Surfaces and texture
- Background: #07080C with one soft spotlight (ellipse 1200 × 700 px, entry colour at 10 %) behind the current card.
- Materials: cards 720 × 440 px, 18 px corners, a matte dark surface (#12141B) with a 1 px top highlight at 12 % and a rim light on the left edge in the entry colour.
- Texture: static grain 3 %; a faint floor plane with the card's reflection at 4 % (three.js) or a mirrored, blurred copy (flat fallback).
- Never: confetti, sparkles, lens flares, trophy clip art, animated noise.

## 6. Framing and layout
- 16:9 (main): numeral x 80 to 620, baseline y 820; card x 760 to 1480, y 260 to 700; stat block under the card y 730 to 860; countdown rail on the far right x 1720, ten 8 px dots from y 240 to 840 with the current rank filled; source line y 1030.
- 9:16: numeral top centre y 240 to 640 (380 px), card y 700 to 1140 (900 × 440), stat y 1180 to 1320, rail horizontal at y 1480; keep inside x 60 to 1020 and away from the right-hand rail of the platform.
- 1:1: numeral left half, card right half, stat under the card.
- Density: one entry on screen; the previous card is already leaving as the next numeral draws (0.5 s overlap).

## 7. Motion
- Entrances: camera dollies 0.8 m to the right in three.js (or the stage slides 320 px left in the flat fallback) over 0.9 s, power3.inOut; the numeral outline draws in 0.6 s; the card rises 40 px and tilts from 8° to 0° over 0.7 s, back.out(1.2); the name rises out of a mask 0.45 s; the stat counts up over 1.2 s, power2.out, while the numeral fills bottom to top.
- Exits: the card slides out with the dolly, the numeral fades to the support colour outline and drifts 60 px left.
- Holds and rhythm: 8 to 15 s per entry in long form, 4 to 6 s in Shorts; number one gets double time.
- Transitions: the dolly is the transition; between rank 2 and rank 1 the screen goes to black for 0.4 s, then a vertical light curtain (accent, 30 %) opens from the centre over 0.8 s to reveal number one.
- Camera: a slow 2 % push during every hold so no frame is dead.
- Frame rate feel: smooth 30 fps.
- Edit grammar: the voice says the rank and the name on the numeral draw, the stat on the count-up; the reveal of number one lands on a musical hit after a one-beat pause.

## 8. Sound
- Bed: cinematic, building across the list, 85 to 100 BPM, −26 LUFS under the voice.
- Effects: a low whoosh on each dolly at −20 dB; a short riser into number one; one impact on the curtain reveal at −14 dB.
- Mix: voice first; final −14 LUFS integrated, true peak ≤ −1 dBTP.

## 9. Build recipe and checks
- Engine and templates: HyperFrames + three.js (`engines/hyperframes/three`, `lights.studio`, `shadowCatcher`) for the card stack; flat HTML fallback for fast renders; `stat-counter` logic for the count-up; catalog typography blocks may supply the name entrance after the HyperFrames audit.
- Signature scenes:
  - Numeral draw and fill: SVG text outline, stroke-dashoffset 0.6 s, then a clip rect rises with the stat count.
  - Card on dolly: card arrives with tilt and rim light; reflection on the floor.
  - Curtain reveal: black 0.4 s, light curtain opens 0.8 s, gold numeral "1" draws, card rises, the stat counts up with an impact.
  - Recap wall: after number one, all ten cards shrink into a 5 × 2 grid in 1.2 s with their ranks, held 3 s for the end screen.
- Steps: 1) confirm the stat and source for every entry; 2) order and check ties; 3) build one entry scene and duplicate with parameters; 4) render stills of rank 10, rank 2 and the reveal; 5) `qa-review`.
- Style checks: numerals never cover the card; the stat is readable at 360 px wide; gold appears only from the curtain onward; the recap grid labels do not overlap.
- Common failures: entries that all feel the same length (vary holds by importance), numeral fills that do not match the stat timing, reflections that double the card's text (blur and fade them).

## Overrides
None in the library copy; project copies list their changes here.

## Credits
Original motionforge style, drawing on the general tradition of televised countdown shows and award reveals.
