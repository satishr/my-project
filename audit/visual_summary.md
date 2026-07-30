# Visual Summary — The Last Village

Note: rendered from direct code review (canvas drawing calls, CSS, DOM structure), not a live screenshot — the preview pane wasn't visible for capture during this pass. Every shape, color, and effect described below is read directly from `town-defense.html`.

## 1. Overall visual impression

**It reads as a functional prototype, not a finished game.** Every entity on screen is a flat-filled primitive (circle, triangle, or 4-point polygon) with a colored glow — no sprites, no texture, no linework beyond a couple of straight "crack" lines on the core. That's the single biggest tell of "programmer art": nothing is drawn, everything is `ctx.arc()` or `ctx.moveTo/lineTo`.

**What already looks good:**
- The color palette itself is genuinely solid — a consistent neon-on-near-black scheme (green/cyan/purple/gold/pink-red) that reads as "arcade/cyber" and doesn't clash. This is the strongest asset in the project right now.
- Glow (`shadowBlur`) on every entity gives a baseline sense of energy/life that a plain flat-fill game wouldn't have.
- The HUD → canvas → overlay layering and the win/lose copy are clean and understandable.

**What makes it feel cheap:**
- Every game object is a bare geometric primitive with no silhouette design — the player is a triangle, enemies are dots, the town core is a glowing circle, towers are circles-with-dots, the forge is an unstyled trapezoid. None of these read as "a thing" without a label.
- The background is 95% empty flat color. There's a single translucent circle with a dashed outline to mark "town area" — no ground texture, no path, no buildings, no trees, no rubble, nothing that says "village."
- HUD text is plain browser system font in a single unstyled row — no icons, no per-item card treatment, functional but generic.

**Fix first:** the background/environment (currently near-blank) and the core/tower/forge silhouettes (currently undifferentiated circles). These are what the player looks at 100% of the time, and they carry zero "place" or "object" identity right now.

## 2. Art style

There isn't yet a defined *art* style — there's a defined *color* style. Right now "style" = one palette applied uniformly to circles and lines. That's consistent (nothing clashes), but consistency of color isn't the same as a visual identity. A geometric/vector neon style (think glowing wireframe outlines, hex/hard-edge shapes, layered glow) would fit what's already there and could be reached without adding real art assets — see `high_impact_upgrades.md`.

## 3. Color and lighting

- Palette is attractive and consistent (`--neon #39ff88`, `--tower #00e5ff`, `--forge #b98bff`, `--gold/--accent #ffd23f`, `--danger #ff3b6b` on `--bg #0a0e17`).
- Contrast is fine for gameplay reading (enemies vs. background, bullets vs. background) but weak for *depth* — nothing is layered, so the scene reads as flat cutouts floating on a black plane rather than a lit space.
- Only one shading technique is used anywhere: `shadowBlur` glow. There's no directional light, no ambient occlusion/shadow under entities, no vignette except the reactive damage-flash. Everything sits at the same visual "elevation."
- Core, towers, and player are visually separated from the background by color alone (bright vs. black) — this works, but a subtle ground shadow under each entity would sell "on a surface" instead of "floating."

## 4. UI quality

- HUD: one unstyled flex row of plain text spans (`Gold: 60 · Core: 150/150 [bar] · 10:00 · Weapon Lv.1 · Best: 0:00`). Functional, readable, but no icons, no per-stat visual grouping, no card/chip styling beyond the single translucent wrapper.
- Overlay (start/win/lose): centered title + paragraph + one gradient pill button on a dark scrim — clean but generic, no border treatment, no icon/crest, no distinct win vs. lose visual identity beyond text color implied by title only (title color is hardcoded green in CSS regardless of win/lose state).
- Typography: system font stack (`Segoe UI, Arial, sans-serif`) everywhere — no distinctive display font for the title/HUD, which is a large part of why it reads generic rather than "branded."
- Spacing/layout is clean and uncluttered — this is a genuine positive, nothing overlaps or feels cramped.

## 5. Animation and visual feedback

- Existing feedback: particle bursts on hit/kill/upgrade, a colored ring pulse (success/insufficient/max-level) on clicked objects, screen shake + red vignette on core damage, procedural WebAudio beeps.
- This is a reasonable *skeleton* of juice, but every effect is minimal-duration and single-layer (one burst, one ring, one shake value) — nothing chains or escalates (e.g., no bigger burst for a tank kill vs. a fast kill, no camera punch on tower build, no core "flinch" scale-pop on repair).
- No idle/ambient animation on anything — the core doesn't pulse, towers don't have a scanning/idle rotation, the forge has no ambient flicker. Everything is dead-still until an event fires, which reinforces the "flat cutout" feeling.

## 6. Backgrounds and environment

This is the weakest area. The entire environment is: a flat fill color + one large low-opacity circle with a dashed ring to denote the town boundary. There is no:
- ground texture or tiling (dirt, grass, cobblestone)
- path/road connecting core → towers → forge
- perimeter/wall silhouette separating "village" from "wilderness" enemies spawn from
- decorative clutter (rubble, campfires, banners, crates) to break up empty space

The world currently feels like a settings diagram, not a village. This is the single highest-leverage place to invest polish, because it's visible for 100% of play time and currently contributes almost nothing.

## 7. Top-line priority

See `visual_priority_plan.md` for the ranked list — in short: **environment art and object silhouettes first**, **UI/typography second**, **animation layering third**. Full breakdowns are in the companion files:
- [`visual_problems.md`](visual_problems.md)
- [`quick_wins.md`](quick_wins.md)
- [`high_impact_upgrades.md`](high_impact_upgrades.md)
- [`visual_priority_plan.md`](visual_priority_plan.md)
