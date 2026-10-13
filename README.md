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
| 2 | GC-STEM | [`cs000.git`](https://github.com/GC-STEM/cs000) | Master template and configuration for CS course repositories | `.github.git` (community standards only) | Public |
| 2 | GC-STEM | [`cs000.wiki`](https://github.com/GC-STEM/cs000/wiki) | Supplemental documentation shared across CS courses | None | Public |
| 3 | GC-STEM | `csXXX.git` | Course content, required documentation, and configuration (`cs100`–`cs999`) | `GC-STEM/cs000.git` (template) | Public |
| 3 | GC-STEM | `csXXX.wiki` | Course-specific supplemental documentation | None | Public |
| 4 | Student | `csXXX.git` | Student-owned online copy of a course repository | `GC-STEM/csXXX.git` | Private |
| 5 | Student | `~/Repos/csXXX` | Local clone of the student's repository | `student/csXXX.git` | Local |

> [!NOTE]
> Upstream identifies the intended source, not necessarily a configured Git remote or automatic synchronization relationship.

## Standards and Inheritance

GitHub automatically provides supported community standards and templates
from this public `.github` repository to other GC-STEM-owned repositories
that do not define their own.

- **Defaults:** Applied by GitHub without copying files downstream.
- **Overrides:** Repository-specific community files take precedence.
- **Templates:** `cs000` supplies initial CS course structure and
  configuration; subsequent changes do not propagate automatically.
- **Wikis:** Maintained independently and never inherited automatically.
- **Student repositories:** GC-STEM defaults do not automatically apply
  to repositories owned by students.

Other files, including `LICENSE`, `CODEOWNERS`, `.gitattributes`,
`.editorconfig`, and GitHub Actions workflows, are not inherited through
GitHub's community standards mechanism. Required copies must be managed
separately.

See [GitHub's default community health file documentation](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).

## Ownership and Governance

Changes belong in the repository that owns the affected resource:

- **STEM-wide community standards:** `.github`
- **Shared STEM documentation:** `.github.wiki`
- **CS master templates and configuration:** `cs000`
- **Shared CS documentation:** `cs000.wiki`
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
