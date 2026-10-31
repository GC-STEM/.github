# Working in GC-STEM/.github

This public repository maintains GC-STEM's default community standards,
templates, organization profile, shared schemas, and repository validation
automation. Its public resources also help maintainers, faculty, and students
understand GitHub organizational practices.

There is no application build or deployment process. Validate changes using
the repository's documentation, configuration, and automation checks.

## Start here

- Read this file, [README.md](README.md), and guidance relevant to the task.
  Check for more specific `AGENTS.md` files along affected directory paths.
- Consult [.github/copilot-instructions.md](.github/copilot-instructions.md)
  and relevant files under `.github/instructions/` when present.
  Clients may not load those files automatically.
- For community documents, public information, and templates, read
  `.github/instructions/community-content.instructions.md`.
  For CI scripts and workflows, read
  `.github/instructions/automation.instructions.md`.
- Follow the instruction precedence supported by your client. Keep shared
  guidance consistent and surface substantive conflicts rather than
  inventing a universal hierarchy between instruction formats.
- Verify current files and authoritative documentation when instructions
  are incomplete, outdated, or inconsistent.

## Repository map and ownership

| Location | Responsibility |
| --- | --- |
| Root community documents | Contribution, conduct, accessibility, security, support, and licensing guidance |
| `profile/README.md` | Public organization profile and resource directory |
| `docs/` | Documentation and supporting materials; inspect their purpose and approval status |
| `schemas/` | Shared manifest contracts |
| `.github/ISSUE_TEMPLATE/` | Issue forms and issue-chooser configuration |
| `.github/PULL_REQUEST_TEMPLATE/` | Named PR templates |
| `.github/DISCUSSION_TEMPLATE/` | Discussion forms and supporting guidance |
| `.github/VULNERABILITY_REPORT.yml` | Private vulnerability-report form |
| `.github/ci/` | Validation scripts, policy, dependencies, tests, and link settings |
| `.github/workflows/` | This repository's GitHub Actions workflows |

Atlas owns the shared operating environment and its automation.
`crs000` owns master CS course templates and configuration.
Course repositories own their course-specific materials.
Wikis are maintained separately. Student repositories and local clones
belong to students.

Identify cross-repository effects and follow-up work without silently
expanding the task into other repositories or institutional administration.

## Working process

1. Inspect the working-tree status and affected files. Preserve existing
   staged and unstaged work.
2. Identify the owning resource, intended behavior, applicable guidance,
   and relevant validation before editing.
3. Make focused changes. Update affected references, documentation,
   configuration, and behavioral tests together when needed.
4. Check results using the appropriate commands below. Diagnose failures
   without weakening checks or concealing lost coverage.
5. Inspect the final diff for unintended changes, sensitive information,
   formatting churn, and unresolved placeholders.
6. Report the result, validation evidence, and remaining limitations.

Use documented approval requirements and existing task authorization.
Do not invent institutional permissions, academic rules, or additional
approval procedures. Preserve documented provisional status and distinguish
drafts and examples from approved requirements.

Follow [CONTRIBUTING.md](CONTRIBUTING.md),
[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md),
[ACCESSIBILITY.md](ACCESSIBILITY.md), [SECURITY.md](SECURITY.md),
[SUPPORT.md](SUPPORT.md), and [LICENSE](LICENSE).

## Essential boundaries

- Supported community defaults are displayed by GitHub for eligible
  organization-owned repositories lacking their own equivalents.
  They are not copied into receiving repositories or clones.
- Repository templates provide starting copies without automatic
  synchronization. Wikis are separate. Student-owned repositories do not
  automatically receive GC-STEM defaults.
- Agent instructions, workflows, CODEOWNERS, formatting configuration,
  and licenses are not inherited as community defaults.
- For shared templates, verify supported locations, destination metadata,
  labels, links, and override behavior. Distinguish automatic PR templates
  from named templates requiring explicit selection.
- Keep public guidance accessible and useful without an AI subscription.
  Explain unfamiliar concepts when relevant and route institutional
  questions to documented official resources.
- Protect credentials, student information, private communications,
  and restricted coursework. Preserve course autonomy, approved alternatives,
  and existing collaboration and AI rules.
- Public availability alone does not grant reuse permission.

## Formatting and automation safeguards

- Follow [.gitattributes](.gitattributes) and
  [.editorconfig](.editorconfig). Currently, Markdown, Python, and PowerShell
  use CRLF; JSON, YAML, and Unix shell scripts use LF.
  Preserve binary files and avoid unrelated reformatting.
- Preserve GC-STEM's tested Brightspace and Turnitin submission policy.
  Infrastructure EOL migration is separately scoped work.
  Changes to course-bound output require checking final artifacts against
  the destination policy.
- Preserve workflow read-only contents permissions, full action commit SHA
  pins, disabled persisted checkout credentials, and repository guards.
  Do not introduce `pull_request_target`.
- Preserve syntax-only checking of documented commands, offline internal
  link checks, meaningful failure status, and useful diagnostics.
  Do not suppress failures or broaden exclusions merely to pass checks.

## Setup and validation

Use Git and Python 3.12 for the Python checks. Read
[CI guidance](.github/ci/README.md) and current workflows for installation
details and tool versions. Run commands from the repository root.

Install the pinned CI dependencies and validate repository configuration:

```bash
python -m pip install --disable-pip-version-check -r .github/ci/requirements.txt
python .github/ci/check_repository.py
```

Select additional checks according to the change.

### Documentation and templates

Ensure Bash is available when checking documented Bash examples:

```bash
python .github/ci/check_readme_commands.py --shell bash
```

Install the workflow-pinned Lychee version before link checks:

```bash
python .github/ci/check_links.py --mode internal --output /tmp/internal-links.md
python .github/ci/check_links.py --mode external --output /tmp/external-links.md
```

Choose suitable report paths on Windows. Internal checking is offline;
external checking requires network access.

Review rendered content and relevant GitHub form behavior where available.
Syntax checks do not establish command functionality, form validity,
accessibility compliance, or institutional approval.

### Python automation

Ensure Bash and the workflow-pinned Lychee version are available before
claiming full corresponding regression coverage:

```bash
python -m compileall -q .github/ci
python -m ruff check --isolated --select E,F,I --line-length 80 .github/ci
python -m unittest discover -s .github/ci -p 'test_*.py' -v
```

Inspect skipped tests explicitly. Add or update behavioral tests for relevant
code changes; prose-only edits do not require new Python tests.

### Workflows and schemas

- For workflow changes, run the repository validator and the workflow-pinned
  actionlint version using `actionlint -color`.
- For schema changes, verify the affected contract and identify consumer
  impact. Successful JSON parsing alone does not establish schema validity
  or consumer compatibility.

Scans use `git ls-files`. Stage only intended new files when necessary for
discovery, preserving existing staged work.

## Completion report

State:

- What changed and which files were affected.
- Which checks passed, failed, skipped, or could not run.
- Any pre-existing failures, environmental limitations, or unresolved issues.
- Any relevant receiving-repository or consumer impact.

Verify relevant hosted Actions results when available. External-link checks
are currently manual or scheduled; an unrun or skipped check is not evidence
of success. Keep temporary findings in the report rather than permanent
agent instructions.
