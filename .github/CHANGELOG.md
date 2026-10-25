# Changelog

Notable changes to GC-STEM/.github. Add approved changes under Unreleased;
record a version and release date only when a release is published.

## Unreleased

### Added

- **Default templates:** Added issue forms in `.github/ISSUE_TEMPLATE/` and
  the default `.github/pull_request_template.md`. Existing root-level
  template folders can be removed after review.
- **CI safeguards:** Added regression coverage for repository validation
  without course IDE configuration.
- **Maintenance:** Added migration notes and ignore rules for Python caches.

### Changed

- **Repository scope:** Retargeted workflow guards and CI documentation
  from GC-STEM/_core to GC-STEM/.github.
- **Validation:** Require this repository's community files, organization
  profile, templates, and CI files. Course editor, IDE, and Git configuration
  remain the responsibility of crs000 and downstream course repositories.
- **Ownership:** Updated CODEOWNERS paths for community standards and the
  organization profile. Existing team names are retained.

### Fixed

- **Workflow execution:** Checks can run in the renamed repository instead
  of being skipped by the former repository-name guard.
- **EoL validation:** This repository explicitly disables course-specific
  line-ending checks. Those checks remain enabled by default when the
  validator is used elsewhere.
- **Dependency instructions:** Corrected the legacy manifest dependency path.

## Maintenance Notes

The IT-140 manifest schema and image assets are retained unchanged. Tracked
Python bytecode is excluded from the update package; remove the existing
tracked cache separately.
