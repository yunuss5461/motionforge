<!-- motionforge style · © 2026 motionforge contributors, MIT -->
# Brand Saga

> One brand's whole life on a long gallery wall: the camera dollies along a timeline, each era is a chapter with its product, its logo of the time and one defining moment, while a sales curve draws itself along the floor of the frame.

| Category | Engine | Best for | Effort |
|---|---|---|---|
| Data rankings & races | hyperframes + three.js (wall and dolly) or hyperframes 2.5D (parallax layers) | single-brand histories, "the rise and fall of", company documentaries, anniversary films | high |

## 1. Essence
- In one sentence: a museum walk through a brand's history where the numbers and the story move together.
- Three adjectives: documentary, warm, sweeping.
- Signature move: the floor curve. A sales line runs along the bottom of the frame for the whole video and draws itself under the camera as it travels, so every chapter sits on top of the data it explains.

## 2. Use it for / avoid it for
- Use for: one brand or company over 30 to 150 years; 3 to 8 chapters; 16:9 long-form of 3 to 15 minutes, Shorts as single-chapter cut-downs.
- Avoid for: comparisons between brands (use `race-broadcast` or `versus-arena`), brands without a documented history (the style promises real dates), anything without permission to show real logos and products.
- Honesty: every date and figure on the wall has a source in the claim list; historical logos and product photos are the owner's assets used with permission or under a clear licence, listed in `assets/CREDITS.md`; reconstructed or approximate figures are labelled "estimated".

## 3. Palette
| Token | Hex | Job |
|---|---|---|
| background | #F1ECE3 | gallery wall (light) |
| ink | #1D1B18 | titles, dates, body |
| accent | #B8432F | the floor curve, the current-chapter marker, key dates; replaced by the brand's primary colour when a brand kit exists |
| support | #8A8378 | captions, minor dates, frame edges |
| support-2 | #DDD5C8 | chapter dividers, plinths, the timeline rail |

Dark variant for brands with dark identities: background #15130F, ink #F1ECE3, support-2 #2A2620; same rules.

Rules: the accent appears only on the floor curve, the active marker and at most one key date per chapter; product photos sit on neutral plinths, never on accent fills.

## 4. Type
- Display: Fraunces (OFL) 600, chapter titles 88 px at 1920×1080, tracking −0.02 em, with optical sizing; years as chapter numerals in Fraunces 300 at 220 px, support colour.
- Body / captions: Inter (OFL) 500, 26 px, line height 1.4, at most 2 lines per caption.
- Labels: IBM Plex Mono (OFL) 500, 16 px, uppercase, +0.12 em (dates on the rail, "SOURCE", "ESTIMATED").
- Language coverage: Fraunces, Inter and IBM Plex Mono ship latin-ext on Fontsource.

## 5. Surfaces and texture
- Background: a matte plaster wall with a soft top light; each chapter has a 1600 px wide panel with a slightly different wall tint (±3 % lightness) so chapters read as rooms.
- Materials: framed items (photo, logo, ad) with 18 px off-white mats and 2 px dark frames; products on 40 px plinths with a soft contact shadow.
- Texture: static paper grain 4 %; old photographs keep their own grain, never add fake scratches.
- Never: torn-paper transitions, sepia filters on modern material, fake aged stains, invented archival images.

## 6. Framing and layout
- 16:9 (main): wall content between y 120 and 820; floor curve band y 860 to 980 (the full history drawn to the camera position, the future dashed at 30 %); timeline rail with dates y 1000; chapter title top left y 120 to 230; captions under the framed item, max width 620 px.
- 9:16: the wall scrolls vertically instead of horizontally; chapter title y 260 to 420, framed item y 480 to 1180, caption y 1220 to 1340, floor curve becomes a side curve on the left x 60 to 160 running top to bottom.
- 1:1: one framed item and its caption per chapter, curve band at the bottom 180 px.
- Density: one chapter in focus; the neighbouring chapters visible at the frame edges at 50 % as context.

## 7. Motion
- Entrances: the camera dollies to each chapter (three.js) or the parallax layers slide (wall 1.0×, frames 1.15×, plinths 1.3×) over 1.6 s, power2.inOut; the chapter numeral fades up 0.6 s; the title rises out of a mask 0.5 s; framed items settle with a 6 px drop and a 0.3 s shadow tighten.
- Floor curve: draws continuously with the camera; at a chapter's key year a 10 px accent dot pops with a 0.35 s back.out and a thin rule rises to the framed item above it.
- Holds and rhythm: 15 to 45 s per chapter in long form; inside a chapter a 1 % slow push keeps the frame alive; a new caption every 6 to 10 s.
- Transitions: the dolly; between distant eras a 0.5 s dip to the wall colour with the next year numeral in its place.
- Camera: horizontal dolly at constant height; no rotation; a 3 % push on the defining moment of each chapter.
- Frame rate feel: smooth 30 fps.
- Edit grammar: chapter cards land on section turns in the narration; archival footage, when licensed, plays inside a frame on the wall, never full screen.

## 8. Sound
- Bed: warm documentary score, piano or strings, 70 to 90 BPM, −28 LUFS under the voice; a change of instrumentation per era is welcome.
- Effects: soft footsteps or room tone during dollies at −32 dB; no whooshes.
- Mix: voice first; final −14 LUFS integrated, true peak ≤ −1 dBTP.

## 9. Build recipe and checks
- Engine and templates: `templates/kinetic-title` for chapter titles, `templates/cover-still` for the thumbnail; HyperFrames + three.js (`lights.daylight` at low intensity, `shadowCatcher`) for the wall and plinths, or a flat parallax build; `timeline-chronicle` and `archival-newsreel` styles are related references; the brand kit supplies logos and colours.
- Signature scenes:
  - Chapter arrival: dolly, numeral, title, framed item settles, curve dot pops.
  - Defining moment: the camera pushes 3 % into one frame, the caption types on, the curve segment for that year thickens to 4 px for 2 s.
  - Then and now: two framed products side by side on one plinth, the old one sliding aside as the new one rises.
  - Closing walk: the camera pulls back to show the whole wall and the complete curve in one frame, held 3 s.
- Steps: 1) build the chapter list with dates, figures and sources; 2) collect licensed assets per chapter; 3) lay out the wall as a 2D plan first; 4) render one still per chapter; 5) `qa-review`.
- Style checks: every framed item has a credit line in `assets/CREDITS.md`; the curve's peaks line up with the chapters that discuss them; captions stay under two lines; no chapter is shorter than 10 s.
- Common failures: walls crowded with items, a curve without a y-axis reference (add a quiet scale label at the start), dollies so frequent the viewer never settles.

## Overrides
None in the library copy; project copies list their changes here.

## Credits
Original motionforge style, drawing on the general tradition of museum exhibitions and documentary timelines. No real brand assets are included in the library.
