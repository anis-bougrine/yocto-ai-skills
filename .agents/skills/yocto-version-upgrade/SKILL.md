---
name: yocto-version-upgrade
description: Plan and carry out Yocto Project or OpenEmbedded release upgrades by comparing branch-specific migration guidance, adapting layers, and validating the target build.
metadata:
  short-description: Upgrade Yocto releases
---

# Yocto version upgrade

Use this skill when upgrading a Yocto/OpenEmbedded product from one release to another, including changes such as Scarthgap 5.0 to Wrynose 6.0. It supports both migration planning and implementation; follow the user's requested scope.

## Establish the actual upgrade path

Identify the exact source and target Yocto releases, codename, branch or tag, BitBake revision, supported product branches, and any vendor-maintained forks. Do not infer the release from a directory name alone. Use manifests, kas configuration, layer branches, release metadata, and build output to establish the actual state.

Determine whether the user wants an assessment, a migration plan, implementation, or all three. Preserve repository policy and the requested target. Do not silently switch releases, move branches, update unrelated dependencies, publish artifacts, or claim support beyond the evidence.

## Read every relevant migration guide

Use the official Yocto Project migration guide for the target release and review the notes for every release between the source and target, including intermediate point releases. Also inspect the matching BitBake release notes, layer vendor notes, BSP guidance, and product-specific upgrade requirements. Prefer versioned documentation matching the target rather than tip documentation; when a guide has changed, confirm guidance against the release branch or tag being migrated to.

For example, the official Wrynose 6.0 migration notes state that a move from Scarthgap 5.0 must also account for the intervening 5.1 Styhead, 5.2 Walnascar, and 5.3 Whinlatter migration notes. Treat this as a sequence of compatibility changes to assess, even when the project upgrades directly to the Wrynose branch.

Create a migration checklist from applicable changes: removed or renamed variables, classes and recipes; changed defaults; override or API changes; supported host distributions and kernels; fetcher, license, package, image, WIC, SDK, kernel, and bootloader changes; and new QA or security behavior. Do not copy generic release notes into the plan when they do not affect this project.

## Inventory project impact

Inspect all active layers and pin points, including product and vendor layers, their branches/commits and compatibility declarations. Search configuration, recipes, appends, classes, scripts, image recipes, WKS files, CI/build containers, and release manifests for migration-sensitive constructs. Use layer and BitBake inspection tools when the environment is available. Trace each finding to its file and determine whether it is active for the product's machines and distros.

Build an impact matrix with: migration note, affected project file or layer, required action, owner/dependency if known, and verification evidence. Separate confirmed incompatibilities from possible risks and items already handled upstream. Note layer upgrades that must move together and any unavailable vendor support.

## Implement in reviewable increments

Keep the source and target states explicit. Follow the project's upgrade strategy and keep changes scoped to migration needs. Where the project needs intermediate compatibility work, organize changes so each step is reviewable; do not create speculative intermediate branches or commits unless requested. Update layer pins and product metadata coherently, and preserve local patches or policy unless a migration note requires a change.

For each fix, use the target release's actual metadata API and documentation. Avoid compatibility shims that hide removed behavior or warnings without a documented reason. Do not suppress QA, license, CVE, or deprecation reports just to get a green build. Record justified exceptions and their removal criteria.

## Validate the target progressively

Use the project's normal setup and CI process. Validate in increasing scope as practical: metadata parsing and layer compatibility, affected recipes/classes, package and image construction, SDK or WIC outputs where used, and target boot/runtime behavior for affected hardware. Use clean or isolated build directories when needed to separate cache effects or preserve the source-release build. Avoid deleting shared downloads or sstate as a routine step.

For failures, identify the first causal task and classify it as migration defect, upstream/vendor regression, environment problem, or unresolved. Re-run the smallest command that exercises each repair, then run product-level gates appropriate to the request. If hardware, proprietary layers, network sources, or long builds are unavailable, report what remains unverified.

## Report the result

Deliver the migration checklist or impact matrix, changed files, relevant release notes, verification commands and results, blockers, accepted risks, and evidence gaps. Distinguish a plan from an implemented and validated migration. State exact source and target revisions; do not say the upgrade is complete based only on metadata parsing or one recipe build.

## References

- Yocto Project migration guides: https://docs.yoctoproject.org/migration-guides/index.html
- Yocto Project release documentation: https://docs.yoctoproject.org/

