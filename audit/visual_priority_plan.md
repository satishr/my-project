# Visual Priority Plan — The Last Village

## Top 5 visual problems
1. Environment is almost empty — one flat fill + one translucent circle is the entire world art. (`visual_problems.md` #1)
2. No object (core, tower, forge, player) has a designed silhouette — everything is a bare circle/triangle/polygon. (#2)
3. Enemies are undifferentiated dots — "fast" vs "tank" reads only as size + color, no shape language. (#3)
4. No lighting/depth cues anywhere except glow — the whole scene sits at one flat "z-height." (#4)
5. Win and lose overlays look visually identical (same static green title color regardless of outcome). (#7)

## Top 5 quick wins
1. Drop shadow under every entity — cheapest fix for the "flat sticker" look. (`quick_wins.md` #1)
2. Fix win/lose overlay title color to actually react to outcome. (#2)
3. HUD icons (coin/heart/clock/sword glyphs) in front of each stat. (#3)
4. Idle pulse on the town core so the most-stared-at object isn't dead-still. (#4)
5. Faint paths drawn from the core to each tower/forge — turns "circle with dots" into "a settlement." (#7)

## Top 5 high-impact upgrades
1. Real silhouettes for tower/core/forge, including a barrel on built towers that visually tracks the angle they already compute mechanically. (`high_impact_upgrades.md` #1)
2. A layered ground pass (tiled town floor vs. wilderness, visible roads, boundary marker) replacing the single translucent circle. (#2)
3. Shape-coded enemies (angular/sharp for fast, heavy/plated for tank) instead of color-only differentiation. (#3)
4. Floating damage numbers + a brief scale-punch on hit — the single best "feels premium" change for combat feedback. (#5)
5. Progressive core damage state (more cracks as HP drops, flicker at critical HP, a real repair shockwave) instead of a static two-line crack. (#7)

## What should be changed first

Start with the **environment and the three structure silhouettes** (core, tower, forge) — items 1–2 in both the problems and high-impact lists. These are on screen 100% of the time, and right now they contribute almost nothing visually. Pair that with the two zero-cost overlay/HUD fixes (win/lose color, HUD icons) since they take minutes and remove an obvious "unfinished" tell. In order:

1. Drop shadows under all entities (quick win, ~15 min)
2. Fix win/lose overlay title color (quick win, ~5 min)
3. Real tower/core/forge silhouettes incl. tracking barrel (high-impact, largest single visual jump)
4. Ground/path/boundary environment pass (high-impact, second-largest jump)
5. HUD icons + idle core pulse (quick wins, fast follow-up polish)

## What can wait until later

- Shape-coded enemies and damage-number combat feedback — valuable, but lower priority than fixing the mostly-empty environment and undifferentiated structures, since those two are visible constantly while combat feedback is only visible in bursts.
- The ambient lighting gradient and canvas vignette — nice atmospheric finishing touches, best applied *after* the ground layer exists (a light pass over an empty background won't read as well as one over a textured scene).
- Title/logo branding treatment — purely cosmetic to the start screen only, lowest gameplay visibility of everything on these lists, safe to defer indefinitely without hurting the in-game experience.
