# GC-STEM GitHub Standards CI

Continuous integration (CI) checks changes to
[GC-STEM/.github](https://github.com/GC-STEM/.github). These workflows validate
this repository's community standards, profile, templates, and automation.
Course configuration and assignment tests belong in crs000 or the applicable
course repository.

## Workflows

| Workflow | Checks | Runs |
| -------- | ------ | ---- |
| GitHub Standards Validation | Required files, configuration syntax, Python automation, regression tests, and GitHub Actions syntax | Push, pull request, manual |
| Documentation Command Syntax | Labeled Bash blocks on Linux, macOS, and Windows Git Bash | Push, pull request, manual |
| Internal Links | Local files, images, directories, and supported heading anchors | Push, pull request, manual, weekly |
| External Links | HTTP/HTTPS destinations and supported heading anchors | Manual, weekly |

Both link workflows run Monday at **11:17 UTC**
(07:17 EDT / 06:17 EST). Schedules use the default branch, may be delayed,
and can be disabled by GitHub after 60 days of public-repository inactivity.

Every job is restricted to `GC-STEM/.github`. These workflows, scripts,
and CODEOWNERS rules are specific to this repository; GitHub does not
distribute them through its default community-file mechanism.

## Files

- **core-policy.json:** This repository's required files and validation
  options. The filename is retained for compatibility with existing tools.
- **check_repository.py:** Parses configuration and applies the selected
  repository policy.
- **check_readme_commands.py:** Checks explicitly labeled shell fences
  without executing their commands. The workflow checks Bash.
- **check_links.py:** Runs Lychee on tracked Markdown and HTML, including
  hidden folders and link text in issue-template YAML.
- **lychee.toml:** Shared link settings and reviewed exceptions.
- **requirements.txt:** Pinned dependencies for these checks.
- **test_ci.py:** Regression tests for configuration, safe syntax checks,
  and link failure detection.

## Validation Scope

The policy requires community files at the repository root, the organization
profile, recognized issue and pull request templates, and CI files.
GitHub-supported defaults are used by other GC-STEM repositories when local
equivalents are absent; they are not copied into those repositories or clones.

This policy sets `check_eol` to `false` and does not require course
`.gitattributes`, `.editorconfig`, `.vscode`, or `pyproject.toml` files.
The reusable validator keeps line-ending checks enabled by default for
repositories whose policies use them.

Configuration checks parse JSON/JSONC, TOML, and YAML. Workflows must use
read-only permissions, full action commit SHAs, and checkout without
persisted credentials. actionlint checks GitHub Actions syntax separately.

## Link Checks

The internal job makes no network requests. Absolute GitHub and wiki URLs
are checked by the external job. Both jobs publish an Actions summary and
retain their report artifacts for 14 days.

External checks use fresh requests, follow redirects, retry failures twice,
and require successful HTTP responses. There are no initial URL exclusions.
Do not accept error statuses or broadly exempt GitHub or SNHU links to make
a check pass. Add precise, documented exceptions only after manual review.

Login redirects, bot protection, rate limits, JavaScript-generated anchors,
and restricted pages can require manual verification. Linked remote pages
are not checked recursively. Example URLs in code blocks and email addresses
are excluded.

## Run Locally

Use Python 3.12 and Git from the repository root:

```bash
python -m pip install -r .github/ci/requirements.txt
python .github/ci/check_repository.py
python .github/ci/check_readme_commands.py --shell bash
python -m ruff check --isolated --select E,F,I --line-length 80 .github/ci
python -m unittest discover -s .github/ci -p 'test_*.py' -v
```

Install Lychee **v0.24.2** for link checks and integration tests:

```bash
python .github/ci/check_links.py --mode internal --output /tmp/internal-links.md
python .github/ci/check_links.py --mode external --output /tmp/external-links.md
```

Choose a suitable report path on Windows. Stage new documentation before
checking it: the scripts use Git's tracked-file list. Link integration tests
run when Lychee is on PATH. `--strict` treats validator warnings as failures.

Shell syntax checks do not prove documented commands work. Transcript,
PowerShell, indented, and nested examples are outside the Bash check.

## Maintenance

Propose STEM-wide standards here and CS configuration in
[crs000](https://github.com/GC-STEM/crs000). Keep required course materials in
course repositories; wiki links must use absolute URLs. Respect institutional
approval processes for legal text, branding, and instructional requirements.

Review dependency and action pins deliberately, run regression tests, and
inspect Actions results after pushing. Template creation does not provide
automatic synchronization; review any copying or reuse separately.

## References

- [Default community files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [GitHub Actions syntax](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax)
- [Scheduled workflow events](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#schedule)
- [Lychee](https://github.com/lycheeverse/lychee)
- [actionlint](https://github.com/rhysd/actionlint)
