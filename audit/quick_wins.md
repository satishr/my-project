# Quick Wins — The Last Village

All of these are achievable with canvas drawing calls and CSS only — no external assets, matching the repo's no-build/no-library constraint (`CLAUDE.md`). Each is roughly a single function edit.

## 1. Add a drop shadow under every entity
Before drawing the player/enemy/tower/core, draw a flat dark ellipse (`ctx.ellipse` or a squashed circle, `rgba(0,0,0,0.35)`) slightly below and offset from each shape. This single change does more for "depth" than anything else on this list — it's the cheapest fix for the "flat sticker" problem (`visual_problems.md` #4).

## 2. Differentiate win/lose overlay color
`#overlayTitle` is hardcoded to `var(--neon)` in CSS. Set `overlayTitle.style.color` in `winGame()`/`loseGame()` (green for win, `var(--danger)` for lose) instead of leaving it static. Two lines of JS, fixes problem #7.

## 3. Add simple HUD icons via Unicode/emoji or drawn glyphs
Prefix each HUD stat with a small symbol — even a plain Unicode glyph (🪙 for gold, ❤ for core, ⏱ for timer, ⚔ for weapon) reads faster than a text label and costs one string edit per span. If emoji feel off-brand, small inline SVGs or 8x8 canvas-drawn icons work too, just more effort.

## 4. Give the core an idle pulse
In `drawCore()`, scale the radius by `1 + Math.sin(elapsedTime*2)*0.03` before drawing. A few lines; makes the core feel "alive" instead of a static painted circle, addressing problem #8 for the single most-stared-at object.

## 5. Add a bullet trail
When spawning/drawing bullets, either (a) draw a short line from the bullet's previous position to current, or (b) keep a tiny fixed-length trail array of past positions per bullet and render with decreasing alpha. Makes shots read as "traveling" instead of "teleporting dots" (problem #9).

## 6. Swap the title/HUD font for a web-safe display face
Add a `font-family` for headings/HUD numerals using something like `'Consolas', 'Courier New', monospace` for the HUD numbers (tabular, techy) and keep body text as-is, or pick a bolder system stack (`'Arial Black', sans-serif`) for the H1/overlay title only. Zero new dependencies, immediate "this was styled on purpose" signal.

## 7. Draw a path between the core and each structure
Four short faint lines (or dashed lines) from the core to each tower spot and to the forge, drawn in `drawBackground()`. Turns "circle with dots around it" into "a settlement with roads," very cheap relative to impact.

## 8. Vary particle burst size by event importance
Currently every burst uses roughly similar counts (`spawnParticles(x,y,color,14)` etc. regardless of context). Scale count/speed by significance — small burst for a hit, bigger for a kill, biggest for a tower/weapon upgrade — so feedback intensity matches the size of the event.

## 9. Add a subtle canvas vignette at rest
A large radial gradient overlay (`rgba(0,0,0,0)` center → `rgba(0,0,0,0.35)` edges) drawn once per frame after everything else, independent of the damage flash. Frames the play area and hides the harsh rectangular canvas edge — a very common cheap trick in arcade-style games.

## 10. Give the "+" build icon and dashed ring a subtle pulse
Currently a static dashed ring + static "+" glyph on unbuilt tower spots. Pulsing the ring's alpha (`0.3 + Math.sin(t*3)*0.15`) draws the eye to "this is interactive" without adding a tooltip or new UI.
