# Cline rules — 終点未着 3D制作・デバッグ

You are the implementing developer, not just a planning assistant. The active Codespace may contain uncommitted files unavailable in the remote GitHub repository. **Inspect the actual local tree before modifying any file.** Read `LastTrainUnarrived/3D_REBUILD_TASK.md` for full requirements.

1. First record the actual project tree, `git status --short`, entrypoints and game engine. Back up key files before invasive edits; do not delete or reset user work. Prefer a dedicated feature branch once local changes are safely preserved.
2. Rebuild the train interior as real 3D geometry: individually rounded red-mohair seat cushions, metal seat frames/heater vents, multi-part window frame/glass/gaskets/latches, suspended straps with straps/metal mounts, mesh racks, fluorescent ceiling casings and vents, realistic Japanese advertisements and signage. Match user reference images in local assets if present; if absent avoid inventing exact reference details.
3. Replace the **seven generic NPC placeholders** with distinct licensed/original seated GLB meshes: realistic facial proportions, eyelids, cornea/iris, ears, nose, lips, scalp, hairline and hair volumes; male/female variants, clothing folds and thickness, hands/feet, comfortable seated poses. Add idle breathing, occasional blinking and natural head motion. Reuse previously approved character references when available, never overwrite identities. Keep the two intentionally faceless supernatural characters faceless.
4. Create GLB assets in Blender via Python if Blender is available; otherwise write reproducible Blender scripts and import them when installed. Do not pretend a Blender render is a final in-game render. Separate source meshes/textures from runtime LODs.
5. Performance: measure before and after using `renderer.info.render.calls`, triangles, FPS histogram, draw resolution, GPU memory where available. Lower cost using instancing, merging, texture atlases, mipmaps, LOD and updatable quality tiers. Keep FHD screen support and report verified real FPS; no unsupported guarantees.
6. Debug the actual game, not a separate demo. Confirm: launch without errors, moving train sway, doors/collision, blackout switches emissive and real lights off, NPC visibility/pose, scene transitions, save/load. Fix faults observed and rerun checks.
7. Output evidence in `LastTrainUnarrived/QA_REPORT.md`: exact commands, screenshot paths, hardware/runtime, FPS measurements if measured, failed tests and remaining limitations. Report omitted work accurately.

Do not copy copyrighted assets from other horror games or railway operators. Preserve player privacy and any API credentials. Do not pad binary archives to achieve a size target.

When starting, **perform implementation directly**, iterate and debug, then summarize changed paths and results. No multi-hour background promises.
