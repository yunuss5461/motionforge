goal: izleyici Fatih Sultan Mehmed'in (II. Mehmed) hayatını, İstanbul'un fethini ve 1453-1481 fetihlerini kaynaklı tarihlerle 75 saniyede kavrar
audience: Türkçe tarih/YouTube izleyicisi, genel kitle
platform + format: YouTube 16:9, 1920x1080, 30 fps, sessiz (ses ve müzik yok), Türkçe ekran metni
length: 75 s, 6 perde (hook 0-6, duvar 6-22, hazırlık 22-30, fetih 30-45, harita 45-67, kapanış 67-75)
tone + brand: belgesel, sıcak, ölçülü; koyu müze duvarı + altın vurgu; Instrument Serif / Inter / JetBrains Mono (base.css, latin-ext)

## Decisions log

| Date | Decision | Why |
|---|---|---|
| 2026-11-07 | Only confirmed rows of `docs/brain/fatih-claims.md` reach the screen | user rule; the claims file is the only fact source |
| 2026-11-07 | Left out: Amasra, Karaman/Konya, Atina, Hersek, Otranto (coordinate not verified), ship count, Topkapı year, Rumeli Hisarı duration, siege length in days, 1451 area, age at second accession | conflicting or unverified in the claims file |
| 2026-11-07 | Siege counter shows calendar dates (6 Nisan to 29 Mayıs 1453), never a day number | "53" vs "57" gün conflict; claims file says use the date range |
| 2026-11-07 | "Trabzon İmparatorluğu sona erdi" replaced by "Trabzon teslim oldu" | close to banned pattern "... sona eriyor"; surrender on 15 Ağustos 1461 is the confirmed fact |
| 2026-11-07 | Sinop and Trabzon (both 1461) appear together in one caption | no confirmed order inside 1461 |
| 2026-11-07 | Map: own Equal Earth forward formula (central meridian 30E), window 16.5-42.5E / 34.5-47.8N, land-50m projected once at load; places as translucent halos, failed sieges as dashed red rings with an X; legend "İşaretler fetih noktalarını gösterir; sınır değildir." | Codex advice (codex-a5) and claims file section 7; no historical border dataset |
| 2026-11-07 | No modern borders | optional; leaving them out keeps the map quieter |
| 2026-11-07 | Map data loaded as synchronous local scripts (`assets/vendor/land-50m.js` wraps world-atlas land-50m.json) | fetch() fails on file:// probes; data is ready before the timeline exists |
| 2026-11-07 | Camera push = SVG transform attribute on the land group; halos, labels, counters stay on unscaled layers; no CSS scale anywhere, the only will-change is on the legend (parent never scales) | determinism rules in docs/brain/decisions.md |
| 2026-11-07 | Golden Horn panel is a labelled schematic ("Şematik çizim · ölçekli değildir") | own SVG, no historical map available; avoids implying precise geography |
| 2026-11-07 | Brand-saga floor curve used as a time axis 1432-1481 (no invented data curve) | there is no sourced series to plot |
| 2026-11-07 | Style approved_by: agent (orchestrator brief) | user delegated look via brief |
| 2026-11-07 | Seek-purity fixes (bisect frames 150/1050/1800 all diffpx 0): invisible full-size `.inv` element per composited container (map rect, wall, siege, horn, act5, death, end) whose alpha alternates with frame parity so every frame fully re-rasters; hidden containers leave the layer tree (`display:none`) except the map; legend gets `will-change: opacity` (its parent never scales); current list row capped at opacity 0.99 so text never flips to LCD antialiasing; Haliç chain drawn exactly vertical on an opaque panel | own Playwright bisect: partial raster of the land path, LCD vs grayscale text and layer promotion depended on seek history |
