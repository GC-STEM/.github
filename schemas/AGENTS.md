# Schema maintenance

These instructions apply to schemas and supporting materials in this
directory and its descendants. Read the [root agent guide](../AGENTS.md)
and the guidance relevant to the affected files before editing.

Treat each schema family as a distinct contract. Shared maintenance
practices do not make the current manifest's application rules universal
requirements for future schemas.

## Establish the contract

- Identify the schema's purpose, owner, intended documents, consumers,
  declared dialect, identifiers, and compatibility requirements.
- Read its descriptions, comments, references, examples, tests, and
  available specifications. Consult `schemas/README.md` or family-specific
  documentation when present.
- For `manifest.schema.json`, inspect the documented Atlas and course
  consumers. This repository owns the shared schema; Atlas and course
  repositories own their respective implementations and configuration.
- Distinguish implemented requirements from proposals, examples, migration
  plans, and provisional decisions.
- Keep human-facing usage and contract documentation in the relevant README
  or specification. Keep this guide focused on agent working practices.
- Identify cross-repository effects without silently expanding the task
  into consumer implementations, provisioning, or institutional policy.

## Preserve compatibility and identity

- Preserve the declared `$schema` dialect unless changing it is part of
  the task. Verify that intended validators and consumers support any
  introduced keywords or vocabulary.
- Distinguish the JSON Schema dialect, schema resource identity, schema
  release version, and instance or application version. Follow established
  conventions for each schema family rather than inventing a shared
  versioning policy.
- Treat changes to property names, required fields, types, constants,
  enumerations, bounds, patterns, branches, and unknown-property handling
  as potential compatibility changes.
- Assess both documents newly rejected and documents newly accepted whose
  features existing consumers may not support.
- Preserve identifiers, reference targets, and extension points used by
  consumers. Explain intentional changes and their migration implications.
- Avoid imposing the manifest's version numbers, terminology, closed-object
  rules, or deployment assumptions on unrelated schema families.

## Write precise schemas

- Maintain valid JSON without comments, trailing commas, or duplicate keys.
  Use supported annotation keywords for explanatory material.
- Keep requiredness, accepted values, null handling, defaults, and
  unknown-property behavior explicit where the contract requires them.
- Preserve the intended behavior of conditionals and schema combinations.
  Test branch selection and rejection behavior when changing discriminators
  or alternatives.
- Keep descriptions and examples consistent with enforceable constraints.
  Explain important restrictions and permitted extension mechanisms.
- Treat `default`, descriptions, examples, and comments according to their
  declared semantics. Ordinary validation does not automatically populate
  missing values, merge documents, or implement application workflows.
- When a contract depends on `format` assertions or other configurable
  behavior, verify the actual validator's support and settings.
- Use synthetic examples and fixtures. Exclude credentials, student records,
  private coursework, answer keys, and restricted assessment materials.

## References and application boundaries

- Preserve correct `$id`, `$ref`, and other reference-resolution behavior
  for the declared dialect. An identifier is not automatically a requirement
  to fetch a remote document.
- Keep validation reproducible using the project's established reference
  registry, local resources, or controlled dependencies. Investigate
  unresolved references rather than silently ignoring them.
- Distinguish structural validation from semantic rules enforced by
  consumers, including cross-document relationships, authorization,
  composition, dependency resolution, and environment readiness.
- A document passing its schema does not establish that referenced
  resources exist or that provisioning, enrollment, submission, or grading
  will succeed.
- Metadata describing approval, permissions, or submission requirements
  does not itself enforce those requirements. Verify the responsible
  implementation or report the verification gap.

## Validate schema changes

Use the environment and repository checks documented in the root guide and
[CI guidance](../.github/ci/README.md). Run commands from the repository root.

```bash
python .github/ci/check_repository.py
```

This command provides repository and configuration checks. Its JSON parsing
does not by itself establish schema correctness or instance compatibility.

For schema contract changes:

1. Validate the schema against the meta-schema appropriate to its declared
   dialect using an available, compatible validator.
2. Resolve applicable references and verify required keyword support,
   including any relevant format-assertion configuration.
3. Test representative valid documents and documents expected to fail.
   Include relevant missing fields, wrong types, boundary values,
   discriminator errors, and unknown-property cases.
4. Exercise changed conditional branches and shared definitions, including
   other branches affected by a reused definition.
5. Check compatibility with representative existing documents and the
   intended consumers where available.
6. Inspect failures for the intended reason; an unrelated error does not
   demonstrate that a changed constraint works.

Use existing fixture locations and test conventions. Add focused behavioral
coverage when changing a contract. Documentation-only edits do not require
new instance-validation tests unless they change executable examples or
documented behavior.

Inspect current tooling and workflows before claiming coverage. If
schema-specific validation is unavailable, report that limitation and the
checks actually performed. Do not invent an existing validation command or
treat an unavailable check as passing.

When adding validation tooling within the task's scope, document its
dependencies, dialect support, reference handling, fixture expectations,
and invocation. Consult automation instructions for changes under
`.github/ci/` or `.github/workflows/`.

## Additional schema families

- Give new schemas a clear purpose, owner, consumer, and documented contract.
  Reuse definitions only when their meaning and evolution are genuinely
  shared.
- For assignment schemas, distinguish GC-STEM's internal assignment model
  from any actual GitHub Classroom or other platform interface.
- Verify platform compatibility against the relevant official specification
  and implemented integration before claiming it. Similar terminology or
  field names do not establish compatibility.
- Keep assignment requirements, grading rules, and institutional decisions
  grounded in their authoritative sources.
- Add more specific agent guides only when a schema family develops a
  substantially different working process.

## Formatting and completion

- Follow [`.gitattributes`](../.gitattributes) and
  [`.editorconfig`](../.editorconfig). JSON currently uses LF; preserve the
  applicable Markdown settings. Avoid unrelated reformatting or EOL changes.
- Preserve the tested course-submission policy when changing any
  course-bound output. Validate final artifacts separately when applicable.
- Update affected descriptions, examples, fixtures, documentation, and
  references together.
- Report the contract changes, compatibility assessment, affected consumers,
  checks performed, and remaining validation or migration gaps.
- Keep temporary findings in the completion report rather than accumulating
  unresolved issue narratives in this guide.
