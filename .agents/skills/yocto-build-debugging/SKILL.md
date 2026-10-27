---
name: yocto-build-debugging
description: Diagnose Yocto and BitBake parse, fetch, task, signature, sstate, packaging, and image build failures from logs and metadata.
metadata:
  short-description: Debug Yocto builds
---

# Yocto build debugging

Use for BitBake parse/build failures, unexpected task behavior, sstate/signature questions, missing packages or image content, and slow or non-reproducible builds.

## Capture context and locate the cause

Record command, target, machine, distro, Yocto/BitBake revisions, host setup, and repeatability. Preserve the first meaningful error and task log. Read active configuration and layer revisions. Do not begin by deleting tmp, sstate, downloads, or the build directory.

Locate the task log, run script, work directory, and recipe inputs. Classify the issue as parse, fetch, task, QA, image assembly, or runtime. The first causal error may precede the final summary.

## Follow evidence

- Parse/override: inspect layer compatibility and bitbake -e history to find effective values and origins.
- Fetch: check SRC_URI, pinned revision, checksums, network/proxy constraints, and source availability. Do not weaken source integrity checks to bypass an unexplained failure.
- Task: inspect log and run script before editing metadata.
- Dependency/order: use tools supported by the installed branch and confirm the relationship is real.
- Sstate/signature: inspect sigdata, task signatures, diffs, and cache configuration where available before invalidating state.
- Packaging/image: inspect do_install, package data, ownership, manifests, and package inclusion. A successful recipe build does not prove image inclusion.
- Performance: identify expensive tasks and cache misses before proposing concurrency/storage changes; account for memory and I/O.

Check current options with bitbake --help or the matching manual. Avoid exposing credentials or environment secrets in reports.

## Repair and verify

Choose the smallest evidence-backed change. Avoid broad clean operations as diagnosis. If a clean or forced rerun is needed, scope it to the affected recipe/task and state the cost. Do not delete shared caches or alter global configuration without need and authorization.

Re-run the narrowest command that exercises the fix; check for the original failure and new QA/parse errors. Separate environment blockers from metadata defects. State exactly what passed, what did not run, and why. Do not claim an image is fixed when only one task was validated.

Reference: documentation and command help matching the checked-out BitBake version at https://docs.yoctoproject.org/bitbake/
