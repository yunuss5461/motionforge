<!-- motionforge style · © 2026 motionforge contributors, MIT -->
# World Heat Race

> A dark world map that heats up country by country as the years run: a sequential colour scale fills borders, the top five countries race in a side panel, and the camera drifts toward whichever region is changing fastest.

| Category | Engine | Best for | Effort |
|---|---|---|---|
| Data rankings & races | hyperframes (SVG map from world-atlas, Natural Earth data) or the catalog World Map block after the HyperFrames audit | country rankings over time: consumption, production, adoption, population, market presence | high |

## 1. Essence
- In one sentence: the viewer watches the world change shape as a pattern, then sees who leads in plain numbers.
- Three adjectives: global, informative, cinematic.
- Signature move: the heat front. Each year, countries whose value rose by more than 10 % brighten for 0.4 s along their borders (a 1.5 px ink outline that fades), so growth is visible as a moving front across the map.

## 2. Use it for / avoid it for
- Use for: values for 50 or more countries over 10 or more time steps; 16:9 first (the world is wide); 9:16 only with a regional crop.
- Avoid for: data for fewer than 20 countries (use `race-broadcast` with flags), totals that simply follow population (normalise per capita and say so), sub-national data (use the catalog US or Spain maps, or a regional map).
- Honesty: countries without data are hatched grey and the legend says "no data", never coloured as zero; the colour scale is shown with its breaks; per-capita and total values are never mixed; borders follow the Natural Earth dataset and the description names it.

## 3. Palette
| Token | Hex | Job |
|---|---|---|
| background | #0B0F14 | ocean and stage |
| ink | #EEF2F5 | titles, values, country names in the panel |
| accent | #FFB000 | the current leader's outline and its row in the panel |
| support | #1E2630 | land with no data (with 1 px #2C3644 hatching at 45°) |
| support-2 | #7F8B99 | borders (0.6 px), legend labels, source |

Sequential data scale (low to high, 7 steps, perceptually even): `#1B2A3A #1F4E5F #227A73 #4DA67A #A4C46A #F2D25C #FF8F3D`.

Rules: the data scale never uses the accent; the accent outline is 2 px and goes only on the current leader; land colour always comes from the data scale or the no-data hatch.

## 4. Type
- Display: Manrope (OFL) 800, headline 56 px at 1920×1080, tracking −0.025 em.
- Body / captions: Manrope 600, 24 px.
- Labels: JetBrains Mono (OFL) 500, 16 to 22 px for values, the year and legend breaks, tabular figures.
- Year: Manrope 800, 140 px, bottom left over the ocean, at 85 % ink.
- Language coverage: Manrope and JetBrains Mono ship latin-ext on Fontsource; country names in the video language come from a reviewed list, never machine-translated on the fly.

## 5. Surfaces and texture
- Background: ocean #0B0F14 with a very soft radial light (4 %) over the region in focus.
- Materials: countries flat-filled from the scale; borders 0.6 px support-2; the projection is Equal Earth (area-true, so big countries do not look bigger than they are).
- Texture: static grain 3 % over the ocean only.
- Never: globe spins for decoration (use `globe-arcs-3d` when a route matters), glowing countries, 3D extruded countries unless the extrusion itself is the data.

## 6. Framing and layout
- 16:9 (main): map x 60 to 1440, y 180 to 960; top-five panel x 1480 to 1840, y 220 to 700 (rows of 92 px: flag 36 px, name, value, small bar); legend x 1480 to 1840, y 760 to 820; year bottom left x 90, baseline y 1000; headline y 70 to 140; source y 1040.
- 9:16: a regional crop (e.g. Europe or Asia) y 300 to 1200; panel under it y 1260 to 1680 with five rows; year top right y 200.
- 1:1: map upper 65 %, panel lower 35 % with three rows.
- Density: the map, five panel rows, the legend, the year; one annotation at a time.

## 7. Motion
- Entrances: the map fades up from the ocean colour in 0.8 s with borders drawing at 0.6 px; countries fill to their first-year colour in a west-to-east sweep over 1.0 s; panel rows slide in 24 px with a 0.06 s stagger.
- Race: colours interpolate in a perceptual space (OKLab) between yearly values; panel ranks use the smoothed-rank method of `race-broadcast` (0.36 s window); the heat front outlines fade over 0.4 s.
- Camera: a slow drift (no more than 6 % zoom and 120 px pan per 10 s) toward the region with the largest growth in the next five years, computed from the data; never moves during a lead change.
- Lead change: the new leader's outline turns accent, its panel row flashes the accent at 20 % for 0.5 s, and the year digits pause for one beat.
- Exits: annotations fade 0.3 s; the end frame zooms back to the full map over 1.2 s.
- Holds and rhythm: 0.5 to 1.2 s per year in long form; at least one annotation per decade.
- Transitions: none inside the map; cut on sentence ends.
- Frame rate feel: smooth 30 fps.
- Edit grammar: narration names a region before the camera drifts there; numbers are spoken only for the top three.

## 8. Sound
- Bed: atmospheric electronic, 80 to 100 BPM, −26 LUFS under the voice.
- Effects: a soft swell under each camera drift at −26 dB; one low hit on a lead change at −18 dB.
- Mix: voice first; final −14 LUFS integrated, true peak ≤ −1 dBTP.

## 9. Build recipe and checks
- Engine and templates: HyperFrames with an SVG map from `world-atlas` (Natural Earth data, ISC; the same package `globe-arcs-3d` uses) and an Equal Earth projection, or the catalog World Map block after the HyperFrames audit; panel logic shared with `race-broadcast`.
- Signature scenes:
  - Heat front: growth outlines sweep across the map each year.
  - Regional dive: the camera drifts and zooms 6 % into a region while its countries' values appear as small labels.
  - Then and now: the map splits vertically, first year on the left, last year on the right, same scale, held 3 s.
- Steps: 1) map every country name to an ISO 3166 code and list unmatched names; 2) decide total or per capita and write it in the subtitle; 3) choose breaks for the 7-step scale from the whole time range, not the first year; 4) render stills for the first year, a lead change and the last year; 5) `qa-review`.
- Style checks: no-data countries are hatched, not dark; the legend breaks match the scale; the panel's top five equal the five highest values in the data for that year; borders stay legible at 360 px wide (otherwise crop to a region).
- Common failures: rainbow scales, breaks chosen from one year that saturate later, unlabeled per-capita data, camera moves that hide the leader.

## Overrides
None in the library copy; project copies list their changes here.

## Credits
Original motionforge style, drawing on the general tradition of thematic cartography and animated data maps. Map data: Natural Earth (public domain) via world-atlas (ISC).
