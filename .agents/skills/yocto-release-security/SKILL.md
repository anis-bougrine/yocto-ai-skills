---
name: yocto-release-security
description: Prepare or review Yocto product releases, migrations, and supply-chain security evidence including pinned inputs, licenses, SBOMs, CVEs, and reproducibility.
metadata:
  short-description: Prepare Yocto releases
---

# Yocto release and security

Use for release readiness, Yocto branch migrations, supply-chain evidence, vulnerability review, license compliance, reproducibility, and release artifact manifests.

## Anchor on the product release

Identify product policy, supported Yocto branch, layer/tool revisions, release manifest or kas configuration, target machines, and build environment. Consult migration notes for the exact source and destination releases. Do not assume current manuals describe an older product branch correctly.

Treat source revisions, configuration, patches, toolchain, and host environment as release inputs. Identify mutable references and unpinned dependencies. Recommend changes within the product release process; do not update unrelated layers or move branches without scope.

## Review migration impact

Compare release notes, migration guides, BitBake changes, host requirements, recipe updates, removed variables/classes, override syntax, license metadata changes, and known issues. Search project metadata for affected constructs and validate on the destination branch. Keep migration edits traceable to the compatibility change.

## Gather supply-chain evidence

Where supported by the branch and product process, collect:
- Layer commits, configuration, machine/distro, image target, source revisions, and tool versions.
- Build logs, task outcomes, package/image manifests, artifact checksums, and provenance.
- License and source-compliance evidence for shipped packages.
- SPDX SBOMs and vulnerability reports, noting data date and tool/database assumptions.
- Reproducibility evidence from independent builds or established project checks.

An SBOM does not prove a release is vulnerability-free. CVE matching can be incomplete or produce false positives; triage dispositions with evidence. Use exclusions only when justified and documented.

## Assess product security

Review the product threat model and image configuration. Consider build-input integrity, patch provenance, credentials, debug services, exposed packages, default accounts, update/boot trust, writable paths, and signing when in scope. Separate build-system security from runtime product security. Do not claim certification based on a configuration scan.

Use security, vulnerability, SPDX, hardening, read-only rootfs, and signing mechanisms supported by the target branch. Verify variable names and feature availability before recommending them.

## Report release readiness

Provide evidence-based blockers, resolved items, accepted risks, missing evidence, and next actions. Separate confirmed defects from unknowns and identify matters needing legal, security, or hardware review. State the analysis scope. Do not publish, sign, or distribute artifacts unless explicitly requested.

References:
- Yocto manuals and matching migration guides: https://docs.yoctoproject.org/
- Security manual: https://docs.yoctoproject.org/security-manual/
- SBOM manual: https://docs.yoctoproject.org/dev-manual/sbom.html
