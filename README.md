# GC-STEM GitHub Standards

> [!WARNING]
> **Under Development (October–December 2026)**
>
> This repository is under construction. Standards and templates are
> provisional until approved for production use.

## Table of Contents <!-- omit from toc -->

1. [Purpose](#purpose)
2. [Repository Architecture](#repository-architecture)
3. [Standards and Inheritance](#standards-and-inheritance)
4. [Ownership and Governance](#ownership-and-governance)
5. [Access and Maintenance](#access-and-maintenance)

## Purpose

[GC-STEM/.github](https://github.com/GC-STEM/.github) is the authoritative
source for default GitHub community standards and templates across Southern
New Hampshire University's Global Campus STEM repositories.

It provides:

- **Community standards:** Conduct, contribution, accessibility, security,
  and support policies.
- **Templates:** Default issue, pull request, and discussion templates.
- **Organization profile:** Public content in `profile/README.md`.
- **Supplemental documentation:** Shared STEM guidance in the
  [repository wiki](https://github.com/GC-STEM/.github/wiki).

**Guiding principle:** Define shared standards once, maintain them centrally,
and preserve course-specific autonomy.

## Repository Architecture

GC-STEM uses five layers with distinct ownership and responsibilities.

| Layer | Owner | Repository | Purpose | Upstream | Visibility |
| :---: | ----- | ---------- | ------- | -------- | ---------- |
| 1 | GC-STEM | [`.github.git`](https://github.com/GC-STEM/.github) | Default community standards and templates for GC-STEM repositories | None | Public |
| 1 | GC-STEM | [`.github.wiki`](https://github.com/GC-STEM/.github/wiki) | Supplemental documentation shared across STEM programs | None | Public |
| 2 | GC-STEM | [`crs000.git`](https://github.com/GC-STEM/crs000) | Master template and configuration for CS course repositories | `.github.git` (community standards only) | Public |
| 2 | GC-STEM | [`crs000.wiki`](https://github.com/GC-STEM/crs000/wiki) | Supplemental documentation shared across CS courses | None | Public |
| 3 | GC-STEM | `csXXX.git` | Course content, required documentation, and configuration (`cs100`–`cs999`) | `GC-STEM/crs000.git` (template) | Public |
| 3 | GC-STEM | `csXXX.wiki` | Course-specific supplemental documentation | None | Public |
| 4 | Student | `csXXX.git` | Student-owned online copy of a course repository | `GC-STEM/csXXX.git` | Private |
| 5 | Student | `~/Repos/csXXX` | Local clone of the student's repository | `student/csXXX.git` | Local |

> [!NOTE]
> Upstream identifies the intended source, not necessarily a configured Git remote or automatic synchronization relationship.

## Standards and Inheritance

GitHub provides supported community documents and templates from
this public `.github` repository to other GC-STEM-owned repositories
that do not define their own.

- **Community documents:** May be stored in `.github/`, the repository
  root, or `docs/`. GitHub checks those locations in that order.
- **Issue forms:** Store in `.github/ISSUE_TEMPLATE/`.
- **Discussion forms:** When provided, store in
  `.github/DISCUSSION_TEMPLATE/`.
- **Single pull request template:** Store in
  `.github/pull_request_template.md`.
- **Overrides:** Repository-specific files take precedence. A
  repository's own issue templates or issue-template configuration
  replace the default issue-template set.
- **Local copies:** GitHub displays inherited defaults without adding
  them to the receiving repository. They are not included in its
  clones or downloads.
- **CS course templates:** `crs000` supplies initial course structure
  and configuration. Later changes do not propagate automatically.
- **Wikis:** Maintained independently and never inherited automatically.
- **Student-owned repositories:** GC-STEM defaults do not automatically
  apply.

The issue forms in `.github/ISSUE_TEMPLATE/` serve this repository
and provide defaults for eligible GC-STEM repositories. Root-level
`ISSUE_TEMPLATE/` files do not provide default issue forms.

Keep required course materials and approved alternatives in the
course repository or official learning environment. Required local
guidance must be included explicitly in the course repository.

`LICENSE`, `CODEOWNERS`, `.gitattributes`, `.editorconfig`, and GitHub
Actions workflows are not inherited through this mechanism. Manage
required copies separately.

See [GitHub's default community health file documentation](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).

## Ownership and Governance

Changes belong in the repository that owns the affected resource:

- **STEM-wide community standards:** `.github`
- **Shared STEM documentation:** `.github.wiki`
- **CS master templates and configuration:** `crs000`
- **Shared CS documentation:** `crs000.wiki`
- **Course-specific resources:** Applicable `csXXX` repository or wiki
- **Student work:** Student-owned repositories and development environments

Changes should be proposed through pull requests, reviewed by the
appropriate maintainers, and validated before adoption.

Institutionally controlled materials require applicable approvals,
including SNHU General Counsel for licensing, Marketing for branding,
and designated academic authorities for instructional content.

Shared standards must not silently overwrite course-specific content,
approved exceptions, or student work.

## Access and Maintenance

The `.github` repository remains public to support GitHub's organization-wide
defaults. Repository write access is controlled by authorized GC-STEM
maintainers.

Students access course materials through their course repositories.
Their coursework may also be completed and submitted without GitHub,
using supported development environments and Brightspace.

**Goal:** Consistent, accessible, secure, and maintainable repository
standards with clear ownership and minimal duplication.
