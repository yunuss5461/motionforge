<!-- motionforge style · © 2026 motionforge contributors, MIT -->
# Race Broadcast

> A broadcast-grade bar chart race on a near-black stage: bars glide past each other instead of jumping, the year rolls like an odometer, event cards and a decade scrubber tell the story, and every change of leader gets one gold moment.

| Category | Engine | Best for | Effort |
|---|---|---|---|
| Data rankings & races | hyperframes (HTML/SVG, one paused timeline; catalog Bar Chart Race block as the starting point after the HyperFrames audit) | brand, company, country and product rankings over decades; "who sold the most" series; market-share histories | high |

## 1. Essence
- In one sentence: a long ranking history that feels like a live sports broadcast: calm, legible, and with a clear climax every time the lead changes.
- Three adjectives: authoritative, kinetic, legible.
- Signature move: the lead change. The new leader's bar gets a single light sweep, a gold-outlined "NEW #1" chip appears inside the bar start, and the whole stage pushes in 1.6 % and back over 1.3 s.

## 2. Use it for / avoid it for
- Use for: rankings with 6 to 12 competitors over 20 to 100 time steps; YouTube long-form (16:9) first, Shorts cut-downs second; series where every episode must look identical.
- Avoid for: fewer than 5 competitors (use `versus-arena`), a single trend line (use `line-race-editorial`), geographic data (use `world-heat-race`), data with fewer than 8 time steps (nothing races; use `data-story`).
- Honesty: the source line is always on screen; values between data points are interpolated, and the description says so ("yearly data, interpolated between years"); money is labelled nominal or inflation-adjusted with the base year; a brand that did not exist yet has no bar, never a zero bar.

## 3. Palette
| Token | Hex | Job |
|---|---|---|
| background | #0A0C11 | near-black stage; never pure black |
| ink | #F3F1EC | values, leader name, year, timeline progress |
| accent | #F2C14E | gold: kicker rule, headline accent words, "NEW #1" chip, final-standings label; nothing else |
| support | #8B8F99 | labels, rank numbers, units, non-leader names at 85 % |
| support-2 | #1C2029 | grid lines, timeline base, card borders |

Series colours are data, not chrome: one fixed colour per competitor for the whole series of videos (brand colour if the brand has one and permits use, otherwise this ramp): `#D9544D #3F6FD8 #2FA46F #E59A2E #4FA3C7 #8C5CC9 #D3558F #1FA59A #A89466 #7C8594`. Logo roundels use the series colour at 62 % brightness.

Rules: gold appears in at most two places at once; bars never use gold; the era tint (a radial light from the top left) shifts warm amber in the 1950s, orange in the 1970s, teal in the 1990s and blue in the 2010s at 20 % opacity, so the decade is felt before it is read.

## 4. Type
- Display: Inter (OFL) 800, 58 px headline at 1920×1080 (72 px at 1080×1920), sentence case, tracking −0.035 em; one or two words in Instrument Serif (OFL) italic 400 in gold.
- Body / captions: Inter 500 to 700, 21 to 25 px; brand names Inter 700 25 px, right-aligned to the bar start.
- Labels: JetBrains Mono (OFL) 500, 15 to 20 px, for rank numbers (`01`…`08`), axis ticks and decade labels; Inter 700 15 px uppercase with 0.2 em tracking for section labels (YEAR, TOTAL MARKET).
- Numbers: tabular figures everywhere (`font-feature-settings: "tnum"`), one decimal, the unit in a smaller muted size after the value ("454.1 M").
- Language coverage: all three families ship latin and latin-ext on Fontsource; load both subsets for Turkish and other Latin languages (see `engines/hyperframes/base.css`).

## 5. Surfaces and texture
- Background: flat #0A0C11 with the era tint and a soft vignette (transparent to 55 % black at the corners).
- Materials: bars are flat colour with a 16 % white-to-transparent sheen on the top half and a 14 % dark lip at the bottom; corners 6 px at the start, 10 px at the tip; logo roundels 44 px with a 3 px stage-coloured ring so they read on any bar.
- Texture: static grain at 3.5 % in overlay mode, generated once from a seeded generator.
- Never: animated grain, glowing bars, 3D extrusion, drop shadows under text, purple gradients, a drawn background grid (the value gridlines are data, kept at #1C2029).

## 6. Framing and layout
- 16:9 (main, 1920×1080): kicker y 78, headline y 106 to 170; tick labels y 182; bars from x 404, up to 1000 px long, 8 slots of 78 px from y 212 (bar 56 px, gap 22 px); rank numbers x 120; names right-aligned to x 384; right panel x 1500 to 1830: year odometer y 222 to 354, event card y 428 to 560, total market and sparkline y 664 to 800; decade scrubber y 952 to 1000; source line y 1030.
- 9:16 (1080×1920): headline y 260 to 420; year odometer centred above the chart y 460 to 590; 10 slots of 92 px from y 640 (bars from x 300, up to 640 px); event card y 1590 to 1720 over the bottom slots' fade; scrubber y 1760; keep everything inside x 60 to 1020 and clear of the right-hand button rail (no values past x 940 in y 900 to 1700: values flip inside the bar when they would cross it).
- 1:1: 6 slots, year in the top right, no event card (events become the caption line).
- Density: at most 8 bars (16:9) or 10 (9:16) on screen; one event card at a time; one chip at a time.

## 7. Motion
- Entrances: kicker rule scales in 0.45 s; headline words rise out of a mask 0.55 s each, 0.075 s stagger, back.out(1.7); gridlines fade in 0.6 s; bars grow from zero in rank order, 0.65 s each, 0.06 s stagger, power3.out; right panel rises 30 px over 0.6 s.
- Rank swaps: never instant. The displayed rank is the weighted mean of the true rank over the previous 0.36 s (12 samples, quadratic weights), so bars glide through each other in about a third of a second and every frame is still a pure function of time.
- Values: monotone cubic interpolation (Fritsch–Carlson) between data points, so curves never overshoot into impossible values; the axis maximum follows the smoothed leader value × 1.1.
- Year: odometer per digit; each digit rolls during the last 38 % of its step with smoothstep easing, a carry rolls the next digit at the same time; the column has a 22 % soft mask at top and bottom.
- Axis ticks: nice steps (1, 2, 5 × 10ⁿ), cross-faded between the two nearest steps on a log scale; labels only show for the dominant step, so they never overlap.
- Exits: below-the-fold competitors fade out over 0.6 ranks; event cards slide in 36 px over 0.45 s and fade out over 0.4 s.
- Holds and rhythm: 0.17 s per year (70 years ≈ 12 s) for a preview; 0.6 to 1.2 s per year for a long-form video; hold the last frame 2.2 s with the final-standings card.
- Transitions: none inside the race; cut to and from it on a sentence end.
- Camera: static except the lead-change push (sine in-out, peak 1.6 %).
- Frame rate feel: smooth 30 fps; 60 fps only if the platform and render budget allow.
- Edit grammar: cold open on the race already moving (no intro card longer than 1.6 s); the narration lands on events, not on every year; one lead change per narration beat.

## 8. Sound
- Bed: cinematic pulse or minimal electronic, 90 to 110 BPM, −26 LUFS under the voice, a riser into each lead change.
- Effects: a soft low "thud" on each lead change at −18 dB; a quiet tick on each decade boundary at −28 dB; no sound per rank swap.
- Mix: voice first, ducked bed; final −14 LUFS integrated, true peak ≤ −1 dBTP.

## 9. Build recipe and checks
- Engine and templates: HyperFrames; `templates/kinetic-title` for the opening headline, `templates/stat-counter` logic for the total-market value, `templates/cover-still` for the thumbnail; reference scene `examples/styles/race-broadcast/` (16:9, fictional data); after the HyperFrames audit, start from the catalog Bar Chart Race block and apply this spec, or from the planned `templates/bar-chart-race`.
- Signature scenes:
  - Lead change: chip "NEW #1" scales in with back.out over 0.33 s inside the new leader's bar start, a 180 px white sweep crosses the bar in 0.7 s, the stage pushes 1.6 % over 1.3 s; the chip holds 1.5 s and fades.
  - Event card: a 320 px card with a 4 px stripe in the event brand's colour, the year in JetBrains Mono, one sentence in Inter 500 21 px; the brand's bar gets a 2 px ink ring for six data steps.
  - Decade scrubber: 1700 px base line, decade ticks and labels, an ink progress fill and a 14 px head; event diamonds in brand colours go from 35 % to 100 % opacity when passed.
  - Total-market sparkline: 300 × 70 px line plus a 6 % fill, drawn up to the current year, value above it.
  - Final standings: gold label, the winner in Instrument Serif italic 40 px with the value, one sentence for second and third.
- Steps: 1) clean the data (yearly, one unit, source and year range written down); 2) pick the series colours once for the whole series; 3) write 3 to 6 events that the narration will mention; 4) set seconds per year from the narration length; 5) render three stills (a lead change, an event card, the final card) before the full render; 6) `qa-review`.
- Style checks: the source line is readable at 360 px wide; values never collide with the right panel (longest value + unit ends before x 1460); the same frame renders to the same hash twice; names of 12 characters still fit (otherwise shorten or use the logo only).
- Common failures: ranks that jump (smoothing window missing), an axis that rescales every frame (use the smoothed leader), labels overlapping during swaps (allowed for ≤ 0.36 s, otherwise slow the race), too many events (more than one per 8 seconds reads as noise).

## Overrides
None in the library copy; project copies list their changes here.

## Credits
Original motionforge style, drawing on the general tradition of animated ranking charts and sports broadcast graphics. All brands, events and numbers in the reference scene are fictional.
