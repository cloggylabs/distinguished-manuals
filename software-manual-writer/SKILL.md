---
name: software-manual-writer
description: Analyzes a software project's source code, docs, and running application to produce a complete manual covering both the technical perspective (architecture, setup, APIs, code structure) and the product perspective (what it does, who it's for, user flows, value proposition) — illustrated with architecture/flow diagrams and real screenshots, not just text. Use this whenever someone asks to document a codebase or product, write a user guide, technical manual, onboarding doc, README overhaul, "how does this thing work" writeup, or developer/product handbook — for engineers, new hires, stakeholders, or customers. Trigger even if they only say "docs," "guide," or "write-up," and even if they ask for only the technical or only the product half of this — still produce the other half too, unless they explicitly decline it. Works with any coding agent that can read files, run shell commands, and optionally take screenshots; does not depend on any single vendor's tools.
---

# Software Manual Writer

Most documentation fails because it's written from one angle only: engineers write
API references nobody outside the team can use to understand *why* the product
exists, and product writers write feature tours that go silent the moment a reader
needs to actually set the thing up. This skill produces a single manual that holds
both angles together, and backs claims with diagrams and screenshots instead of
prose alone — a reader should be able to see the thing, not just read about it.

## Before you start: scope the manual

Default to producing the full manual (technical + product + diagrams + screenshots)
unless the request clearly narrows it. Don't stop to ask permission for the default —
only ask if something is genuinely ambiguous, such as:

- The project has no running UI (e.g. a library or CLI) — confirm whether "product
  perspective" should mean "the experience of the developer using this library/CLI"
  instead of end-user screenshots.
- There are multiple distinct products/apps in one repo — ask which one(s) to cover.
- You have no way to run or screenshot the app at all (see "If you can't run the
  app" below) — say so and proceed with everything else rather than blocking.

Figure out the audience implicitly from the request ("onboarding doc for new
engineers" vs. "guide for customers") — it changes emphasis, not which sections you
include. Keep both perspectives in every manual; audience shifts how much space
each gets.

## Workflow

1. **Technical discovery** — read the code, manifests, configs, and tests to
   understand architecture, setup, and APIs. Details in
   `references/technical-analysis.md`.
2. **Product discovery** — figure out what the thing actually does for a user and
   why it exists, from docs, UI copy, and (if possible) using it. Details in
   `references/product-analysis.md`.
3. **Run it and capture screenshots** — if the project has any runnable UI, start it
   and capture real screens of the key flows you described in step 2. Details in
   `references/screenshots.md`.
4. **Build diagrams** — turn the architecture and the key user/data flows into
   Mermaid diagrams. Details in `references/diagrams.md`.
5. **Assemble the manual** — combine findings into the output structure below,
   using `assets/manual-template.md` as the starting skeleton.
6. **Flag gaps honestly** — if something couldn't be verified (no way to run the
   app, an API with no docs and no obvious callers, etc.), say so in the manual
   instead of guessing. A manual that's honestly incomplete is more useful than one
   that's confidently wrong.

Do steps 1 and 2 largely in parallel in your own investigation — product
understanding should inform which code paths matter, and reading the code often
reveals product behavior that marketing copy or READMEs never mention (e.g. a
feature flag gating something not in any doc).

## Output structure

For most projects, write to a `docs/` folder (create it if absent) so the manual
can live alongside the code and be updated later:

```
docs/
  MANUAL.md              # the manual itself
  diagrams/
    architecture.md       # or .mmd — mermaid source, one file per diagram
    <flow-name>.md
  screenshots/
    <screen-name>.png
```

Embed diagrams as fenced ` ```mermaid ` blocks directly in `MANUAL.md` (most
renderers — GitHub, GitLab, many editors — render these inline) rather than only
linking out to the `diagrams/` copies; keep the `diagrams/` files as the editable
source of truth. Reference screenshots with relative markdown image links
(`![Dashboard view](screenshots/dashboard.png)`).

If the user asked for a single file instead of a folder (e.g. "just give me a
markdown file"), inline everything into one document but still save screenshots as
real image files next to it — never describe a screenshot in words as a
substitute for showing it.

Follow `assets/manual-template.md` for section order and headings, adapting
section weight to the audience you inferred, but keep every section unless the
user explicitly asked you to drop it.

## If you can't run the app

Not every environment can start a server, open a browser, or has display/screenshot
capability. If so:

1. Still write the full technical and product sections — these come from code and
   docs, not from running anything.
2. In place of screenshots, note explicitly in the manual: "Screenshots not
   captured — \<reason\>. Replace the placeholders below once run locally." Leave a
   markdown image placeholder with a descriptive alt text and filename so a human
   can drop the real file in later without restructuring anything.
3. Never fabricate a description of what a screen "would look like" and present it
   as if it were observed — guesses belong in prose clearly marked as inference,
   not in a caption implying you saw it.

## Quality bar

Before considering the manual done, check it against:

- Could someone with zero context on this project get it running from the setup
  section alone?
- Could a non-technical stakeholder read the product section and explain in one
  sentence what the product is for and who uses it?
- Does every major component in the architecture diagram actually correspond to
  something you found in the code (no invented boxes)?
- Is every screenshot real, current, and actually showing what its caption claims?
- Would someone reading only the technical half, or only the product half, still
  get something complete — rather than half a document?
