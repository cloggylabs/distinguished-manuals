# Technical discovery checklist

Goal: understand how the project is built, how to run it, and how its pieces fit
together — well enough to write setup instructions and an architecture diagram
that an engineer could actually follow.

## Where to look, in order

1. **Root-level docs**: `README`, `CONTRIBUTING`, `ARCHITECTURE.md`, `docs/`,
   `/.github` templates. These often contain setup steps and intent that save you
   from re-deriving everything from source — but verify claims against the actual
   code/config, since docs drift out of date.
2. **Manifests / dependency files**: `package.json`, `pyproject.toml`,
   `requirements.txt`, `Cargo.toml`, `go.mod`, `pom.xml`, `Gemfile`, etc. These tell
   you the language, framework, and major libraries, and usually list the actual
   run/build/test scripts/commands.
3. **Entry points**: look for `main`, `index`, `app`, `server`, `cmd/`,
   `src/main.*` — wherever execution starts. Trace from there to see what gets
   wired up (routers, DB connections, background workers).
4. **Configuration**: `.env.example`, `config/`, `docker-compose.yml`,
   `Dockerfile`, Kubernetes manifests, Terraform/IaC. These reveal required
   external services (databases, queues, third-party APIs) and environment
   variables a setup guide must mention.
5. **API surface**: route definitions, OpenAPI/Swagger specs, GraphQL schemas, gRPC
   `.proto` files, or (for libraries) the public exports/module interface. This is
   the contract other systems or developers rely on — document it precisely,
   including request/response shapes where feasible, not just endpoint names.
6. **Data layer**: schema files, migrations, ORM models — these tell you what the
   system actually persists and often clarify domain concepts better than any
   prose doc.
7. **Tests**: integration and end-to-end tests are a goldmine for understanding
   real behavior and expected flows, often more reliable than comments.
8. **CI/CD**: `.github/workflows`, `.gitlab-ci.yml`, etc. — tells you the real
   build/test/deploy pipeline, which should match (or correct) whatever the README
   claims.

## What to produce from this

- **Setup instructions**: prerequisites, install, configure (env vars, secrets),
  run, test — as commands a reader can copy-paste, not paraphrased summaries.
  Verify each command is one you actually found in a manifest/script/doc, not one
  you're guessing at from convention.
- **Architecture overview**: the major components/services and how they talk to
  each other (sync calls, async/queue, shared DB, etc.) — this becomes the input to
  the architecture diagram (see `diagrams.md`).
- **API reference**: enough for someone to call the main endpoints/functions
  without reading the source — but don't try to exhaustively re-document
  auto-generated specs that already exist; link to them and summarize the
  highlights instead.
- **Code structure map**: a short guide to "where things live" (e.g. "`src/api/`
  holds route handlers, `src/domain/` holds business logic") so a newcomer can
  navigate without a full tour.

## Judgment calls

- If the stack is unfamiliar, don't guess at idioms — grep for how existing code
  in the repo actually does things (e.g. how other endpoints handle auth) and
  describe that, rather than the generic textbook pattern for the framework.
- Large monorepos: scope to the part of the repo relevant to the request rather
  than attempting to document everything at once — but say explicitly what you
  scoped out and why, so the reader knows the manual isn't claiming full coverage.
- When a manifest script and a README instruction disagree, trust the manifest
  (it's what actually executes) and flag the discrepancy rather than silently
  picking one.
