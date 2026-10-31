---
applyTo: "README.md,ACCESSIBILITY.md,CODE_OF_CONDUCT.md,CONTRIBUTING.md,SECURITY.md,SUPPORT.md,LICENSE,profile/**,docs/**,.github/ISSUE_TEMPLATE/**,.github/PULL_REQUEST_TEMPLATE/**,.github/pull_request_template.md,.github/DISCUSSION_TEMPLATE/**,.github/VULNERABILITY_REPORT.yml,.github/VULNERABILITY_REPORT.yaml"
---

# Community content

Supplement the [repository-wide instructions](../copilot-instructions.md)
with these practices for community documents, public information,
educational resources, and contribution forms.

## Audience and authority

- Write for the audience and task at hand: administrators, developers,
  maintainers, faculty, and current or prospective students. Introduce
  separate audience sections only when their next steps differ.
- Explain unfamiliar GitHub concepts when needed. Distinguish ownership,
  access, responsibilities, and contribution opportunities without
  assuming that a reader's affiliation grants repository permissions.
- Follow the authority and ownership described in
  [README.md](../../README.md). Preserve course-specific requirements,
  approved alternatives, and existing collaboration and AI rules.
- Keep institutional policies, legal notices, branding, and academic
  requirements consistent with their authoritative sources. Preserve
  documented approval and provisional status.
- Verify current institutional claims and GitHub behavior before changing
  them. Link to authoritative information instead of duplicating details
  likely to change.
- Resolve placeholders within the assigned scope using verified information.
  Preserve meaningful draft notices until the documented readiness or
  approval conditions have been met.

## Clear and accessible documentation

- Follow [ACCESSIBILITY.md](../../ACCESSIBILITY.md). Use descriptive
  headings, meaningful link text, short paragraphs, and direct language.
  Expand unfamiliar abbreviations on first use.
- Provide meaningful alternative text for informative images and a text
  explanation of complex diagrams. Supply appropriate captions,
  transcripts, and descriptions for instructional media.
- Communicate meaning through text as well as color or emoji. Use simple
  tables with clear headers for data, rather than page layout.
- Present commands, code, and error messages as selectable text.
  Identify prerequisites, operating system, shell, working directory,
  placeholders, and expected results when relevant.
- Separate commands from example output. Label code fences accurately,
  and keep runnable commands free of copied prompt characters.
- Explain the purpose and consequences of a GitHub practice when that
  helps readers decide what to do. Keep essential guidance usable without
  Copilot, an AI subscription, or access to an optional wiki.

## Community policies and support routes

- Keep reporting and contribution guidance aligned with
  [CONTRIBUTING.md](../../CONTRIBUTING.md) and
  [SUPPORT.md](../../SUPPORT.md). Distinguish asking for help, reporting
  a problem, suggesting an improvement, and proposing file changes.
- Preserve documented alternatives for people who cannot use GitHub,
  lack access, or need private assistance.
- Keep forms proportionate to the report. Require only information needed
  to begin triage. Allow uncertainty and incomplete technical details.
  Avoid requiring reporters to diagnose the problem or propose a solution.
- For accessibility reports, accept a description of the barrier without
  requiring a diagnosis, accommodation documentation, screenshots,
  assistive-technology expertise, or a WCAG classification.
- Direct academic and personal matters through the documented course or
  institutional channels. Keep security and conduct concerns aligned with
  their designated private reporting routes.
- Public forms and examples must avoid collecting credentials, student
  records, grades, private feedback, medical information, completed
  solutions, or restricted assessment materials.
- Preserve existing response expectations. Do not invent service
  guarantees, deadlines, academic exceptions, or promises of acceptance.

## Organization profile and educational resources

- Use `profile/README.md` as a welcoming directory for public visitors.
  Make useful next steps clear for current and prospective students
  and faculty, while keeping maintainer guidance discoverable.
- Link to official SNHU sources for programs, admission, tuition,
  financial aid, employment, policies, and institutional support.
  Label resources requiring authentication.
- Describe public repositories accurately. Examples and supplemental
  resources do not establish current curriculum, assessment requirements,
  enrollment eligibility, or access to restricted materials.
- Distinguish published guidance from examples, internal notes, scaffolds,
  and planned capabilities in `docs/`. Keep required course materials
  with the owning course or official learning environment.

## Portable templates and forms

- Check each format against its current GitHub specification. Issue forms,
  discussion forms, PR templates, and vulnerability-report forms have
  different supported metadata and behavior.
- Preserve valid YAML structure, supported field types, descriptive labels,
  and unique field IDs where required. Keep examples relevant to the
  report rather than assuming a particular application stack.
- Verify destination compatibility before introducing labels, assignees,
  projects, issue types, or discussion categories into shared defaults.
  Labels referenced by inherited issue forms must exist in each receiving
  repository. Discussion-form filenames must match their category slugs.
- Confirm that the documented entry point selects the intended PR template.
  Distinguish an automatic single template from named templates requiring
  explicit selection.
- Evaluate links in the context where inherited content will appear.
  Use explicit central-policy URLs when receiving repositories may lack
  the referenced files; retain relative links for content actually present
  at the intended destination.
- Check the effects of shared-template changes on receiving repositories
  and their overrides. Keep repository-specific assumptions out of shared
  defaults unless their applicability is documented.
- Describe reports as public or private according to the actual feature
  and repository visibility. Keep vulnerability details in the designated
  private reporting process.

## Review and validation

- Preserve the current formatting and EOL rules. Documentation edits do
  not introduce an infrastructure EOL migration or alter the tested
  course-submission policy.
- Update affected headings, navigation, anchors, template descriptions,
  and cross-references together.
- Use the relevant documentation, configuration, shell-example, and link
  checks from the repository-wide instructions and
  [CI guidance](../ci/README.md).
- Review rendered Markdown and form behavior where available, including
  required fields, link destinations, privacy language, and accessibility.
  Successful YAML parsing alone does not establish GitHub form validity.
- Report checks performed and remaining limitations. Distinguish syntax
  validation, functional verification, accessibility review, and link
  checking; keep temporary findings out of permanent instructions.
