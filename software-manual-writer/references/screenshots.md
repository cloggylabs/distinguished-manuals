# Capturing screenshots

A manual that only describes a UI in words is strictly worse than one that shows
it — capture real screenshots of the real running app whenever any capability
exists to do so. Never invent a description of a screen and present it as if it
were observed; if you can't capture it, say so (see SKILL.md § "If you can't run
the app").

This skill doesn't assume any specific tool for this — different agents have
different capabilities. Use whichever of the following you actually have access
to, in roughly this order of preference:

1. **Browser automation** (if the agent has a browser/web-automation capability):
   start the app's dev server, navigate to each key screen identified in product
   discovery, and capture a screenshot of each. Prefer capturing after the page
   has fully loaded and any loading spinners/skeletons are gone — a screenshot of
   a loading state is misleading as documentation.
2. **Headless browser via a scriptable tool already in the project or ecosystem**
   (e.g. a Playwright/Puppeteer-style CLI, if the project already depends on one or
   one is trivially available) — run it to open the relevant URL and save a
   screenshot to a file. Only reach for installing a new heavy dependency if the
   user's environment clearly allows it; otherwise prefer a lighter approach or
   ask.
3. **OS-level screenshot capability**, if the agent can control the desktop/take
   screen captures directly — run the app, bring it to the foreground, capture.
4. **Ask the user** to run the app and share screenshots, if none of the above is
   available and the app genuinely needs visual documentation (e.g. it's a
   graphical desktop app with no web view). This is a legitimate outcome, not a
   failure — say clearly what you need and why.

If none of these apply and asking isn't practical, fall back to the placeholder
approach described in SKILL.md rather than guessing.

## Practical tips

- **Start the app for real.** Follow the setup instructions you just wrote in the
  technical section — if they don't actually work, that's a bug in the manual to
  fix before anything else, not something to route around.
- **Wait for real content.** Seed/demo data beats an empty state for most
  screenshots, unless the empty state itself is part of the flow you're
  documenting (e.g. first-run onboarding).
- **One screenshot per meaningfully distinct screen/state**, not one per pixel of
  scroll. Capture the state that best shows what that step of the flow is for.
- **Crop/frame sensibly** if your tool allows it — a full 4K desktop screenshot
  with a tiny browser window in the corner is worse than a tightly framed capture
  of just the app viewport.
- **Redact or avoid real secrets/PII.** If seed data contains anything sensitive
  (API keys, real-looking emails, tokens visible in the UI), use a different
  account/dataset or blur/crop it out rather than publishing it in the manual.
- **Naming convention**: `docs/screenshots/<flow-or-screen-name>.png`, lowercase,
  hyphenated, matching the heading it illustrates in `MANUAL.md` — this makes it
  obvious at a glance which screenshot belongs to which section.
- **Caption every screenshot** with what it shows and, if relevant, what step of
  the flow it represents — a bare image with no caption loses most of its value.

## For CLIs / libraries / APIs

Capture real terminal output or a real request/response instead of a UI
screenshot: actually run the command or make the call, copy the real output
verbatim into a fenced code block. The same honesty rule applies — don't
hand-write plausible-looking output from memory.
