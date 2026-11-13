# 終点未着 — 実装タスク / 3D realism + performance

## 0. Before coding / current state
User wants THIS existing game upgraded in the Codespaces workspace (`my-first-app/LastTrainUnarrived`). Source files may exist **only in the Codespace's local working tree** (the remote GitHub main currently has only its initial README). Do NOT overwrite the project, assume that the code is already committed, or turn it into a new blank game.

First:
```sh
pwd
git status --short
find LastTrainUnarrived -maxdepth 3 -type f | head -100
find . -maxdepth 2 \( -name package.json -o -name '*.html' -o -name '*.glb' -o -name '*.js' \) -print | head -100
```
Inspect the real project entrypoint, scenes, render loop, existing meshes, collision, door states, characters and quality settings. Establish a safe backup/feature branch without resetting local changes. Read instructions before proceeding. Existing characters, saves, story (six chapters) and stage logic must survive.

## 1. Train interior — highest priority
Realistic Japanese older commuter train, based on reference photos supplied by the user. Avoid generic low-poly cubes. Build with Blender meshes exported to GLB, or implement geometries correctly in Three.js if a modelling app is not available.

- **Seat / 座席:** red textile moquette, ~7-seat benches with independent contoured cushions and rounded/back-supported corners, seam piping and believable creases, side rails, heater grilles, metal feet. PBR fabric basecolor/normal/roughness. Avoid existing overlaid/duplicated old-seat geometry.
- **Window / 窓:** thick frames and depth, upper/lower opening panes where applicable, rubber seal, metal sliding latches, realistic transparent tinted glass, subtle night reflections and condensation. Reflections disappear or change appropriately during blackout.
- **Straps / つり革:** each ring, strap fabric and upper metal clamp in solid geometry with realistic size and spacing. Pendulum/secondary movement follows acceleration/braking; limit per-frame updates with shared poses or GPU instancing.
- **Luggage rack / 網棚:** metal border, cross-wire mesh, bracket joints and shadow; avoid one mesh/draw per wire when batching is possible.
- **Ceiling / 天井:** fluorescent/LED housings with diffuser cover, seams, vents, fasteners, signage rails. Blackout must turn off both real lights and emissive materials (no residual glowing fluorescent tubes); emergency lamps only when narratively intended.
- **Advertisements / 広告:** varied fictional Japanese adverts, appropriate paper curl/placement in ad holders, low-cost textures. Preserve image copyrights and do not duplicate actual commercial content.

Add reasonable collision shapes only where needed, with sliding and no clipping through seats/doors; avoid collisions for purely decorative bolts/screws. Maintain train scale (doors, seating eye height, aisle width, poles) and camera sight lines.

## 2. Characters — next priority
Create **seven distinct everyday seated passengers**, not repeated gender-swapped mannequins. Profiles should differ naturally in age, skull geometry, posture, hairstyle, clothing, accessories and build; avoid stereotypes and exaggerated sex characteristics. Focus on:
- Facial mesh: forehead, brow ridge, eye socket, separate eyes with sclera/cornea/iris, eyelids/eyelashes, nose bridge/nostrils, ears, jaw, lips, cheeks, subtle facial asymmetry.
- Hair meshes: scalp, hairline, clear silhouette and clumps/strands suitable for real-time rendering.
- Body: shoulders, chest, waist, legs, knees, hands with fingers, feet, proper arm/leg joints, clothes with thickness and wrinkles. Natural seated posture and bench contact.
- At least 2-3 LOD tiers per unique mesh, optional 4K/2K/1K texture tiers, use PBR color/normal/roughness and correct material color space. No 4K face textures for distant NPCs.
- Animation: occasional blinks, subtle breathing, eyes shifting, realistic head turns; supernatural action only at established event triggers.
- Reference characters: 雨宮紗良 (27yo female protagonist), 数える乗客 (intentional no face), 車窓の女 (female, appears in/reflected at windows), 忘れ物係 (intentional no face), 赤い傘の子 (small figure), 水底の車掌 (male conductor). Preserve existing illustrated design IDs/asset names, positions and story semantics.
- The user shared a `Humano_01BusinessOffice_01_Rhino.zip` male model: it may be useful for PRIVATE reference, but do not republish its contents in the public repository or distributed game without verifying license/redistribution rights. Create new original/licensed models instead.

## 3. FPS and memory: mandatory, not optional
The player reports **~20 FPS** in Windows fullscreen. Before changing code, record baseline FPS, resolution, draw calls, triangles, and texture load. Determine whether the GPU bottleneck stems from pixel ratio, shadows, postprocessing, too many lights, textures or draw calls. On a compatible PC target usable fullscreen FHD at 60 FPS; optional 90/120 only when measured sustainable.

- Instancing and batching repeated screws, wires, handles, bolts and static scenery.
- LOD/frustum culling, reducing shadows to essential light sources, baking lights when feasible, selective material complexity, mipmapping, texture atlases, efficient shader count and optional SSAO/bloom.
- Cap GPU memory usage sensibly; do NOT load all 1GB of assets at startup. Quality presets (Performance/Auto/High/Ultra) must actually swap assets and pixel ratio.
- Benchmark with measurable diagnostics (e.g. `renderer.info.render.calls`, triangles, min/avg/1% low FPS). Document hardware; do not claim improvement without measurements.
- File size itself is NOT the goal: user allows 1GB to improve visual quality. Avoid meaningless duplicate data to hit a number.

## 4. Train movement and horror atmosphere
Keep event pacing deliberate, Japanese everyday ambience rather than constant jump scares. Add slight acceleration/deceleration inertia, track-joint rhythm, subtle movement of straps, controlled ambient station announcements, and night scenery/parallax; retain stable and accessible camera controls. Ensure sound levels not overwhelming.

## 5. Test matrix / acceptance criteria
Run actual game, not just static syntax checks; inspect errors in terminal and browser/Electron devtools:
1. Normal car renders seats, windows, straps, racks, ceiling and varied adverts with correct scale, shadows/materials.
2. NPCs have visible faces and distinct silhouettes/poses; intentional faceless anomalies retain their character.
3. Power outage: all fluorescent light sources AND emissive covers go dark; if emergency lights appear, they are distinct and dim.
4. Walking, collision and train/platform doorway transition work without clipping.
5. Save/load; start and complete as many of six story chapters as environment allows; no regressions.
6. FHD screenshots / FPS and draw call report before/after on the test device, plus Performance/Auto/High comparison.
7. `npm run build` or existing Windows build script works if present; no new copyrighted resources or API credentials.
8. GLBs load without broken references; asset streaming/fallback when local files missing.

## 6. Deliverables (real files, not promises)
- Game changes in its existing sources plus original meshes/textures under an appropriate assets folder; Blender scripts or .blend if available and licensing allows.
- A `QA_REPORT.md` with reproducer, changed files, test commands and output, frame statistics with machine details, screenshots, known gaps.
- Clear game launch instructions. Avoid 1GB GitHub individual-file upload limits; use Git LFS or release assets only with explicit setup/permission. Do not commit private/third-party uploads into a public repo.
- Short final summary distinguishing **implemented**, **tested**, **not tested**. No invented outcomes.

IMPORTANT: Begin implementation after inspecting this task. The user's approval for debugging is already given. Do not repeatedly ask for confirmation for ordinary safe code and asset changes; do not wipe uncommitted files.
