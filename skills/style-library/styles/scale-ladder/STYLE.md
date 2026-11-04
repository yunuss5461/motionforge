<!-- motionforge style · © 2026 motionforge contributors, MIT -->
# Scale Ladder

> Big numbers made physical: amounts become stacks, blocks and areas on one shared scale, and the camera pulls back one order of magnitude at a time until a company's revenue dwarfs a country's budget.

| Category | Engine | Best for | Effort |
|---|---|---|---|
| Data rankings & races | hyperframes + three.js (instanced blocks, zoom-out by decades) or hyperframes SVG (2D squares) | revenue vs GDP, "how big is X", net worth comparisons, market caps, production volumes | medium |

## 1. Essence
- In one sentence: the viewer stops reading numbers and starts feeling sizes.
- Three adjectives: astonishing, precise, clean.
- Signature move: the decade pull-back. Each step the camera zooms out exactly 10× in 1.4 s while the previous item shrinks into a corner of the next, and a scale chip ("× 10") ticks over.

## 2. Use it for / avoid it for
- Use for: comparisons spanning at least two orders of magnitude; 5 to 9 items on one ladder; 16:9 and 9:16 equally.
- Avoid for: amounts of the same size (use `versus-arena`), change over time (use `race-broadcast` or `line-race-editorial`), anything where area comparisons would mislead (different units, different years without adjustment).
- Honesty: areas, not lengths, carry the comparison (a square's side grows with the square root of the value, and the style says so in the description); every item shows its exact value, unit, year and currency basis; nominal and real money never mix on one ladder.

## 3. Palette
| Token | Hex | Job |
|---|---|---|
| background | #F4F2EC | bright, calm field so sizes read |
| ink | #15161A | values, names, scale chip |
| accent | #2F5BEA | the item being introduced; earlier items fall back to the support colour |
| support | #C9C4B8 | previous items, scale rulers |
| support-2 | #6F6C66 | units, sources, small labels |

Dark variant: background #0E0F13, ink #F4F2EC, support #3A3D45; same rules.

Rules: exactly one item in the accent at a time; each item keeps a thin 1 px outline in ink when it turns support colour so stacked squares stay legible.

## 4. Type
- Display: Space Grotesk (OFL) 700, 64 px at 1920×1080 for item names, tracking −0.02 em.
- Values: Space Grotesk 700, 110 px, tabular figures, with a short unit; long numbers use words for magnitude ("4.2 trillion") with the digits underneath at 28 px.
- Body / captions: Inter (OFL) 500, 26 px.
- Labels: JetBrains Mono (OFL) 500, 16 px ("× 10", "SCALE 1 SQUARE = $1B", "SOURCE").
- Language coverage: Space Grotesk, Inter and JetBrains Mono ship latin-ext on Fontsource.

## 5. Surfaces and texture
- Background: flat field with a very soft radial light (3 %) toward the current item.
- Materials: items as flat squares with 2 px corner radius (2D) or matte instanced cubes with soft studio light (3D); unit blocks (e.g. one block = $1 B) for countable comparisons.
- Texture: none or static grain 2 %; precision is the look.
- Never: perspective that distorts size (3D camera stays orthographic for comparisons), clip-art money bags, coins raining.

## 6. Framing and layout
- 16:9 (main): the current item centred at x 960, y 540 at 60 % of the frame height; name and value in a block on the right x 1340 to 1820 (or left, alternating); the scale chip top left y 80; a ruler along the bottom y 1000 showing the current unit; source y 1030.
- 9:16: item centred in y 500 to 1300; name and value under it y 1360 to 1560; scale chip y 260.
- 1:1: item in the upper 70 %, text block in the lower 30 %.
- Density: the current item, the previous one visible inside it, and at most two older items as tiny marks.

## 7. Motion
- Entrances: the new item grows from its anchor corner to full size in 1.0 s, power3.out; its name rises 20 px in 0.4 s; the value counts up in 1.2 s, power2.out.
- Pull-back: the orthographic camera's zoom drops 10× over 1.4 s, power2.inOut (log-linear, so every frame feels equally fast); the scale chip flips "× 10" over 0.3 s at the midpoint; the ruler relabels.
- Exits: items never leave; they turn support colour and stay as context.
- Holds and rhythm: 4 to 8 s per item; the biggest jump gets one extra second of hold before the value appears (let the size land first).
- Transitions: none; the ladder is one continuous shot.
- Camera: orthographic zoom only, centred on the bottom-left anchor shared by all items.
- Frame rate feel: smooth 30 fps.
- Edit grammar: the voice names the item as it grows and gives the number only after the size has landed.

## 8. Sound
- Bed: ambient, airy, 70 to 90 BPM, −28 LUFS under the voice.
- Effects: a soft rising tone during each pull-back at −24 dB; a gentle low "thunk" when a big item finishes growing.
- Mix: voice first; final −14 LUFS integrated, true peak ≤ −1 dBTP.

## 9. Build recipe and checks
- Engine and templates: HyperFrames with SVG squares for 2D, or three.js `InstancedMesh` blocks with an orthographic camera for 3D (`engines/hyperframes/three`); `stat-counter` logic for values; related reference style `cosmos-scale`.
- Signature scenes:
  - Decade pull-back: camera zooms out 10×, chip ticks, ruler relabels.
  - Block fill: one block = one unit; blocks fill row by row in 1.5 s (instanced, seeded order) for countable amounts.
  - Side by side: the two final items placed side by side on the same scale, ratio written large ("38×").
- Steps: 1) bring all values to one unit, year and currency basis; 2) sort ascending; 3) check that each step is at least 3× the previous (otherwise group them); 4) render stills at each pull-back midpoint; 5) `qa-review`.
- Style checks: area is proportional to value (measure two squares on a still); every ratio written on screen matches the data; the accent marks only the newest item.
- Common failures: lengths instead of areas (overstates differences), perspective cameras, a ladder with too many small steps (merge them), values shown before the size lands.

## Overrides
None in the library copy; project copies list their changes here.

## Credits
Original motionforge style, drawing on the general tradition of scale-comparison explainers and data journalism.
