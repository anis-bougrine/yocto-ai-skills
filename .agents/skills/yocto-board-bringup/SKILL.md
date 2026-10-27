---
name: yocto-board-bringup
description: Bring up or adapt a Yocto machine and image for a hardware board, covering machine metadata, kernel and boot artifacts, device trees, firmware, and boot evidence.
metadata:
  short-description: Bring up Yocto boards
---

# Yocto board bring-up

Use when enabling a board or SoC, diagnosing boot failures tied to machine metadata, or integrating kernel, bootloader, device tree, firmware, and image artifacts.

## Establish hardware and build context

Identify exact board revision, SoC, boot media, boot ROM/firmware path, and expected boot chain. Record Yocto release, active machine, distro, image target, layer revisions, and setup. Read vendor documentation and repository bring-up notes. Do not assume board revisions share pinmux, DRAM, bootloader, or device-tree requirements.

Inspect existing machine configurations and recipes. Identify which layer owns machine, kernel, bootloader, firmware, and image integration. Reuse existing BSP support where possible.

## Trace the artifact path

Follow machine configuration, kernel provider/configuration, device-tree selection, bootloader configuration, firmware, image layout, boot partition contents, and deployed filenames. Check that every required artifact is built, installed, deployed, and referenced by the storage layout. Verify variable semantics for the checked-out release; inspect effective values with bitbake -e and task logs.

Keep board-specific details in the owning layer. Do not invent register values, pin assignments, timing parameters, or device-tree properties; require vendor documentation or measured evidence. Document workarounds with affected board revision, symptom, rationale, and removal condition.

## Diagnose and verify

Separate build failures from runtime boot failures. For builds, start with the first failing task and log. For boot issues, collect serial output, bootloader environment, storage layout, reset behavior, and last confirmed stage. Map evidence to the boot chain before changing configuration.

Build the narrowest relevant target, inspect deploy artifacts and image contents, and verify the flash/boot procedure. If hardware is unavailable, state what was checked offline and what needs a physical boot. For runtime validation, record board revision, image identity, boot medium, console evidence, and functions tested. Do not generalize board support from one compile.

Summarize boot-path changes, metadata/artifacts, evidence, and unresolved hardware assumptions. Provide reproduction commands when practical.

Reference: project BSP materials and matching Yocto documentation at https://docs.yoctoproject.org/
