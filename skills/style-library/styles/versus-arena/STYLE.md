<!-- motionforge style · © 2026 motionforge contributors, MIT -->
# Versus Arena

> Two brands face off across a diagonal split: their colours fill each half, metrics arrive round by round as twin bars that shoot toward the centre, a tug-of-war meter moves with every win, and the verdict lands on a final scoreboard.

| Category | Engine | Best for | Effort |
|---|---|---|---|
| Data rankings & races | hyperframes (HTML/SVG; optional three.js product turntables per side) | brand vs brand, product vs product, country vs country, "which is bigger" episodes | medium |

## 1. Essence
- In one sentence: a fair fight made visible, where every round has a clear winner and the score is never in doubt.
- Three adjectives: competitive, fair, punchy.
- Signature move: the centre clash. Each round, two bars shoot from the outer edges toward the centre line in 0.5 s; the longer one crosses 24 px over the line, the line flashes in the winner's colour, and the tug-of-war meter shifts one notch.

## 2. Use it for / avoid it for
- Use for: exactly two contenders, 4 to 8 comparable metrics, 30 to 120 s; also as a segment inside a longer ranking video.
- Avoid for: three or more contenders (use `countdown-reveal` or `race-broadcast`), metrics in different units on the same bar (normalise or split), one-sided comparisons (the format implies a contest).
- Honesty: metrics use the same unit, year and definition on both sides; normalised bars (per capita, per store) are labelled; a round with no clear winner (within 2 %) is called a draw, not forced.

## 3. Palette
| Token | Hex | Job |
|---|---|---|
| background | #0B0C10 | the arena floor between the halves |
| ink | #FFFFFF | metric names, values, scores |
| accent | #F4F1E8 | the centre line and the verdict frame; it takes the winner's colour only during a clash flash |
| support | #30333C | round counter, inactive meter notches, dividers |
| support-2 | #A3A7B1 | units, sources, round labels |

Contender colours are data: left and right each own one colour (brand colour if permitted, otherwise #E14B4B and #3E7BF0); each half is filled with its colour at 14 % over the background, darkened toward the outer edge.

Rules: the two contender colours must differ by at least 40° of hue and pass a colour-blind check (deuteranopia) against each other; if not, the right side switches to the ramp's blue and keeps its logo.

## 4. Type
- Display: Big Shoulders Display (OFL) 900, 120 px at 1920×1080 for contender names, uppercase, tracking +0.01 em; "VS" in the same face at 64 px inside the centre medallion.
- Metric names: Inter (OFL) 700, 34 px, centred on the line.
- Values: Inter 800, 54 px, tabular figures; units Inter 500, 22 px muted.
- Labels: JetBrains Mono (OFL) 500, 16 px, uppercase, +0.14 em ("ROUND 3 / 6", "SOURCE").
- Language coverage: Big Shoulders Display, Inter and JetBrains Mono ship latin-ext on Fontsource.

## 5. Surfaces and texture
- Background: two halves split by a line tilted 8° from vertical, each half a horizontal gradient from the contender colour at 18 % (inner) to 6 % (outer); a centre medallion 120 px with a 2 px accent ring.
- Materials: bars are solid contender colour, 64 px tall, square at the outer edge, 12 px rounded at the centre tip; the leading tip has a 2 px white edge.
- Texture: static grain 3 %; a subtle 1 px diagonal hatching (6 % opacity) inside each half to give the colours depth.
- Never: lightning bolts, fire, "fight" sound effects, cartoon gloves, any imagery suggesting the brands are literally fighting.

## 6. Framing and layout
- 16:9 (main): contender names top left and top right (y 90 to 210, x 120 to 760 and 1160 to 1800), logos above the names at 96 px; metric rounds stack in the centre y 300 to 820, one active row at y 520; tug-of-war meter y 900 to 940, 1200 px wide, 12 notches; round counter y 980; source y 1030.
- 9:16: contenders top and bottom instead of left and right (top half y 0 to 960, bottom half 960 to 1920), the split line tilted 8° from horizontal; metric rows centre on the split, bars grow from the top and bottom edges toward it; meter vertical on the left edge x 60.
- 1:1: as 16:9 with two metric rows visible.
- Density: one active round, at most two previous rounds shown above it at 40 % as a running record.

## 7. Motion
- Entrances: the split line draws from top to bottom in 0.5 s; each half's colour fills from the outer edge in 0.6 s; names slam in from the outer edges 80 px with back.out(2) in 0.4 s; the VS medallion scales from 0 with back.out(1.8) at 0.9 s.
- Rounds: metric name rises 20 px over 0.3 s; both bars shoot toward the centre in 0.5 s, power4.out, values counting with them; the winner's tip crosses the line by 24 px; the centre line flashes the winner's colour for 0.25 s; the meter shifts one notch with a 0.35 s back.out; the round row then slides up 96 px to join the record.
- Holds and rhythm: 4 to 7 s per round; a draw holds 1 s longer with both tips touching the line and a "DRAW" label.
- Exits: after the last round both halves wipe toward the winner's side over 0.8 s, leaving the winner's colour on 70 % of the frame for the verdict.
- Transitions: none between rounds (they flow); a hard cut in and out of the arena.
- Camera: static; a 1.5 % push on the verdict.
- Frame rate feel: smooth 30 fps; clashes may use one held frame at the moment of crossing for impact.
- Edit grammar: one sentence per round, the metric name on the first word, the winner on the clash.

## 8. Sound
- Bed: tense percussion, 100 to 120 BPM, −26 LUFS under the voice.
- Effects: a short whoosh per bar pair at −20 dB, one tight hit on each clash at −18 dB, a deeper hit on the verdict.
- Mix: voice first; final −14 LUFS integrated, true peak ≤ −1 dBTP.

## 9. Build recipe and checks
- Engine and templates: HyperFrames (HTML/SVG); `stat-counter` logic for the counts; optional `product-turntable-3d` per side for product duels.
- Signature scenes:
  - Arena open: split line draws, halves fill, names slam, VS medallion pops (1.4 s).
  - Clash round: twin bars shoot to the centre, winner crosses, line flash, meter notch.
  - Verdict: halves wipe to the winner, score "5 : 2" in Big Shoulders 220 px, one-line verdict in Inter 700.
  - Draw round: tips touch, "DRAW" label in the support colour, meter does not move.
- Steps: 1) define every metric with unit, year and source for both sides; 2) decide the rounds' order (save the closest round for last but one); 3) check the two colours for colour-blind contrast; 4) render a still of one clash and the verdict; 5) `qa-review`.
- Style checks: both sides use the same scale in every round; the longer bar really is the larger value; the meter total equals the round wins; nothing important crosses the platform's right-hand rail in 9:16.
- Common failures: a scale that changes between sides, metrics where "more" is worse without saying so (invert and label "lower is better"), forced winners on near-ties.

## Overrides
None in the library copy; project copies list their changes here.

## Credits
Original motionforge style, drawing on the general tradition of sports head-to-head graphics and comparison infographics.
