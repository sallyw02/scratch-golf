# Scratch

Scratch is a lightweight CRM for independent golf coaches: students, a lesson calendar, post-lesson notes, follow-up threads and a "needs attention" list. Only Coaches sign in. Stack is Next.js (TypeScript), Supabase (Postgres and auth), Drizzle ORM, Tailwind with shadcn/ui, and Vercel.

Before starting work, read:
- `CONTEXT.md` for domain terms. Use its words in code, UI and commits (Lesson, never "booking").
- `docs/adr/` before changing architecture, data access, auth or email.
- `PROJECT_CONTEXT.md` for scope, priorities and how Sally wants to work.

## Codebase map

Planned layout. Update this section when the scaffold lands.

- `src/app/` holds pages, and `src/app/api/` holds the REST route handlers. Pages call these endpoints (ADR 0003).
- `src/db/schema.ts` is the single source of truth for tables.
- `src/db/queries/` is the only code that touches the database. Every function takes a `coachId` (ADR 0002).
- `src/lib/email.ts` holds the one send function. It writes to the outbox table (ADR 0005).
- `src/lib/needs-attention.ts` holds the Needs Attention rule as a pure function.
- `tests/e2e/` holds Playwright tests. Unit tests sit next to the code as `*.test.ts`.
- `drizzle/` holds generated migrations, and `supabase/` holds local Supabase config used in CI.

## Build and test commands

npm and Node 24. The scripts in `package.json` are the source of truth. The core loop is:

- `npm run dev` starts the app at localhost:3000.
- `npm run lint` and `npm run typecheck` must pass before any commit.
- `npm test` runs Vitest unit tests, and `npm run test:e2e` runs Playwright.
- `npm run db:generate` creates a migration after a schema change, and `npm run db:migrate` applies it. Commit the schema change and its migration together.

Work one ticket per branch, opened as a PR against `main`. Build features test-first with `/tdd`. When a prompt is notable by the rules in `PROMPT_LOG.md`, offer to add an entry.

## Code style

Follow `CODING_STANDARDS.md`, including its Next.js section. `/code-review` checks every PR against that file, so new rules go there, not here.

## Testing and running the app

To spin up the app locally:

1. Copy `.env.example` to `.env.local` and fill in the dev Supabase project values. Ask Sally for them.
2. `npm install`
3. `npm run db:migrate`, then `npm run db:seed` to load test Coaches and Students.
4. `npm run dev`, then sign in as a seeded Coach. Credentials live in the seed file.
5. Check sent emails at `/outbox`.

Every main flow (add a Student, schedule a Lesson, send a Lesson Note, reply through a Follow-up Thread link) has a Playwright test. Each new endpoint gets a test proving that a second Coach cannot read or change the first Coach's data. CI runs everything against a fresh local Supabase.

## Security

- Secrets live only in `.env.local` and Vercel environment settings. Never write keys, passwords or connection strings into any tracked file, including this one and `PROMPT_LOG.md`.
- The Supabase service role key is server-only and never reaches client code.
- All database reads and writes go through `src/db/queries/` with the signed-in Coach's ID taken from the session, never from the request body.
- Student reply links use long random tokens, and the reply endpoint exposes only that one Follow-up Thread.
- All email goes through `src/lib/email.ts`. Supabase and Resend are the only external services. Ask Sally before adding another API, including any LLM API.
- Seed and test data use made-up names and `example.com` emails only.
