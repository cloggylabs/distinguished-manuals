# Product discovery checklist

Goal: understand what the product *does for someone* and *why it exists* — the
half of the manual that a pure code read-through will never fully surface, because
intent and audience live in copy, design, and usage, not just logic.

## Where to look

1. **User-facing copy**: landing/marketing pages, in-app onboarding text, empty
   states, tooltips, pricing pages. This is usually the clearest statement of the
   value proposition and target audience — often better than any internal doc,
   since it was written to persuade a real outside reader.
2. **Docs aimed at end users**: a `docs/` site, help center, in-app help, FAQ.
   Distinguish these from developer docs — they describe workflows from the user's
   point of view, in the user's vocabulary, not the code's.
3. **The UI itself, actually used**: if you can run the app (see
   `screenshots.md`), click through the primary flows — sign-up/first-run,
   the core action the product exists for, and whatever produces the main
   value (a dashboard, a generated artifact, a completed transaction). Note
   what each screen is for in plain language, not component names.
4. **Issue tracker / changelog / release notes**, if accessible — these reveal
   what users actually struggle with and what the team considers worth shipping,
   which is a good signal for "what matters most to explain."
5. **Code as a secondary product signal**: feature flags, role/permission checks,
   and pricing-tier gates in the code often reveal product segmentation (free vs.
   paid, admin vs. member) that marketing copy glosses over or doesn't mention yet.

## What to produce from this

- **One-sentence value proposition**: what does this do, for whom, instead of
  what? If you can't state this in one sentence after discovery, that's a sign you
  need to look further, not a sign to write a vague paragraph instead.
- **Audience / user roles**: who uses this and what do the different roles
  actually see/do differently? (e.g. admin vs. end user, free vs. paid tier)
- **Key user flows**: the 3-6 journeys that matter most (first-run/onboarding, the
  core value-generating action, and anything else central) — described step by
  step, each illustrated with a real screenshot if a UI exists for it (see
  `screenshots.md`) and optionally a flow diagram (see `diagrams.md`) for anything
  with branches or multiple actors.
- **What it's not**: if there's a clear boundary (e.g. "this isn't a replacement
  for X, it integrates with X"), state it — this is often the fastest way to
  orient a new reader and prevent them forming the wrong mental model.

## For products without a visual UI (libraries, CLIs, APIs)

"Product perspective" still applies — the "product" is the developer experience.
Treat the equivalent of a user flow as: install → first successful call/command →
the core thing it's good for → a non-trivial real use case. Screenshots become
terminal output / usage examples instead of UI screens — capture real output by
actually running the commands, don't hand-write example output from memory.

## Judgment calls

- Don't just restate the README's marketing blurb — verify it against what the
  product actually does when used. Copy can be aspirational or stale.
- If the product clearly serves multiple very different audiences (e.g. a
  platform with both an admin console and a public API), give each its own
  mini value-proposition and flow set rather than merging them into one generic
  narrative.
- Resist writing feature lists. A list of features is not a product
  understanding — describe flows and outcomes, and let features emerge as
  supporting detail within them.
