# Visual Problems — The Last Village

Ranked most to least severe. Each entry names the concrete cause in the code, not just the symptom.

## 1. The environment is almost empty (biggest problem)
`drawBackground()` draws a flat fill plus one `rgba(255,255,255,0.03)` circle with a dashed stroke. That is the entire world art. No ground texture, no path between structures, no perimeter wall/fence, no wilderness detail outside the town circle. Because the player looks at this for the full 10-minute session, its emptiness dominates the overall impression more than any single entity does.

## 2. No object has a designed silhouette
- Town core = a plain circle with a radial gradient. Nothing marks it as a "core," "keep," or "well" — it could be a ball.
- Tower spot (built) = a bigger circle with small dots under it for level. No turret, barrel, base, or rotation toward a target.
- Forge = a flat 4-point polygon (an approximated trapezoid) with dots for level. No anvil detail, no fire/glow differentiating it from a generic purple shape.
- Player = an unshaded triangle. No cockpit/detail, no distinguishable "front" beyond rotation.
Every object is legible only by color and position, not by shape — a colorblind or first-time player has no shape-language to lean on.

## 3. Enemies are undifferentiated dots
"Fast" and "tank" enemies are both `ctx.arc()` circles distinguished only by radius (10 vs 15) and color (`#ff9f5a` vs `--danger`). There's no armor plating, no distinct body shape, nothing that visually communicates "this one is dangerous" beyond size — a new player can't tell threat level at a glance without watching the HP bar.

## 4. No lighting/depth cues
The only shading technique used anywhere is `ctx.shadowBlur` glow. There is no drop shadow under any entity, no ambient occlusion, no gradient-based "volume" on any shape except the core's radial fill. Every entity looks like a flat sticker floating at the same z-height, which is why the scene reads as "vector diagram" rather than "place."

## 5. HUD has no icon language
The HUD (`#hud`) is five plain text spans: `Gold: 60`, `Core: 150/150` + bar, `10:00`, `Weapon Lv.1`, `Best: 0:00`. There are no icons (coin, shield, clock, sword) — a player has to read words to parse state at a glance, which is slower and looks more like a debug overlay than a game HUD.

## 6. Generic system typography throughout
`font-family: 'Segoe UI', Arial, sans-serif` is used for literally every piece of text — the H1 title, HUD, overlay title, overlay body, and button. Nothing about the typography communicates "game" vs. "web page." A single distinctive display font on the title/HUD numerals would go a long way for very little effort.

## 7. Overlay screens are visually undifferentiated
Win and lose overlays reuse the exact same layout, same green title color (`#overlayTitle { color: var(--neon) }` is static CSS, not swapped per outcome), same button style. A losing screen and a winning screen should not look the same shade of "good news green" — right now `THE VILLAGE HAS FALLEN` renders in the same glowing green as `VILLAGE SAVED!`.

## 8. No idle motion anywhere
Nothing animates unless triggered by a game event. The core doesn't pulse, towers don't idle-scan, gold pickups don't bob, the forge has no ambient flicker. A completely static frame between actions reinforces the "flat/unfinished" read, especially during any lull in enemy spawns.

## 9. Bullets and enemy death have no motion trail
Bullets are static dots each frame (`ctx.arc(b.x, b.y, b.r, ...)`) with no streak/trail, so fast-moving shots can look like teleporting dots rather than traveling projectiles, especially at the 520–480px/s speeds used here.

## 10. No screen-space polish beyond the single damage vignette
The only full-screen effect is the red damage flash when the core is hit. There's no vignette/frame treatment at rest, no subtle scanline/grain/gradient overlay that a lot of neon-arcade games use to make the canvas feel like a "display" rather than a raw white/black rectangle.
