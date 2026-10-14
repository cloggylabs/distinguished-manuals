<!--
Starting skeleton for MANUAL.md. Adapt section weight to the audience
(e.g. a customer-facing guide spends more words on "What it does" and less on
"Code structure"; an engineering onboarding doc is the reverse) — but keep every
section present unless the user explicitly asked you to drop one. Remove this
comment block in the final output.
-->

# <Project Name> Manual

_One or two sentences: what this is, in plain language, before anything else._

## Table of contents

- [What it does](#what-it-does)
- [Who it's for](#who-its-for)
- [Key user flows](#key-user-flows)
- [Architecture overview](#architecture-overview)
- [Getting started](#getting-started)
- [API / interface reference](#api--interface-reference)
- [Code structure](#code-structure)
- [Known gaps](#known-gaps)

---

## What it does

<The one-sentence value proposition from product discovery, expanded into a short
paragraph. What problem does it solve, and what does it replace or sit alongside?>

## Who it's for

<The audience(s)/role(s), and what differs between them (e.g. admin vs. member,
free vs. paid tier). If there's one primary audience, say so plainly instead of
hedging across several.>

## Key user flows

<For each of the 3-6 flows identified in product discovery:>

### <Flow name>

<What the user is trying to accomplish, in one sentence.>

1. <Step, with a screenshot if a UI exists for this step>
2. <Step>
3. <Step>

![<Screen name>](screenshots/<screen-name>.png)
_<Caption: what this screenshot shows and which step it corresponds to>_

<Repeat for each flow. Add a flowchart/sequence diagram here instead of, or in
addition to, screenshots when the flow has branches or multiple actors — see
references/diagrams.md.>

## Architecture overview

<Short paragraph orienting the reader, then the diagram:>

```mermaid
flowchart LR
  %% Replace with the real architecture found during technical discovery
```

<Then a short walkthrough of each major component in the diagram: what it is,
what it's responsible for, and what it talks to.>

## Getting started

### Prerequisites

<Runtimes, versions, accounts/credentials, external services needed.>

### Install

```bash
<real commands found in the manifest/scripts>
```

### Configure

<Required environment variables / config, with what each one is for.>

### Run

```bash
<real run command>
```

### Test

```bash
<real test command>
```

## API / interface reference

<For a service: the main endpoints, with method, path, purpose, and
request/response shape. For a library: the main public functions/classes. Link
to a fuller auto-generated spec if one exists rather than duplicating it
entirely.>

## Code structure

<Short map of "where things live" — directory by directory, one line each,
focused on what a newcomer actually needs to navigate, not an exhaustive file
listing.>

```
src/
  api/        <what lives here>
  domain/     <what lives here>
  ...
```

## Known gaps

<Anything you couldn't verify, couldn't run, or had to scope out — stated plainly
so the reader knows the boundaries of what this manual covers. Delete this
section only if there genuinely are no gaps.>
