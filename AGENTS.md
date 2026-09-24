# Agent Instructions — LayerSample (Unreal Compositor Layer Sample)

Unreal Engine sample illustrating how to render UMG widgets via VR compositor layers (Unreal's `StereoLayer` API) instead of the main pass, including non-quad layer shapes.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup and editor options (Epic Launcher + MetaXR plugin, or Meta fork of UE)
- `LayerSample.uproject` — Unreal engine version and plugins
- `Content/Blueprints/` — `MenuActor`, `Menu`, `Menu_CompositorLayer`, `SimpleCompositorLayerActor`, `LayerGameMode`, `VRCharacter`
- `LICENSE` — license terms

## Quest / Horizon-specific notes

- Git LFS is **required**. Run `git lfs install` before cloning.
- Project is **blueprint-only** — no `Source/` folder, no Visual Studio project to generate, no C++ to compile.
- The OculusXR (MetaXR) plugin must be installed via the Epic Marketplace integration or the Meta fork of UE; opening the project without it will fail to load `OculusXR`.
- Educational core: when a widget renders to a stereo layer, **disable its in-scene rendering** (see `OnToggleClicked_Event` on `MenuActor`) to avoid double-drawing.
- `EngineAssociation` in `.uproject` is not pinned to a specific 5.x — UE5 with a compatible MetaXR plugin should open it, but plugin/engine version mismatches are a common foot-gun.

# Meta Quest tooling

This is a Meta Quest / Horizon OS sample. The bespoke intro above is the source of truth for what this project is and how it's built — use it (and the files it points at) instead of restating facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Unreal answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Unreal-specific skills: <https://github.com/meta-quest/agentic-tools>. Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
