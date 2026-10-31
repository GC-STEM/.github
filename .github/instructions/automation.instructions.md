---
applyTo: ".github/ci/**,.github/workflows/**"
---

# Repository automation

Supplement the [repository-wide instructions](../copilot-instructions.md)
with these practices for validation scripts, CI configuration, dependencies,
tests, workflows, and their documentation.

## Scope and configuration

- Read [CI guidance](../ci/README.md), the affected scripts, their tests,
  and calling workflows before changing behavior.
- Keep automation focused on this repository's community standards,
  templates, profile, configuration, and documentation. Course runtime
  provisioning and assignment tests belong to their owning repositories.
- Keep `core-policy.json` specific to this repository. Distinguish its
  required-file list from requirements imposed by the reusable validator.
- Preserve the separation between configuration parsing and optional EOL
  agreement checks. This repository currently sets `check_eol` to `false`;
  the reusable validator enables those checks by default.
  Disabling EOL checks must not disable other configuration validation.
- Follow the current `.gitattributes` and `.editorconfig`. Running on Linux
  does not authorize converting every script to LF. Keep EOL migrations
  separately scoped and preserve the tested course-submission policy.
- Update affected CLI documentation, workflow calls, policy references,
  and tests together when behavior changes.

## Python implementation

- Use the Python version and pinned dependencies declared by the current
  CI configuration. Keep CI dependencies separate from course environment
  requirements, and avoid unrelated dependency updates.
- Preserve format-specific parsing: strict JSON where required, JSONC
  support where intended, TOML parsing, and safe YAML handling.
  Workflow YAML must preserve `on` as a key; the current validator uses
  `BaseLoader` to avoid YAML 1.1 boolean interpretation.
- Treat configuration and documentation as data. Do not evaluate embedded
  expressions or execute configuration content to validate its syntax.
- Use explicit UTF-8 text handling, `pathlib`, and repository-root-aware
  paths. Preserve supported `--root`, `--policy`, and other CLI options.
  Avoid assumptions about a maintainer's checkout name or home directory.
- Use argument lists for subprocess calls and explicit working directories.
  Preserve appropriate timeouts, useful error messages, and failure status.
- Keep validation errors distinct from review warnings. Preserve the
  documented `--strict` behavior rather than silently changing which
  conditions fail normal validation.

## File discovery and EOL validation

- Reuse tracked-file discovery through `git ls-files`. Preserve hidden-file
  coverage and NUL-delimited handling where used. Avoid replacing it with
  unrestricted scans of `.git`, virtual environments, or generated files.
- Newly added files must be tracked before these scans can discover them.
  Stage only intended new files when necessary, preserving existing work.
- For EOL agreement checks, obtain effective attributes from Git and editor
  properties through EditorConfig. Preserve ordered and exact-path
  exceptions instead of approximating them with extension-only rules.
- Configuration agreement does not prove the bytes of a generated or
  packaged student submission. Validate final artifacts separately when
  a task changes course-bound output or distributed settings.
- Keep generated reports, caches, and bytecode out of proposed source
  changes.

## Documented-command checks

- Preserve the syntax-only guarantee in `check_readme_commands.py`.
  Invoke the selected shell with `-n`; do not execute documentation commands,
  substitutions, or redirections to check syntax.
- Check explicitly supported language labels. Distinguish runnable Bash
  examples from transcripts, generic `shell` or `console` blocks, and
  unsupported languages.
- Preserve supported fence handling, source line numbers, unclosed-fence
  errors, and subprocess timeouts.
- Preserve `CI_TEST_SHELL` handling and the Linux, macOS, and Windows Git Bash
  workflow coverage. Verify platform-specific executable resolution when
  changing shell discovery.
- Describe successful syntax validation accurately; it does not establish
  that an example performs its intended operation.

## Link checks and reports

- Preserve the division between offline internal checks and HTTP/HTTPS
  external checks. Internal checking must not make network requests.
- Keep tracked documentation and issue-template YAML link text in scope.
  Preserve source-relative resolution for synthetic Markdown files,
  cleanup on success or failure, and report references to original sources.
- Preserve Lychee's failure exit status. Keep unsuccessful checks visible
  even when reports and summaries are successfully generated.
- Maintain TLS verification, successful-response requirements, bounded
  requests, retries, redirects, and concurrency. Avoid persistent success
  caches that conceal changed destinations.
- Investigate authentication redirects, rate limits, bot protection, and
  generated anchors. Add only precise, documented exceptions after manual
  verification; do not broadly exclude domains or accept error responses
  merely to pass.
- Preserve useful failure reports, Actions summaries, and artifact uploads.
  Keep report paths appropriate to the platform and temporary files out
  of the repository.
- Distinguish configured coverage from comprehensive coverage. Checking
  linked destinations does not recursively validate their contents.

## GitHub Actions safeguards

- Preserve `permissions: {contents: read}`, full commit SHA pins for external
  actions, and `persist-credentials: false` for checkout.
  Do not introduce `pull_request_target`.
- Preserve the `GC-STEM/.github` job restrictions, bounded job timeouts,
  concurrency controls, and failure-report preservation.
- Use the declared shell and correctly quote paths. Pass untrusted text
  as data rather than constructing executable shell commands from it.
  Keep credentials out of commands, reports, and logs.
- When updating tools or actions, verify provenance and compatible inputs.
  Update associated version comments, binary checksums, and documentation
  where applicable.
- Preserve intentional trigger coverage. Internal links and documentation
  syntax currently run on pushes and pull requests; external links are
  checked manually or on schedule. Document intentional trigger changes.

## Tests and verification

- Run the relevant repository validation and checks described in the
  repository-wide instructions and CI guide.
- For Python behavior changes, run compile checks, the configured isolated
  Ruff checks, and relevant `unittest` regression tests.
- Add or update behavioral tests for changed validation, discovery, parsing,
  subprocess, or failure-reporting behavior. Prose-only edits do not require
  new Python tests.
- Keep tests isolated with temporary repositories, controlled fixtures,
  and local HTTP servers. Avoid relying on live public sites for regression
  results. Verify both accepted input and meaningful failure cases.
- Install the workflow-pinned Lychee version and ensure Bash is available
  before claiming full corresponding regression coverage. Inspect skipped
  tests explicitly; a successful test command can include skipped classes.
- For workflow changes, run the repository validator and the pinned
  actionlint version. For link-check changes, exercise the affected internal
  and external behavior.
- Report checks passed, failed, skipped, or unavailable, including missing
  prerequisites and pre-existing failures. Verify relevant hosted Actions
  results without treating an unrun or skipped job as a successful check.
