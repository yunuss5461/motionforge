<!-- motionforge style · © 2026 motionforge contributors, MIT -->
# Line Race Editorial

> A newspaper-grade line chart that races through time: lines grow across warm paper with their labels riding the tips, one story line in the accent, quiet annotations pinned to turning points, and an axis that rescales smoothly as records fall.

| Category | Engine | Best for | Effort |
|---|---|---|---|
| Data rankings & races | hyperframes (SVG paths with clip reveal) | trends of 2 to 8 series over time, market shares, prices, population, "how X overtook Y" stories | medium |

## 1. Essence
- In one sentence: the authority of a serious business paper's chart, with the momentum of a race.
- Three adjectives: rigorous, elegant, calm.
- Signature move: the riding label. Each series' name and current value travel at the tip of its line; when two tips come close, the labels slide apart vertically with a 0.3 s ease and a thin leader line keeps them attached.

## 2. Use it for / avoid it for
- Use for: continuous data over 10 or more time steps, where the shape of the trend matters more than the rank; 16:9 long-form and explainers; Shorts with 2 or 3 series.
- Avoid for: rankings of many competitors (use `race-broadcast`), categorical comparisons (use `versus-arena`), noisy daily data without smoothing (say which smoothing you used, or aggregate).
- Honesty: the y-axis starts at zero unless the chart says otherwise in a visible note; log scales are labelled "log scale"; annotations quote dates and sources; the line for the current period is solid, projections are dashed and labelled.

## 3. Palette
| Token | Hex | Job |
|---|---|---|
| background | #F6F1E7 | warm paper |
| ink | #1F1D1A | headline, axis labels, annotation text |
| accent | #C8102E | the one story line and its label |
| support | #6E8CA0 | the second most important line |
| support-2 | #B8B0A2 | all other lines, gridlines (#E3DCCD), axis rules |

Rules: one accent line, one support line, everything else in support-2; gridlines horizontal only, 1 px #E3DCCD; the zero line 1.5 px ink.

## 4. Type
- Display: Newsreader (OFL) 600, headline 54 px at 1920×1080, sentence case, tracking −0.01 em; a deck line in Newsreader 400 italic, 28 px.
- Body / annotations: IBM Plex Sans (OFL) 500, 21 px.
- Labels: IBM Plex Sans 600, 22 px for riding labels; IBM Plex Mono (OFL) 500, 16 px for axis ticks and dates, tabular figures.
- Language coverage: Newsreader, IBM Plex Sans and IBM Plex Mono ship latin-ext on Fontsource.

## 5. Surfaces and texture
- Background: flat warm paper, no vignette.
- Materials: lines 3 px (story line 4.5 px) with round joins; a 6 px tip dot; area under the story line at 6 % accent only when the story is about volume.
- Texture: static paper grain 2.5 %.
- Never: glow on lines, 3D, drop shadows, more than two colours that compete, a legend box (labels ride the lines instead).

## 6. Framing and layout
- 16:9 (main): headline x 120, y 90 to 150; deck y 165 to 200; plot area x 120 to 1560, y 260 to 900; riding labels in a right gutter up to x 1820; x-axis dates y 930; annotations as 280 px notes with a 1 px leader to the point; source and notes y 1010 to 1040 (IBM Plex Sans 15 px).
- 9:16: headline y 260 to 380; plot y 560 to 1360 (x 60 to 820), riding labels up to x 1000, annotations above the plot y 420 to 540 one at a time.
- 1:1: plot in the upper 75 %, annotations under it.
- Density: at most 8 lines, at most 2 annotations visible, one of them in the accent.

## 7. Motion
- Entrances: headline fades up 0.5 s; axes and gridlines draw from left 0.6 s; lines start at the first time step.
- Race: a clip rect reveals all lines left to right at a constant data rate (0.3 to 1.0 s per time step); tips and labels are positioned from the same interpolated value (monotone cubic) so they never detach.
- Label collision: labels keep a minimum gap of 28 px; when tips cross, labels swap order over 0.3 s, power2.inOut, with leader lines.
- Axis: the y-max follows the smoothed series maximum × 1.12; gridline values cross-fade between nice steps (1, 2, 5 × 10ⁿ), labels only for the dominant step.
- Annotations: when the clip passes an annotated point, a 6 px ring pulses once (0.6 s), the note slides in 16 px over 0.35 s and holds 3 s.
- Exits: annotations fade 0.3 s; at the end non-story lines drop to 40 % and the story line's label grows to 28 px.
- Holds and rhythm: one annotation per 6 to 10 s at most.
- Transitions: none inside the chart; cut on sentence ends.
- Camera: static; an optional 4 % push into the final crossing point.
- Frame rate feel: smooth 30 fps.
- Edit grammar: the voice leads the reveal slightly (J-cut 0.3 s) so the viewer hears the turning point as the line reaches it.

## 8. Sound
- Bed: understated, piano or soft pads, 70 to 90 BPM, −28 LUFS under the voice.
- Effects: a quiet pencil tick on each annotation at −28 dB; nothing else.
- Mix: voice first; final −14 LUFS integrated, true peak ≤ −1 dBTP.

## 9. Build recipe and checks
- Engine and templates: HyperFrames with SVG; `templates/kinetic-title` for the headline and deck, `templates/cover-still` for the thumbnail; the planned `line-race` template in Paket 3 of the development plan, or the catalog Minimal Line Graph block after the HyperFrames audit; related reference style `data-story`.
- Signature scenes:
  - Overtake: the story line crosses its rival; labels swap with leaders; a note "2003: Bubbla overtakes Fizzo" slides in.
  - Record high: the axis rescales smoothly, a dashed horizontal "previous high" line stays for 2 s.
  - Zoom to detail: the plot crops to a five-year window over 1.2 s for a close look, then returns.
- Steps: 1) choose one story line before animating; 2) write the annotations as dated sentences with sources; 3) set the data rate from the narration; 4) render stills at each annotation; 5) `qa-review`.
- Style checks: no label overlaps at any annotation still; the y-axis note is present if it does not start at zero; one accent line only.
- Common failures: legend boxes, too many accent colours, labels drifting off their lines, annotations that arrive before the line reaches the point.

## Overrides
None in the library copy; project copies list their changes here.

## Credits
Original motionforge style, drawing on the general tradition of business-newspaper charting and data journalism. No publication's design is copied.
