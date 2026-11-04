# Handoff: recreating the Scratch setup for recipe-genie

Sally is switching her CS146S final project from Scratch (a CRM for golf coaches) to a new app called recipe-genie. The product changes, but the documentation depth and AI-native workflow from Scratch should carry over, because the course grades how AI is used across the whole lifecycle. This brief lists what was built and decided in the Scratch repo (/Users/sally/Documents/scratch-golf) so you can recreate the equivalent for recipe-genie. Read the Scratch files directly when you need the exact wording or structure.

Do not copy golf content. Reuse the structure, the process and the generic rules, and rebuild the product-specific parts by asking Sally questions.

## First step: make the Scratch repo permanently readable

Before anything else, give the recipe-genie repo standing read access to Scratch so every future session can open it without a permission prompt. Create or update `.claude/settings.json` in the recipe-genie repo with this, merging into any existing settings rather than overwriting them:

```json
{
  "permissions": {
    "additionalDirectories": ["/Users/sally/Documents/scratch-golf"]
  }
}
```

Explain to Sally what the file does, commit it on its own branch through a PR, and log it in PROMPT_LOG.md if it fits the criteria.

## Which code review skill

Every mention of /code-review in this brief and in the Scratch docs means Matt Pocock's skill, `/mattpocock-skills:code-review`. It reviews a diff against CODING_STANDARDS.md and against the originating issue or spec. Claude Code also has a built-in `/code-review` that hunts for correctness bugs and ignores the standards file. Typing the short name can pick the built-in one, so always write and run the full name. In recipe-genie's CLAUDE.md, CODING_STANDARDS.md and PR workflow, spell it as `/mattpocock-skills:code-review`. The built-in review can still be run as an extra pass, but it is not the one the standards are written for.

## How Sally wants to work

Sally is a beginner with agent harnesses. Explain what you are about to do and why in plain language before doing it, and name any skill you use and what it will produce. Ask before large or hard-to-undo changes and prefer small reviewable steps. Her strongest language is Python, and she is open to TypeScript if you explain the tradeoff. Write concisely in full sentences, avoid em dashes, and keep semicolons and colons to a minimum.

Her global ~/.claude/CLAUDE.md already covers writing style for shared docs and the PR description format, so it applies automatically in the new repo.

## Course requirements that drive everything

The project is a solo MVP for CS146S: The Modern Software Developer (Stanford, fall 2026). It is graded on the working product and on AI use at every stage: prototyping, planning, code generation, testing, review and CI/CD. Sally must keep a log of real prompts showing how her prompting changed, and every change must go through a PR with AI review. The Scratch timeline targeted late November 2026, so time is now tighter than when Scratch started.

## Files to recreate, in the order they were made

1. PROJECT_CONTEXT.md is the first file a new session reads. Scratch's version has these sections: who Sally is and how to work with her, course objectives, the product (problem, target user, use case, working name), MVP features in Priority 1 and 2 plus stretch goals, planned screens, tools, timeline, the prompt log, the Matt Pocock skills workflow, and "Where I am now". Recreate every section with recipe-genie content and keep "Where I am now" current.

2. README.md is short: a one-paragraph product description, the course line, a status line, a repo guide pointing at the other docs, and the workflow rule that every change is a PR reviewed by CodeRabbit and Claude Code.

3. CODING_STANDARDS.md is what /mattpocock-skills:code-review checks against. The general, data and security, testing and PR sections were written stack-agnostic first and are mostly reusable. Small focused functions, code named after glossary terms, no dead code, no committed secrets, a .env.example with placeholders, server-side validation, unit tests for business rules, a Playwright test per main flow, and one ticket per PR all carry over. A stack-specific section was added once the stack was decided. Replace the Scratch rule about coach scoping with recipe-genie's own ownership rule, and replace the email section only if recipe-genie sends email.

4. .gitignore ignores .env and .env.* except .env.example, plus .DS_Store, node_modules, __pycache__ and .venv.

5. PROMPT_LOG.md has an intro, five tests for what counts as a notable prompt, a guide of one to three entries per session, and a fixed entry format with number, title, date, stage, tool, the exact prompt, result, "Changes and why" and links. Copy the intro, criteria and format word for word. Then decide with Sally whether to carry the three Scratch entries over as history. The pivot itself is a notable prompt and should be logged as a new entry, because it is a scope decision.

6. CONTEXT.md is the domain glossary. Each term has a bold name, a one or two sentence definition and an "Avoid" line listing synonyms not to use. Terms are grouped under headings. Scratch had Coach, Student, Group, Needs Attention, Lesson, Lesson Status, Lesson Note, Swing Video Link and Follow-up Thread. Recipe-genie needs its own terms from a grilling session, not invented by you.

7. docs/adr/ holds short ADRs, one decision per file, numbered 0001 onward. Each is a title and one paragraph giving the decision, why it was chosen and the tradeoff. Only the stack ADR added a "Considered Options" section. Scratch's five covered the stack, the data access pattern and how ownership is enforced, REST endpoints over server actions, which users have accounts, and an email outbox instead of real sending during the MVP. Recipe-genie needs its own ADRs, but the same kinds of questions are worth asking.

8. CLAUDE.md is the project agent file, written with the writing-for-agents skill in the structure from class. Its sections are a one-paragraph product and stack summary, a "read before starting" list (CONTEXT.md, docs/adr/, PROJECT_CONTEXT.md), a planned codebase map, build and test commands, the workflow rules (one ticket per branch, PR against main, build test-first with /tdd, offer a PROMPT_LOG entry for notable prompts), a pointer to CODING_STANDARDS.md, how to run the app locally, testing expectations, and a security section.

## Workflow decisions to carry over

All agentic work runs through Claude Code. Sally dropped Lovable so AI usage stays in one place for grading. She follows a research, plan, implement structure.

She uses Matt Pocock's skills plugin, installed with `claude plugin install mattpocock-skills@claude-plugins-official`. The planned sequence is to set up the skills with GitHub Issues as the tracker, run /grill-with-docs on the product to produce the glossary and ADRs, then /to-spec and /to-tickets in the same session for Priority 1. Each ticket is built with /implement, which drives /tdd and ends with /mattpocock-skills:code-review, with context cleared between tickets. PRs use /mattpocock-skills:code-review against main and /pr, then get compared with CodeRabbit's review. /research is for technical decisions, /diagnosing-bugs for stubborn bugs and /retro after sessions that went badly. For understanding generated code she wants the Explore agent, /teach and /improve-codebase-architecture. She chose to skip /wayfinder, /implement-spec and /triage for now.

In Scratch, /grill-with-docs ran in three rounds. Product shape came first, then language and domain rules, then database, data access and tooling. Asking product questions before the stack question worked well because product answers ruled out options early. Repeat that order. Sally accepted every recommendation last time and noted she should check the ADRs closely in review, so give her room to push back this time.

Tooling choices were Playwright for end-to-end tests plus unit tests, CodeRabbit on every PR, GitHub Actions running tests on every PR, and Vercel for deployment.

## Generic rules worth keeping

These came out of Scratch's ADRs and CLAUDE.md and apply to almost any web app. All data access goes through one queries module, scoped to the signed-in user's ID taken from the session, never from the request body. Every new endpoint gets a test proving one user cannot read or change another user's data. Secrets live only in .env.local and the host's environment settings and never in a tracked file, including CLAUDE.md and PROMPT_LOG.md. Server-only keys never reach client code. Seed and test data use made-up names and example.com emails. Any external service beyond the decided ones needs Sally's approval first.

## Things to raise with Sally early

Scratch deliberately avoided AI in the product. Its "needs attention" list used simple rules, and its CLAUDE.md requires asking Sally before adding any LLM API. A name like recipe-genie suggests an LLM feature, so confirm whether the product calls a model, which provider, how API keys and costs are handled, and how those features get tested. That answer may change the stack ADR and will need its own ADR.

Recipe-genie gets its own repo. Scratch's planning work, including this brief, is merged into Scratch's main branch, so read from main.

Scratch had not yet reached /to-spec, /to-tickets or any app code. Its next step was writing the technical spec assignment. Recipe-genie needs to catch up through the glossary, ADRs and CLAUDE.md before reaching that same point.
