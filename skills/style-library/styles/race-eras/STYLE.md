<!-- motionforge style · © 2026 motionforge contributors, MIT -->
# Race Eras

> A ranking race whose whole design ages with the data: 1950s halftone print, 1970s warm film, 1980s neon, 1990s chrome, 2000s gloss and 2010s flat, each decade dissolving into the next while the bars keep racing.

| Category | Engine | Best for | Effort |
|---|---|---|---|
| Data rankings & races | hyperframes (HTML/SVG + CSS filters; canvas layer for the halftone pass) | century-long brand and product histories, "how tastes changed" stories, nostalgia-led rankings | high |

## 1. Essence
- In one sentence: the viewer feels time passing through the design itself, not only through a year counter.
- Three adjectives: nostalgic, surprising, controlled.
- Signature move: the era handover. At each decade boundary the background, bar material, headline typeface and grain change over 1.2 s through a soft wipe from left to right, while bars and values keep moving without a hitch.

## 2. Use it for / avoid it for
- Use for: rankings that span at least four decades; consumer brands, music, cars, toys, foods; long-form 16:9 videos where the decade changes are story beats.
- Avoid for: spans shorter than 30 years (one or two eras only: use `race-broadcast`); serious or sensitive data (deaths, disasters, conflicts); brands whose guidelines forbid recolouring.
- Honesty: the era look is decoration only; bars keep the same series colours in every era (only material and finish change), so the viewer never loses track of who is who.

## 3. Palette
| Token | Hex | Job |
|---|---|---|
| background | era table below | the stage of the current decade |
| ink | era table below | names, values, year |
| accent | #E8B13A | one constant thread: the current leader's outline and the year underline, the same in every era |
| support | #7D7A73 | rank numbers, units, axis labels (alpha adjusted per era) |

Era table (background / ink / bar finish / grain):

| Era | Background | Ink | Bar finish | Texture |
|---|---|---|---|---|
| 1950s | #EFE6D2 newsprint | #1E1B16 | flat ink with 45° halftone dots at 18 % | paper grain 6 %, slight 0.3 px blur |
| 1960s | #F2E9DA | #23201B | flat, rounded 14 px | paper grain 4 % |
| 1970s | #2A1D14 brown | #F1E2C8 | soft vertical gradient, 1 px cream highlight | warm film grain 5 %, 4 % orange halation |
| 1980s | #0D0820 | #F6F0FF | 2 px coloured outline + 30 % fill, scanline overlay 3 % | none |
| 1990s | #10161D | #E9EEF2 | chrome: 3-stop grey gradient tinted by the series colour | 2 % dither |
| 2000s | #0E1830 | #FFFFFF | glossy: top 50 % white sheen at 28 %, reflection strip | none |
| 2010s+ | #0B0D12 | #F3F1EC | flat colour, 8 px corners | static grain 3 % |

Rules: series colours stay constant across eras; ink must reach 4.5:1 contrast on every era background (checked per era); the accent is the only colour that never changes.

## 4. Type
- Display per era (headline and year only; body never changes):
  - 1950s to 1960s: Fraunces (OFL) 700, optical size high, 60 px, slight negative tracking.
  - 1970s: Fraunces 900, 64 px; with the variable build (`@fontsource-variable/fraunces`) set the SOFT axis to 50 for the rounded seventies feel; the static files have no SOFT axis, so the look is plainer without it.
  - 1980s: Unbounded (OFL) 800, 56 px, uppercase, +0.04 em.
  - 1990s: Archivo (OFL) 800, 56 px; with the variable build (`@fontsource-variable/archivo`) set width to 125 for the expanded look; the static files are normal width only.
  - 2000s: Space Grotesk (OFL) 700, 58 px.
  - 2010s+: Inter (OFL) 800, 58 px, −0.035 em.
- Body / captions: Inter 500 to 700, 22 to 25 px, constant across eras so names and values never jump.
- Labels: JetBrains Mono (OFL) 500, 15 to 20 px.
- Typeface change: cross-fade two stacked copies of the headline over 0.6 s inside the era wipe; never swap a font mid-word in one element.
- Language coverage: all five display families ship latin-ext on Fontsource; Turkish glyphs (ı İ ş ğ) must be checked per era font with the glyph script in `qa-review` (X4).

## 5. Surfaces and texture
- Background: the era colour plus one era motif at 6 to 10 % opacity: 1950s a printed rule border, 1970s a large rounded sunburst, 1980s a perspective horizon line (a single line, never a grid floor), 1990s a brushed-metal band behind the year, 2000s a soft light streak, 2010s nothing.
- Materials: see the era table; logo roundels follow the bar finish.
- Texture: static per era, generated once from a seed; the halftone is rendered on a canvas layer from the bar geometry each frame (deterministic, no noise animation).
- Never: animated film dust, VHS tracking glitches, fake scratches that move, any era effect on the numbers themselves.

## 6. Framing and layout
- 16:9 (main): the `race-broadcast` grid (8 slots of 78 px from y 212, bars from x 404, right panel from x 1500), with the era label as a small stamp above the year ("THE 1970s", 15 px, +0.2 em).
- 9:16: headline y 260 to 420, year and era stamp y 460 to 600, 10 slots of 92 px from y 650.
- 1:1: 6 slots, era stamp in the top left under the headline.
- Density: as `race-broadcast`; the era motif sits behind everything and never behind values.

## 7. Motion
- Entrances: as `race-broadcast`; the first era is already in place at frame 0.
- Era handover: starts 0.6 s before the decade boundary, lasts 1.2 s; a vertical soft-edged mask (160 px feather) sweeps left to right, revealing the new era's background, motif, grain and bar finish; the headline cross-fades inside the same window; the year's digits roll as usual.
- Rank swaps and values: smoothed rank (0.36 s window) and monotone cubic values, as `race-broadcast`.
- Holds and rhythm: at least 6 seconds per era so each look registers; long-form 0.8 to 1.2 s per year.
- Transitions: era handovers are the only transitions; no cuts inside the race.
- Camera: static; a 1 % push during each era handover.
- Frame rate feel: smooth 30 fps in every era (no stepped frames, they break the race).
- Edit grammar: narration names the era as the wipe starts ("By the seventies…"); one fact per era.

## 8. Sound
- Bed: one continuous track with an era-matched stinger at each handover (a brass hit, a funk guitar lick, a synth stab, a turntable scratch, a modern sub drop) at −20 dB, recorded or licensed, never imitating a specific famous song.
- Effects: none per swap; a soft paper rustle under the 1950s wipe only.
- Mix: voice first; final −14 LUFS integrated, true peak ≤ −1 dBTP.

## 9. Build recipe and checks
- Engine and templates: HyperFrames with a canvas layer for the 1950s halftone; `templates/kinetic-title` for the era-specific headline, `templates/cover-still` for the thumbnail; start from `examples/styles/race-broadcast/` and add an era table driving CSS variables (`--mf-bg`, `--mf-text`, bar finish classes) through the style tokens.
- Signature scenes:
  - Era handover: feathered left-to-right mask, 1.2 s, power2.inOut, everything but the data changes.
  - Era stamp: "THE 1980s" letter-spaced stamp drops 12 px and settles in 0.4 s when the wipe passes the panel.
  - Nostalgia freeze: on a key event the race slows to 25 % for 1.5 s while the event card appears in that era's typography.
- Steps: 1) decide which eras the data spans; 2) check ink contrast on each era background; 3) build era tokens; 4) render one still per era before the full render; 5) `qa-review`.
- Style checks: a viewer can track one brand across all eras without reading its name (same colour, same position logic); every era still passes 4.5:1 contrast; the handover never coincides with a lead change (shift the handover by up to 0.5 s if it does).
- Common failures: era effects that touch the data (bars changing colour), kitsch overload (more than one motif per era), handovers so long that two eras compete on screen.

## Overrides
None in the library copy; project copies list their changes here.

## Credits
Original motionforge style, drawing on the general visual vocabulary of 20th-century print, film and screen design. No specific publication, film, game or brand design is copied.
