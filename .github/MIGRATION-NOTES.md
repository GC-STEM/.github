# Migration Review — GC-STEM/.github

Reviewed the `main` snapshot at
[a0411748715c2f233192e803da4f70e312b71138](https://github.com/GC-STEM/.github/commit/a0411748715c2f233192e803da4f70e312b71138)
on October 13, 2026. This package updates the repository's `.github/`
folder and adds default templates in GitHub's recognized locations.

## Extract All

Extract directly to `D:\Repos\_Core\.github\.github\`.
The ZIP starts with `ci/`, `workflows/`, `assets/`, and the other files
in this folder; it has no enclosing `.github/` directory.

Extraction replaces files with matching names and adds new files. It does
not remove obsolete files. Review the resulting Git diff before committing.

## Changes Included

- Workflow guards target `GC-STEM/.github`.
- The required-file policy matches STEM-wide community standards and
  this repository's profile, templates, and CI.
- Course line-ending and IDE requirements are disabled for this repository.
  The validator preserves those checks by default for reuse elsewhere.
- Issue forms are in `.github/ISSUE_TEMPLATE/`; the default pull request
  template is `.github/pull_request_template.md`.
- CODEOWNERS paths, CI documentation, and the changelog reflect the new role.
- Image assets and the IT-140 manifest schema are preserved unchanged.

`core-policy.json` keeps its filename for compatibility. It now describes
this repository's requirements.

## Remaining Work Outside This Folder

- Update root-level `ACCESSIBILITY.md` and `CONTRIBUTING.md`, which still
   reference the former repository and wiki. Review every destination;
   `GC-STEM/.github` currently has Discussions disabled, so simply replacing
   the old Discussions URL would not provide an active support channel.
- Fix the two `../LICENSE` links in root-level `CONTRIBUTING.md` to
   `LICENSE`. Its other relative policy links resolve correctly.
- Verify or transfer referenced wiki pages. Keep required course guidance
   in course repositories and use the wiki for optional supplements.
- Remove obsolete root-level `ISSUE_TEMPLATE/` and
   `PULL_REQUEST_TEMPLATE/` after reviewing the included replacements.
   The empty root-level `DISCUSSION_TEMPLATE/` is also misplaced; future
   discussion forms belong in `.github/DISCUSSION_TEMPLATE/`.
- Remove the tracked
   `.github/ci/__pycache__/check_readme_commands.cpython-313.pyc`.
   The included ignore file prevents new Python caches from being added.
- Verify that the existing `@GC-STEM/maintainers` and `@GC-STEM/admins`
   teams exist and have the required repository access.
- Move the IT-140-specific `.github/manifest/` schema and its course
   dependencies to the owning course repository. It is not a STEM-wide
   community standard or an organization default.

Repository-wide link checks may report these existing documentation issues.
The update does not suppress them.

## Validation

- All 23 regression tests passed, including Lychee integration tests.
- Strict repository validation, Ruff, Bash documentation syntax, and
  actionlint passed.
- Internal link checking found two failures, both `../LICENSE` references
  in root-level `CONTRIBUTING.md`. No failures originated in the bundled files.
- Existing action commit pins were verified against their source repositories.
  The downloaded actionlint and Lychee releases matched their published hashes.
- A full live external-link scan was not run.

## Architecture Reminder

The public `GC-STEM/.github` repository supplies supported community-file
defaults. cs000 supplies CS course templates and configuration. Student-owned
repositories do not inherit GC-STEM defaults. CODEOWNERS, workflows, editor
settings, licenses, and course manifests need separate management.

See [GitHub's default-file requirements](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).
