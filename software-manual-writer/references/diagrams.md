# Building diagrams

Use [Mermaid](https://mermaid.js.org/) as the default diagram syntax: it's plain
text (reviewable in a diff, editable by hand), and renders natively in GitHub,
GitLab, most modern editors, and many documentation tools — making it the most
portable choice across the different environments this skill's output might end
up in. If the target renderer is known not to support Mermaid, fall back to plain
ASCII-art diagrams in a fenced code block rather than an undisplayable format.

Only draw a diagram where it earns its place — a diagram that just restates a
sentence in boxes is noise. Draw one when there are genuinely multiple components,
actors, or branches whose *relationships* are the point (that's exactly what's
hard to follow in prose).

## Which diagrams to produce

- **Architecture diagram** (almost always, if there's more than one component):
  a `flowchart` or `graph` showing the major services/modules and how they
  connect — sync calls, async/queue messages, shared datastores, external
  dependencies. Base every box strictly on something you actually found in the
  code/config during technical discovery (see `technical-analysis.md`) — never add
  a component because it's "typical" for this kind of system.

  ```mermaid
  flowchart LR
    Client -->|HTTPS| API[API Server]
    API --> DB[(Database)]
    API -->|publishes| Queue[[Message Queue]]
    Queue --> Worker[Background Worker]
    Worker --> DB
  ```

- **Sequence diagram** for any flow involving multiple actors/services talking to
  each other over time (e.g. auth, checkout, a webhook callback) — this is where
  prose gets hardest to follow and a diagram pays off most.

  ```mermaid
  sequenceDiagram
    actor User
    participant Frontend
    participant API
    participant AuthProvider
    User->>Frontend: Clicks "Log in"
    Frontend->>AuthProvider: Redirect for auth
    AuthProvider->>Frontend: Returns token
    Frontend->>API: Request with token
    API->>Frontend: Authenticated session
  ```

- **Flowchart** for a user journey with decision points (e.g. onboarding with a
  branch for "already has an account").

  ```mermaid
  flowchart TD
    Start[User signs up] --> Verify{Email verified?}
    Verify -->|Yes| Onboard[Onboarding wizard]
    Verify -->|No| Reminder[Verification reminder]
    Reminder --> Verify
    Onboard --> Dashboard[Main dashboard]
  ```

- **Entity-relationship diagram**, only if the data model is central to
  understanding the product (e.g. a multi-tenant system where the tenancy model
  is the whole point) — don't reproduce the full schema if it's large; show the
  handful of entities that matter for understanding the system.

  ```mermaid
  erDiagram
    USER ||--o{ ORDER : places
    ORDER ||--|{ LINE_ITEM : contains
    PRODUCT ||--o{ LINE_ITEM : "ordered as"
  ```

## Keeping diagrams readable

- Cap at roughly 8-10 nodes per diagram. A real system with more components than
  that needs multiple diagrams at different zoom levels (e.g. one overall
  architecture diagram, plus one detailed sequence diagram per complex flow)
  rather than one unreadable mega-diagram.
- Label edges with what actually flows across them (`places order`, `publishes
  event`), not generic arrows — the label is often the most informative part.
- Keep names in diagrams consistent with the names used in the surrounding prose
  and in the actual codebase — a diagram using different terminology than the text
  around it is more confusing than no diagram.

## Where to put them

Save each diagram's Mermaid source as its own file under `docs/diagrams/` (e.g.
`architecture.md`, `checkout-flow.md`) as the editable source of truth, and also
embed the same fenced ```mermaid block directly inline in `MANUAL.md` at the point
where it's discussed, so the manual is fully readable without following a link
out.
