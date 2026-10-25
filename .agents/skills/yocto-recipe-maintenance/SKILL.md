---
name: yocto-recipe-maintenance
description: Create, update, or review BitBake recipes, bbclasses, patches, and package metadata with attention to fetching, licensing, dependencies, packaging, and task behavior.
metadata:
  short-description: Maintain BitBake recipes
---

# Yocto recipe maintenance

Use for adding/upgrading software, repairing recipe metadata, maintaining patches, changing package splits, or reviewing a bbclass.

## Discover conventions

Inspect the recipe, appends, neighboring recipes, layer guidance, active layer stack, and Yocto/BitBake release. Check release-specific syntax in matching manuals or repository examples. Look for an existing recipe before adding one. Decide whether the change belongs in a recipe, append, class, distro configuration, or image package list.

## Build reliable recipes

- Pin source inputs. Use accurate archive checksums; use immutable Git revisions according to project policy. Do not use moving branch heads for release builds.
- Keep SRC_URI, patch search paths, checksums, and source-directory assumptions consistent. Confirm patches apply to the selected source revision.
- Declare accurate license metadata and required license files/checksums using target release conventions. Never infer a license from project name or use a blanket license value.
- Model build-time and runtime dependencies separately. Use package-scoped dependencies when granularity matters; do not add dependencies merely to silence QA.
- Choose classes and task overrides that match the upstream build system. Avoid replacing standard tasks without need.
- Review PACKAGECONFIG options and dependency effects. Check installed paths, package ownership, FILES entries, and package splits. Avoid broad globs that hide install mistakes.
- Align sysroot staging, service integration, user/group creation, alternatives, and post-install behavior with local conventions and release-specific classes.
- Preserve patch purpose, provenance, and upstream status. Avoid overlapping patches.
- Do not fetch network dependencies from configure or compile tasks. Route inputs through BitBake fetchers.

## Work and verification

Consider devtool add/modify/upgrade when supported, then review generated metadata. Use bitbake -e for effective values/origins; use task listing or graph tools when task order is unclear. Build the narrowest relevant recipe/package, inspect task logs and QA, and inspect package contents when packaging changes. Confirm image inclusion if requested.

Avoid broad cleans unless evidence indicates stale state; state rebuild cost. Report unavailable source, license evidence, architecture, or runtime environment. State precisely what passed and do not describe a recipe-only check as a full image build.

Reference: BitBake and Yocto manuals for the checked-out release at https://docs.yoctoproject.org/
