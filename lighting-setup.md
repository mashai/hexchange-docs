# Lighting Setup

Audit of everything controlling how the game looks, as of the forest-environment integration pass. Covers what's actually configured right now, what's actually *in effect* (some settings are silently overridden by others), and what "properly set up" should look like given the constraint: **one quality tier, playable on most PCs.**

Scope: `Assets/Scenes/game-with-new-env.unity`, the current main scene.

## TL;DR

- URP, one render pipeline asset, one quality tier — consistent everywhere, no per-platform/per-tier drift to worry about.
- Only the sun casts real shadows. The 9 other shadow-casting-looking lights in the scene never actually cast shadows — additional light shadows are off at the pipeline level.
- Nothing is baked. Zero lightmaps, zero reflection probes. Fully realtime lighting + one skybox-derived reflection cubemap that regenerates automatically.
- Anti-aliasing is currently **off** (a fix that didn't survive a Play Mode session earlier — still needs redoing).
- Weather Maker is currently disabled while we tune the native/non-Weather-Maker look; it hooks back in later via `WeatherMakerTimeSync`.

## Render Pipeline

- **Pipeline asset**: `WeatherMakerURPProfile.asset` (Assets/WeatherMaker/Prefab/ScriptableRenderPipeline/URP/). Used as both the project-wide default (`GraphicsSettings.asset → m_CustomRenderPipeline`) *and* the single Quality Settings tier's override. Same asset in both places — nothing is silently using a different pipeline anywhere.
- **Renderer**: two Renderer Data assets exist (`WeatherMakerURPForwardRenderer.asset`, `WeatherMakerURPDeferredRenderer.asset`), but only index 0 is active by default, and the live camera confirms `actualRenderingPath: Forward`. Deferred exists but isn't in use.
- **HDR**: supported by the pipeline, and now enabled on the main `Camera` (`allowHDR: true`) — needed for Bloom and the highlight side of the color grade to have real range to work with. This was off originally; fixed.
- **MSAA**: supported by the pipeline (`m_MSAA: 1`), but the `Camera` has it off (`allowMSAA: false`).
- **Anti-aliasing**: currently **`None`** on the camera's post-process AA setting too. So right now there is zero anti-aliasing of any kind — this is a known gap, see Known Issues.

## Quality Settings

One tier, named "Standard" (`ProjectSettings/QualitySettings.asset`). This matches the "one setting most PCs can handle" goal directly — there's no tier-switching logic to maintain. The tier points at the same `WeatherMakerURPProfile.asset` as the project default, so there's exactly one place to tune performance-affecting values (shadow distance/resolution, MSAA, render scale, etc.), not several.

Worth a look before finalizing: **Shadow Distance is `8192`**, tuned for Weather Maker's demo-scale scenes. That's a large draw distance for shadow rendering and may be more than this scene's actual play area needs — worth dialing back if we want the lightest possible load for "most PCs."

## Shadows

- **Main Light Shadows**: on. Resolution 2048, 4 cascades (splits at 0.25 / 0.1,0.3 / 0.067,0.2,0.467), shadow distance 8192, depth bias 1, normal bias 1. This is the *only* light casting real shadows right now.
- **Additional Light Shadows**: **off** at the pipeline level (`m_AdditionalLightShadowsSupported: 0`). There are 7 Spot Lights and 2 Point Lights in the scene, each individually configured with Soft Shadows + Strength 1 — but none of that matters, because the pipeline setting overrides all of them. They're not casting shadows no matter what their own Inspector says. (Correction to something I said earlier in this pass — I'd flagged these as a possible second source of harsh shadows before checking the pipeline asset; they're not, since they can't cast shadows at all right now.)
- **Soft Shadow Quality**: the pipeline default is `2` = **High**. The `Sun Source` light's own Inspector shows "Soft Shadows Quality: Low", but that field is inert — the light has "Use Pipeline Settings" checked, so the pipeline's High value is what's actually used at runtime, not the dropdown's displayed Low. Don't be misled by that field.
- **Shadow Strength** on `Sun Source`: `0.873` — this one *is* real and per-light, and is the actual lever for how dark/harsh the sun's shadows read. This is the one still open for tuning (see conversation — proposed dropping to ~0.5–0.6, not yet applied).

## Global Illumination / Baked Lighting

**Nothing is baked.** Confirmed from the actual `LightingSettings` asset the scene references (`Assets/CheckoutFrenzy/Scenes/GameSettings.lighting`, shared with stock CheckoutFrenzy):
```
m_EnableBakedLightmaps: 0
m_EnableRealtimeLightmaps: 0
m_RealtimeEnvironmentLighting: 1
```
Fully realtime lighting, no lightmaps of any kind. This matches the warning visible in the `Sun Source` light's Inspector ("Light mode is currently overridden to Realtime mode"). Its Mode dropdown says "Mixed," but that's cosmetic — with baking disabled, it behaves as pure Realtime regardless.

This is consistent with the "one quality tier, most PCs" goal — no bake step to maintain, no lightmap memory/storage cost — but it does mean all indirect/bounce lighting comes from the ambient probe (below), not from any baked GI.

## Reflections

Zero `ReflectionProbe` components in the scene. `Default Reflection Mode` is Skybox (`m_DefaultReflectionMode: 0`) — Unity auto-generates one global reflection cubemap from whatever the RenderSettings skybox material is, and re-bakes it automatically when that material changes. The `ReflectionProbe-0.exr` file sitting in the scene's data folder is that auto-generated cubemap, not a placed probe. No probe placement/maintenance needed unless we later want localized reflections (e.g. inside a building interior).

## Ambient Lighting

`RenderSettings.ambientMode` = Gradient (Trilight): separate Sky / Equator / Ground colors rather than one flat color or a skybox-sampled probe.

- Current values: Sky `(89, 117, 171)`, Equator `(73, 102, 120)`, Ground `(117, 173, 161)` (0–255), Ambient Intensity `0.77`.
- **Caveat**: the "Ambient Intensity" multiplier only does anything when Ambient Mode is Skybox (per Unity's own docs). In Gradient mode it's inert — the `0.77` currently set has no visual effect. If we want the equivalent dimming, it has to be baked directly into the three colors' RGB values, not left as a separate multiplier.
- Each Gradient color is an HDR color field with its own "Intensity" (exposure) slider stored in the color's alpha channel — this one *is* real, unlike the multiplier above. Leave it at neutral/0 and enter exact RGB values directly rather than using the slider, to avoid accidentally scaling the color (this bit me once already this session — the slider is an exposure-stop control, not a 0–1 multiplier, and "1" means "brighter," not "unscaled").

## Fog

`RenderSettings` native fog (not Weather Maker's fog system, which is currently parked — see below):
- Mode: Exponential Squared
- Color: `(50, 141, 173)` (0–255) — a saturated teal
- Density: `0.01` (lowered from an initial `0.025`, which read as too hazy)

## Post-Processing

One `Global Volume Profile.asset` (Assets/Fantastic Ancient Forest/Settings/), shared identically between this scene and the original demo scene — not a separate/weaker copy. It was configured correctly all along; it just wasn't rendering, because `Render Post Processing` was off on the camera (now fixed).

What's actually in the profile:
| Effect | Active | Key values |
|---|---|---|
| Channel Mixer | yes | Red crushed to 54%, Blue boosted to 113.7% — baseline teal-leaning grade |
| Bloom | yes | Intensity 2, threshold 0.34, warm tint |
| Vignette | yes | Intensity 0.222, smoothness 0.553 |
| Color Adjustments | yes | Post-exposure -1.3, contrast +5 (hue/saturation/color filter overrides are present but switched off) |
| Split Toning | yes | Shadows teal `(0.30, 0.55, 0.69)`, Highlights warm gold `(1.0, 0.97, 0.67)` — the signature "cool shadow / warm highlight" look |
| Lift/Gamma/Gain | yes | Shadows/mids pushed blue, highlights pushed warm (reinforces Split Toning) |
| Depth of Field | **no** | Present but disabled (`active: 0`) |

Important interaction: Split Toning's warm half and Bloom both need real bright highlights in the base (pre-grade) image to do anything. If the underlying lit scene is flat (no real light/shadow contrast, no HDR headroom), only the cool/teal half of every one of these effects has anything to act on — which is exactly why the scene read as a uniform teal "underwater" wash before HDR was enabled. With HDR on and post-processing actually rendering, the warm side should now have something to grab onto.

## Weather Maker

Currently **disabled** (`WeatherMakerPrefab` GameObject inactive) while we get the native/non-Weather-Maker look right first. When re-enabled:
- `WeatherMakerTimeSync` (Assets/Hexchange/Scripts/Gameplay/) pushes `TimeManager.TotalMinutes` into Weather Maker's `DayNightCycle.TimeOfDay` every frame and zeroes Weather Maker's own clock (`Speed`/`NightSpeed`), so `TimeManager` stays the single source of truth for game time.
- `TimeManager` itself checks `Hexchange.DebugSettings.Instance.DisableStockDayNightVisuals` to decide whether to run its own sun-rotation/fog-color code — currently `true` (on), so it's not fighting Weather Maker or the manual RenderSettings work.
- `Hexchange.DebugSettings.Instance.DisableSunShadows` (also `true`) tells `WeatherMakerTimeSync` to strip shadow-casting off Weather Maker's own sun light once it's active.

## Known Issues / Not Yet Done

- ~~**Anti-aliasing** was set to SMAA once via MCP, but that change happened while the Editor was in Play Mode and was silently discarded on Stop.~~ Fixed — reapplied in Edit mode and confirmed persisted (`m_Antialiasing: SubpixelMorphologicalAntiAliasing`).
- ~~**Shadow Strength** on `Sun Source` (`0.873`) and its perceived harshness.~~ Lowered to `0.55`.
- **RenderSettings edits made via direct file edit have reverted unexplained at least twice** this pass (fog/ambient/skybox/sun fields specifically) — root cause not fully understood; current best theory is Play Mode's snapshot-restore-on-Stop interacting badly with changes that bypassed Unity's own dirty-tracking (i.e., edits made by writing the `.unity` YAML directly rather than through the Editor). Since switching to doing these edits through the Lighting window UI directly, they've held. **Recommendation: keep doing RenderSettings changes through the Editor UI (or MCP Unity where it can reach the field, which it currently cannot for RenderSettings), not via direct scene-file edits, until this is root-caused.**
- ~~**Shadow Distance (`8192`) and cascade count (`4`)** hadn't been reviewed against actual performance targets.~~ Lowered to `150` distance / `2` cascades as a starting point — was inherited from Weather Maker's open-world demo defaults, not sized for this game's bounded play area. This was a guess at a reasonable starting value, not measured against the actual play area size — revisit if distant geometry starts losing shadows too early, or push it down further if there's still headroom. This edit was made directly to the `WeatherMakerURPProfile.asset` file (a plain project asset, not scene data), which doesn't have the same revert risk as the RenderSettings scene edits above.

## What "Properly Set Up" Looks Like (Target Checklist)

Given the one-tier, broad-compatibility goal:

- [x] One render pipeline asset, used consistently as both project default and the single quality tier.
- [x] One quality tier (already true — nothing to change here).
- [x] HDR on (needed for Bloom/grading to work at all).
- [x] Anti-aliasing on (SMAA — the cheap, safe choice, doesn't require MSAA or TAA's extra cost/setup).
- [x] Post-processing actually rendering (was silently off; fixed).
- [x] No baked lighting to maintain (already true, consistent with the "no bake step" simplicity goal) — as long as we're comfortable with fully-realtime ambient/indirect quality, which for a stylized cozy-dark game is probably fine.
- [x] No reflection probes to place/maintain — the auto skybox-derived cubemap is enough unless a specific interior needs localized reflections later.
- [x] Shadow Distance/cascades right-sized (150 / 2, down from 8192 / 4) — a starting guess, not measured; revisit if it under- or over-shoots.
- [x] Sun shadow strength lowered (`0.873` → `0.55`) — a first pass, not exhaustively tuned; revisit to taste once you've seen it in-game.
- [ ] Weather Maker re-enabled once the native look is locked in, with its own Sky/Fog/DayNightCycle profiles matched to this same target look (Step 2 of the original two-step plan).
