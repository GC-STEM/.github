# Working in GC-STEM/.github

Start with this file and the linked repository guidance; also check for applicable `AGENTS.md` and `.github/instructions/*.instructions.md` files. Verify current files and GitHub documentation whenever guidance is incomplete, outdated, or conflicting. This public repository maintains GC-STEM's supported default community standards and templates, the public organization profile, and this repository's validation automation. It is not an application or service: there is no application build, deployment, or course-assignment test command. Its checks are documented in [CI guidance](./ci/README.md).

## Ownership and repository map

Use [README.md](../README.md) to identify the resource's owner before editing:

- This repository owns STEM-wide community defaults, its issue and pull request templates, and organization-wide profile content. `.github/ci/` holds this repository's validation policy, scripts, dependencies, regression tests, and link-check settings; `.github/workflows/` runs those checks. These workflows and repository settings are specific to this repository.
- The [shared STEM wiki](https://github.com/GC-STEM/.github/wiki) is maintained separately. `crs000` owns master CS course templates and configuration; its wiki owns shared CS-course documentation. Individual `csXXX` repositories and wikis own course content and course-specific requirements. A student's repository and local clone belong to the student.
- Root [CONTRIBUTING.md](../CONTRIBUTING.md), [CODE_OF_CONDUCT.md](../CODE_OF_CONDUCT.md), [ACCESSIBILITY.md](../ACCESSIBILITY.md), [SECURITY.md](../SECURITY.md), [SUPPORT.md](../SUPPORT.md), and [LICENSE](../LICENSE) are the authoritative repository sources for contribution, conduct, accessibility, security/privacy, support, and reuse. Follow course-specific collaboration and AI rules; repository review does not replace required institutional approval. The README identifies General Counsel for licensing, Marketing for branding, and designated academic authorities for instructional content. Standards remain provisional while institutional review is pending.
- `profile/README.md` is an explicitly unfinished profile scaffold, not approved academic or administrative information. `docs/` contains software-lifecycle document scaffolds with TODOs and placeholders, not automatically approved organizational guidance or ready-to-distribute course templates. `schemas/manifest.schema.json` describes an SOE/CSO manifest; establish the owning workflow and requirements before changing or treating it as a GC-STEM-wide requirement.
- `.github/ISSUE_TEMPLATE/`, `.github/PULL_REQUEST_TEMPLATE/`, `.github/DISCUSSION_TEMPLATE/`, and `.github/VULNERABILITY_REPORT.yml` hold GitHub forms, templates, or their supporting guidance. `.github/CODEOWNERS` describes ownership for this repository only.

The current [CI README](./ci/README.md) names `.github/pull_request_template.md` as the single pull request template, but the tracked template is `.github/PULL_REQUEST_TEMPLATE/default.md`. Follow the actual template and current GitHub documentation; do not silently propagate the discrepancy. Also verify the manifest schema's ownership: the current schema describes SOE/CSO v3.2, while `.github/CHANGELOG.md` calls it an unchanged IT-140 schema. The active `.github/ISSUE_TEMPLATE/config.yml` directs Academic Support to Microsoft Apps, while [SUPPORT.md](../SUPPORT.md) directs course and academic questions to Brightspace; do not treat these routes as reconciled or change either without maintainer review.

## GitHub distribution boundaries

GitHub displays supported default community health files from this public `.github` repository for eligible GC-STEM-owned repositories that lack a repository-specific equivalent. It checks a destination repository's `.github/`, root, then `docs/`, before checking the defaults in those locations. These displayed defaults are not copied into the destination repository, its clone, or its downloads. Repository-specific files take precedence; a repository's issue-template folder or configuration can replace the default issue-template set.

Creating a repository from a template copies its starting files and creates a separate repository; later template edits do not synchronize automatically. Maintain or copy any needed updates explicitly. The `crs000` to course-repository relationship is a starting template, not ongoing synchronization. Wikis are separate. Student-owned repositories do not automatically receive GC-STEM defaults.

Do not treat every file in this repository as a community default. `.github/copilot-instructions.md`, `.github/instructions/*.instructions.md`, and `AGENTS.md` guide work in the repository where they are present; they are not distributed as community defaults to sibling repositories. Workflows, CODEOWNERS, `.editorconfig`, `.gitattributes`, and licenses have their own repository-specific behavior and must be maintained where needed. See [GitHub's default community health file documentation](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file), [repository template documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template), and [Copilot repository instructions documentation](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions).

## Writing and review

Follow [CONTRIBUTING.md](../CONTRIBUTING.md) and the affected resource's owner and review process. Keep course autonomy and approved exceptions intact; do not invent course requirements, institutional authority, academic rules, permissions, or approval requirements. Public availability is not a license to reuse content. The repository's interim [license notice](../LICENSE) grants no general reuse permission.

For educational resources, use clear, accessible language; explain unfamiliar GitHub terms when useful; and tailor explanations to the reader's stated context without assuming expertise, identity, access, or authority. Explain why a practice matters when it helps readers decide. Keep useful resources discoverable from the README, organization profile, and relevant supplemental documentation, and preserve a usable path for people who do not use Copilot. Route course, grading, enrollment, employment, account, and institutional questions to documented official resources, not invented GitHub procedures; surface conflicting routes without guessing which policy controls. Follow existing guidance to protect credentials, student information, private communications, and restricted coursework.

Preserve working repository-relative links and use absolute GitHub/wiki URLs for separately maintained resources. Match nearby Markdown and form conventions. `.editorconfig` specifies UTF-8, final newlines, spaces, and Markdown trailing-whitespace preservation; it sets two-space indentation for JSON/YAML and four-space indentation for Python. `.gitattributes` specifies CRLF for Markdown and student-submitted files, and LF for JSON/YAML and scripts. Avoid broad reformatting or line-ending changes.

## Setup and validation

Run commands from the repository root with Git and Python 3.12. Install the pinned CI dependencies, then run the checks relevant to the change:

```bash
python -m pip install --disable-pip-version-check -r .github/ci/requirements.txt
python .github/ci/check_repository.py
python -m compileall -q .github/ci
python -m ruff check --isolated --select E,F,I --line-length 80 .github/ci
python -m unittest discover -s .github/ci -p 'test_*.py' -v
python .github/ci/check_readme_commands.py --shell bash
```

`requirements.txt` pins EditorConfig, json5, PyYAML, and Ruff. Repository/configuration changes need `check_repository.py`; Python automation changes also need compileall, Ruff, and regression tests; documentation or templates with shell examples need the Bash syntax check. The syntax checker uses shell `-n`: it parses explicitly labeled Bash fences but does not execute documented commands. Its coverage is not a functional test.

For documentation, templates, and link changes, install Lychee v0.24.2 as in the workflows and run:

```bash
python .github/ci/check_links.py --mode internal --output /tmp/internal-links.md
python .github/ci/check_links.py --mode external --output /tmp/external-links.md
```

The internal check is offline; the external check requires network access. Login redirects, bot protection, rate limits, and generated anchors may need manual review. Do not broaden exclusions or accept errors just to pass. Workflow changes also require actionlint v1.7.12 (`actionlint -color`); GitHub Actions runs the pinned version and verifies the download. GitHub Actions results remain the authoritative hosted check.

The validators and link and documented-command scans discover files with `git ls-files`; newly added documentation is invisible until tracked. Ensure new files are tracked before running these scans, then review the index and final diff. Use GitHub Actions for checks requiring hosted runners, and report unavailable tools or network checks rather than claiming they passed.
