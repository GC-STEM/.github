# Working in GC-STEM/.github

This public repository maintains GC-STEM's default community standards,
templates, organization profile, and repository validation automation.
It also helps administrators, maintainers, faculty, and students understand
GitHub organizational practices.

Start with these instructions and applicable `AGENTS.md` and
`.github/instructions/*.instructions.md` files when present. Read guidance
relevant to the task; verify current files and official GitHub documentation
when information is incomplete, outdated, or conflicting.

## Purpose, ownership, and authority

- Use [README.md](../README.md) to identify the resource's owner.
  This repository owns shared community standards and templates;
  `profile/README.md` is the organization profile; `schemas/` contains
  shared manifest schemas; `.github/ci/` and `.github/workflows/` contain
  this repository's validation tools and workflows.
- Atlas owns the shared operating environment and its automation.
  `crs000` owns master CS course templates and configuration.
  Course repositories own course-specific materials. Wikis are maintained
  separately; student repositories and local clones belong to students.
- Follow [CONTRIBUTING.md](../CONTRIBUTING.md),
  [CODE_OF_CONDUCT.md](../CODE_OF_CONDUCT.md),
  [ACCESSIBILITY.md](../ACCESSIBILITY.md),
  [SECURITY.md](../SECURITY.md), [SUPPORT.md](../SUPPORT.md),
  and [LICENSE](../LICENSE).
- Preserve documented institutional approvals, course autonomy, approved
  exceptions, and provisional status. Public availability alone does not
  grant reuse permission. Follow existing course collaboration and AI rules.
- Check the purpose and approval status of scaffolds, examples, TODOs,
  and placeholders before presenting them as established guidance.
- Identify genuine conflicts affecting the task, explain the evidence,
  and follow documented ownership and approval requirements. Report
  unresolved discrepancies separately from permanent agent instructions.

## GitHub defaults and templates

- Preserve recognized GitHub locations and repository-specific overrides.
  Supported community defaults apply to eligible GC-STEM-owned repositories
  lacking their own equivalents. They are displayed by GitHub, not copied
  into receiving repositories or clones.
- A repository's own issue templates or configuration replace the default
  issue-template set. Labels referenced by inherited forms must exist in
  this repository and each receiving repository.
- Distinguish a single automatic `pull_request_template.md` in a supported
  location from named templates under `PULL_REQUEST_TEMPLATE/`.
  Named templates require explicit selection, such as the `template` URL
  parameter; naming one `default.md` does not make it automatic.
- Repository templates provide starting copies without ongoing
  synchronization. Wikis are separate. Student-owned repositories do not
  automatically receive GC-STEM defaults.
- Copilot instructions, `AGENTS.md`, workflows, CODEOWNERS, formatting
  configuration, and licenses are not inherited as community defaults.
  Maintain required copies explicitly.

## Changes and communication

- Keep changes focused, preserve unrelated work, and update affected
  references. Explain the resulting behavior and relevant validation.
- Use accessible language, explain unfamiliar GitHub concepts when useful,
  and tailor guidance to the reader's stated context. Keep resources
  discoverable and usable without Copilot.
- Route academic, grading, enrollment, employment, and account questions
  to documented official resources. Do not invent institutional claims,
  course requirements, permissions, or approval procedures.
- Protect credentials, student information, private communications,
  and restricted coursework. Follow documented private reporting routes.
- Preserve working repository-relative links. Use absolute URLs for
  separately maintained repositories and wikis.

## Formatting and submission compatibility

- Follow the current [.gitattributes](../.gitattributes) and
  [.editorconfig](../.editorconfig). Currently, Markdown, Python, and
  PowerShell use CRLF; JSON, YAML, and Unix shell scripts use LF.
  Preserve binary files and avoid unrelated reformatting.
- GC-STEM's course-submission EOL requirements are based on institutional
  testing with Brightspace and Turnitin. Preserve that tested policy and
  its file-specific exceptions.
- Any infrastructure EOL migration is separately scoped work. Update
  related editor, formatter, validation, and documentation settings together;
  do not propagate infrastructure defaults into course configurations.
- When changing distributed settings or file-generation behavior, validate
  final course-bound artifacts against the destination policy. Configuration
  agreement or normalized Git content alone does not prove submission-byte
  compatibility.

## Automation safeguards

- Preserve `permissions: {contents: read}`, full commit SHA pins for external
  actions, `persist-credentials: false` for checkout, and the
  `GC-STEM/.github` job restrictions. Do not introduce `pull_request_target`.
- Preserve validation coverage and documented security controls.
  Do not suppress failures, accept error responses, or broaden link
  exclusions merely to obtain passing checks.

## Setup and validation

Use Git and Python 3.12 from the repository root. See
[CI guidance](./ci/README.md) and current workflows for installation details
and pinned tool versions.

```bash
python -m pip install --disable-pip-version-check -r .github/ci/requirements.txt
python .github/ci/check_repository.py
```

Select additional checks relevant to the change:

- Documentation or templates containing Bash examples:

  ```bash
  python .github/ci/check_readme_commands.py --shell bash
  ```

  Ensure Bash is available. This checks syntax without executing examples;
  it does not establish functional correctness.

- Python automation:

  Ensure Bash and Lychee v0.24.2 are available on PATH before running the
  regression suite. Missing prerequisites cause test classes to skip.

  ```bash
  python -m compileall -q .github/ci
  python -m ruff check --isolated --select E,F,I --line-length 80 .github/ci
  python -m unittest discover -s .github/ci -p 'test_*.py' -v
  ```

- Documentation, templates, or links:

  Install Lychee v0.24.2 before these checks. Internal checking is offline;
  external checking requires network access.

  ```bash
  python .github/ci/check_links.py --mode internal --output /tmp/internal-links.md
  python .github/ci/check_links.py --mode external --output /tmp/external-links.md
  ```

  Choose suitable report paths on Windows. Manually investigate restricted
  pages, login redirects, rate limits, and generated anchors.

- Workflows: run the repository validator and actionlint v1.7.12
  (`actionlint -color`), using the verified installation in `tests.yml`.

Scans use `git ls-files`. Stage only intended new files when necessary for
discovery, preserving pre-existing staged work. Inspect the final diff.

Report checks passed, failed, skipped, or unavailable, including lost test
coverage and pre-existing failures. Verify relevant GitHub Actions results;
external-link checks are currently manual or scheduled, not automatic on
every pull request.
