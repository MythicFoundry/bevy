# Mordlite downstream Bevy maintenance

Created (UTC): 2026-11-09T18:40:22.299Z
Updated (UTC): 2026-11-09T18:40:22.299Z

This branch starts at upstream Bevy v0.19.1, commit `b56fc29d3016e641754765244b5ba3f9cc504671`.
It captures the complete Mordlite vendor source cut, including the integrated skin-capture phase mapper.
The 22 changed source files are organized into nine commits; grouping is by current responsibility, not a reconstruction of original authorship or chronology.

1. `91b7b4b40df0` — Support sampled MSAA targets and active depth regions
2. `feecb7ab9834` — Respect explicit graphics backend masks during Vulkan interop
3. `8ac5b8d1a5f6` — Avoid sparse compute initialization on unsupported devices
4. `6ea576b446ab` — Expose transient render phase mapping for skin diffusion capture
5. `88e3ab7dcb3d` — Align volumetric fog with the reconstructed main pass
6. `ed8176c1310f` — Align lighting and screen effects with reduced main-pass coordinates
7. `8f3a3f981fc3` — Allocate compatible physical shadow arrays on OpenGL
8. `b6d131d11597` — Allow an application-owned deferred visibility attachment
9. `f495007f93da` — Sample mesh depth pyramids within the active region

[The source manifest](mordlite-patches.json) pins all 230 source/license files and the nine source commits.
All copied source and license bytes match the captured Mordlite vendor tree. Original upstream license files are retained.
Upstream workspace Cargo manifests remain intact. Cargo's published manifests and per-package lockfiles are packaging artifacts, not source patches.

Mordlite continues building its existing vendored crates through its unchanged Cargo patch configuration.
This fork owns the extracted patch history; it is not yet a live dependency or an automatic synchronization source.
Future vendor edits must be explicitly reconciled here and exported through reviewed, pinned package preparation; never copy source-workspace Cargo manifests directly over published-package manifests.
The original historical preparers remain provenance records, not a complete current exporter.
The original complete vendor package snapshot and extraction receipt remain in Mordlite's task staging and outputs.

## Upgrade policy

Keep this 0.19.1 branch stable. Prepare any 0.20.1 port on a separate branch based on upstream tag v0.20.1.
For each commit, first check whether upstream supplies the behavior, then port only what remains necessary.
Bevy 0.20.1 uses wgpu30 and WESL engine shaders; this patch stack must not be blindly replayed.
The optional sparse pipeline fix has an upstream replacement candidate and should be verified before being carried forward.
Keep general fixes suitable for upstream contribution separate from Mordlite-specific extension points.
No engine compilation or runtime acceptance is established by this source extraction.
Never run unguarded compiler commands from this checkout; Mordlite builds retain their existing guarded target and manual deployment policy.
