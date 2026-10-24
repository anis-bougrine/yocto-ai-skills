---
name: yocto-layer-engineering
description: Design, inspect, and change Yocto/OpenEmbedded layers, configuration, overrides, and metadata integration while preserving project conventions.
metadata:
  short-description: Engineer Yocto layers
---

# Yocto layer engineering

Use for layer creation/integration, layer configuration, machine or distro metadata, overrides, append files, and metadata precedence.

## Establish project shape

Identify the checked-out Yocto/BitBake release, manifest or kas files, layer revisions, setup entrypoint, build configuration, contribution guidance, and nearby metadata conventions. Treat checked-out metadata as authoritative. Syntax and behavior vary by release; verify unfamiliar behavior in the matching manuals.

Map the active stack with bitbake-layers show-layers, show-recipes, show-appends, and show-overlayed where available. If the environment is not initialized, locate the project setup entrypoint and explain the missing environment instead of guessing paths.

## Change metadata coherently

- Follow local naming, directory, license-header, formatting, and branch conventions.
- In layer.conf, use comparable layers' conventions for collection, pattern, priority, and supported series. Do not invent compatibility claims.
- Keep product policy in the product layer or owning distro/machine configuration. Prefer a focused append or override to editing upstream layers.
- Check bbappend filename matching and supported recipe versions across branches.
- Use syntax supported by the target BitBake release; do not mechanically translate override syntax.
- Keep machine, distro, image, and package responsibilities distinct.
- Avoid adding dependencies or changing layer priority just to force an accidental selection.
- Trace assignment, append, override, include, and precedence. Use bitbake -e target to inspect effective values and history.

## Review integration

Identify affected recipes, machines, distros, images, and branches. Check for shadowed recipes, orphaned appends, missing manifest entries, layer dependencies, and compatibility declarations. Use project parse/layer checks and a targeted build when available; avoid full image builds by default.

Summarize changed files and behavior. Include evidence from layer inspection or final values, and state assumptions that could not be verified.

Reference: matching Yocto Project and BitBake manuals at https://docs.yoctoproject.org/
