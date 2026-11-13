# 終点未着 / LastTrainUnarrived — repository instructions

This repository contains or is developed alongside a Japanese first-person psychological horror game, **終点未着 (LastTrainUnarrived)**. The active Codespaces workspace may contain **uncommitted game files** under `LastTrainUnarrived/` even when they are not yet on GitHub. Inspect files before making changes. **Never overwrite existing game data blindly**.

## Goal
Implement improvements, not just offer plans. Read `LastTrainUnarrived/3D_REBUILD_TASK.md` first. Main priority: photorealism-leaning Japanese train interior (seat cushions, windows, straps, luggage rack, ceiling, advertisements), then distinctly sculpted seated passenger 3D models with realistic faces and clothing. Aim to remove the old placeholder-looking models while preserving the horror story and interaction.

## Mandatory constraints
- Preserve the original six chapters, save format, controls, event triggers, blackout behavior, doors/collision and existing characters. Check paths, globals, and file loading before editing; do not replace the whole `index.html` with a demo.
- Original cast: 雨宮紗良 (female, 27), 数える乗客 (intentionally faceless), 車窓の女 (female apparition), 忘れ物係 (intentionally faceless), 赤い傘の子, 水底の車掌. Keep character identities consistent with available reference assets.
- Existing `主人公.png` and `SK_WindowWoman.glb` must not be deleted or silently replaced. Inspect provenance and use only assets allowed by their licenses. The user's Humano asset must **not** be committed or repackaged unless redistribution rights are verified.
- FPS currently reported ~20 on user's PC; profile first. Prefer instancing, shared geometry/materials, LOD, frustum culling, asynchronous asset loading, limited dynamic lights/shadows, optional render scale and economical postprocessing. Target 1080p at 60FPS in Performance/Auto mode on a capable GPU, **measure and report**, don't promise fixed FPS.
- Use Three.js/GLTFLoader for GLB integration if already present. For new meshes, prefer quality meshes exported as GLB from Blender with PBR textures, not flat planes or hundreds of independent draw calls.
- The requested ~1GB package size is a *quality budget*, not a quota. Do not add dummy/duplicated/unreferenced files to inflate it; GitHub blocks >100MB single files without external/LFS handling. Do not expose secrets/API keys.
- Test syntax/build, run game, inspect console errors, and verify a normal chapter, a station exit, blackout, save/load, and character visibility. Write actual results to QA notes; distinguish tests run from those not run.

**Start with a brief inventory** (`pwd`, `git status`, `find`, package scripts, existing models) and then make code/asset changes, debug, and commit reviewable changes. Never claim a feature is complete without a reproducible check.
