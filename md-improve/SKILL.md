---
name: md-improve
description: Repair Markdown syntax and document structure in user-specified files while preserving all content; use for rendering issues in lists, emphasis, formulas, links, and other Markdown constructs, not for rewriting or fact-checking.
---

---
name: md-improve
description: Repair Markdown syntax, rendering, and document structure in user-specified files, including web-extracted content, while strictly preserving original content. Do not rewrite, summarize, translate, or fact-check.
---

# Markdown Improvement

Inspect user-specified Markdown files and repair malformed syntax, escaping, whitespace, and document structure that interfere with intended rendering. Make the smallest necessary changes while preserving all original content, meaning, ordering, and hierarchy. This is structural repair, not content editing or stylistic reformatting.

## Rules

- **Content preservation:** Do not rewrite, summarize, translate, fact-check, correct wording, add, remove, or reorder information. Preserve punctuation, numbers, citations, code, URLs, link destinations, mathematical expressions, and their semantics. Modify only markup and whitespace necessary for unambiguous repairs.
- **Markdown structure:** Repair malformed headings, emphasis, lists, task lists, blockquotes, tables, links, images, references, footnotes, code fences, and mathematical delimiters. Fix indentation, nesting, escaping, and block boundaries without changing intended structure. Preserve valid constructs even when alternative formatting seems preferable.
- **Web extraction artifacts:** Identify and repair unintended escaping, broken line breaks, malformed nesting, HTML conversion artifacts, and invisible or nonstandard whitespace that disrupt rendering. Restore escaped list markers when clearly intended as lists, but preserve literal examples and code. Never normalize characters or decode entities indiscriminately.
- **Context-sensitive formatting:** Distinguish actual Markdown syntax from literal characters, code, currency symbols, and mathematical notation. Handle interactions involving parentheses, Korean particles, and emphasis delimiters; use `<strong>...</strong>` for bold text containing parentheses followed immediately by a Korean particle when necessary for reliable rendering. Preserve the exact enclosed text.
- **Renderer compatibility:** Respect the document's intended Markdown dialect and renderer, defaulting to GitHub Flavored Markdown when unspecified. Preserve valid HTML, MDX, JSX, and renderer-specific extensions. Repair mixed Markdown/HTML and mathematical markup only when the intended interpretation is clear.
- **File integrity:** Modify only specified files. Preserve filenames, paths, YAML front matter, metadata, encoding, line endings, and meaningful whitespace where practical. Do not reformat unaffected sections or modify linked files.
- **Ambiguity:** Infer intended markup from surrounding context, but never invent missing content or make speculative structural changes. Leave uncertain constructs unchanged and report them.

## Workflow

1. Inspect the files, identify rendering problems and extraction artifacts, and determine the intended Markdown dialect when possible.
2. Apply minimal, localized repairs while protecting content and avoiding unrelated formatting changes.
3. Review the diff to verify that edits affect only necessary markup and whitespace, preserving text, code, links, formulas, and document hierarchy.
4. Where suitable tools are available, validate parsing and rendering with a compatible renderer. Check for regressions and ensure repeated execution produces no further changes (idempotency).
5. Report modified files, repair categories, unresolved ambiguities, and validation limitations concisely.

Prioritize content preservation over rendering improvements whenever they conflict. Do not make changes solely for stylistic consistency.