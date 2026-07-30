# High-Impact Upgrades — The Last Village

These take more effort than the quick wins but would move the project from "readable prototype" to "looks intentionally designed." Still achievable with canvas primitives only — no external art pipeline required, in keeping with the project's single-file/no-asset constraint.

## 1. Design real silhouettes for the three interactive structures
Instead of circle-with-dots (tower) and generic-trapezoid (forge), build each from 3–5 layered canvas primitives so they read as *objects*, not shapes:
- **Tower**: a base ring + a raised turret body + a barrel drawn along the current aim-toward-nearest-enemy angle (towers already compute a target each cooldown — reuse that angle to visually rotate the barrel). This alone would make towers feel like they're actually aiming/tracking, which they mechanically already do but currently never show.
- **Town core**: layer 2–3 concentric shapes (outer stone/metal ring behind the glowing orb) so it reads as a "structure housing a core" rather than a bare glowing ball.
- **Forge**: keep the anvil base but add a small flame/glow shape on top (a simple teardrop gradient) that intensifies with weapon level, giving the forge a distinct "in-use" identity from the tower/core.

## 2. Build a real ground layer instead of one translucent circle
Replace the single dashed circle in `drawBackground()` with a layered environment pass:
- A subtly-tiled ground pattern inside the town radius (alternating slightly-different-shade tiles or a faint grid) vs. a darker/desaturated "wilderness" outside it.
- Visible paths connecting core → each tower → forge (see quick win #7, but rendered as a textured strip rather than a thin line — e.g., two parallel dashed lines forming a road).
- A perimeter marker (broken fence posts, a low wall arc, or corner watch-fires) at the town boundary so "enemies coming from outside" has a visual line to cross, reinforcing the core fantasy (defending a boundary) instead of just a math radius.

## 3. Type-differentiate enemies by shape, not just color/size
Give the "fast" enemy a sharper, angular silhouette (e.g., a triangle/arrow shape pointing toward its direction of travel) and the "tank" enemy a heavier, rounded/plated silhouette (e.g., an octagon or a circle with a darker inset ring suggesting armor). Shape-coding threat type is both a legibility upgrade (colorblind-safe) and a polish upgrade (stops every enemy from reading as "a dot").

## 4. Layered lighting pass
Add one soft ambient radial gradient centered on the town core across the whole canvas (very low intensity, e.g. `rgba(57,255,136,0.04)` falling off to nothing at the edges) so the core visually "lights" the settlement. Combine with the drop-shadow quick win and this alone would take the scene from "flat cutouts on black" to "a lit place at night," which fits the neon-arcade direction already implied by the palette.

## 5. Escalating combat feedback (damage numbers + hit-reaction)
Add small floating damage-number text on enemy hits (short-lived, drifts upward, fades) and a brief scale-punch (`entity radius *= 1.15` for ~0.1s) on the struck enemy. This is the single highest-leverage "feels premium" change for moment-to-moment combat — right now a hit only shows a 4-particle puff, which under-communicates impact compared to almost any commercial shooter/tower-defense game.

## 6. A designed title/branding treatment
Replace the plain gradient-text `<h1>` with a small canvas- or SVG-drawn logo/crest (e.g., a simple banner or shield shape behind the wordmark) shown on the start overlay only, reusing the same neon palette. Doesn't need external assets — a hand-drawn SVG shield with the existing gradient as its fill would read as "someone designed a logo" rather than "browser default heading styled with CSS."

## 7. State-reactive core visuals beyond color swap
Currently the core only changes fill color and gets two static crack lines below 50% HP. Make damage progressive and visible: more/longer cracks as HP drops further, a flickering/unstable glow at critical HP (<15%), and a brief "repaired" shockwave ring animation on `tryRepairCore()` success (larger and slower than the existing generic success ring) so repairing feels like meaningfully restoring the core rather than a generic click-confirm.
