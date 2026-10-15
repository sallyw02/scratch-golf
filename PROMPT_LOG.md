# Prompt Log

This log records notable prompts I gave AI tools while building Scratch, what came back, and how my prompting changed.

A prompt is notable if it meets at least one of these tests. Everything else, such as small fixes, quick questions and "yes, go ahead" replies, stays out.

- It starts a new stage or skill, such as the first `/grill-with-docs` run or the first `/implement` on a ticket.
- It produces an artifact I keep, such as a spec, an ADR, a ticket set or a test suite.
- It leads to a decision about scope, stack or design.
- I had to rewrite it because the first version failed or gave a poor result. Log both versions.
- The AI got something wrong in a way worth remembering, such as a bug it introduced or a review comment I rejected.

As a rough guide, expect one to three entries per working session. If a session has none, check whether a decision was made that should be logged.

Each entry uses this format.

```
## <number>. <short title>
Date: YYYY-MM-DD
Stage: planning | prototyping | implementation | testing | review | CI/CD
Tool: Claude Code (skill or agent used, if any)

Prompt:
> exact prompt text

Result: what the AI produced, in one or two sentences.

Changes and why: what I changed in the prompt or the plan afterward, and the reason. Write "None" if it worked as intended.

Links: related PR, commit or file.
```

## 1. Kickoff review of project context
Date: 2026-10-14
Stage: planning
Tool: Claude Code

Prompt:
> read over PROJECT_CONTEXT.md, ask me any clarifying questions, and suggest some immediate next steps to handle.

Result: Claude asked six questions covering Lovable, stack, email provider, prompt log format, deadline and PR reviewer. It also suggested an initial commit, installing the Matt Pocock skills plugin and starting this log.

Changes and why: None. Asking for questions first surfaced decisions I had left open.

Links: PROJECT_CONTEXT.md

## 2. Answering setup decisions
Date: 2026-10-14
Stage: planning
Tool: Claude Code

Prompt:
> Addressing your questions. 1. No longer will be using Lovable, plan to use Claude code for all agentic workflows ... 2. Go with resend for email provider ... 3. Proceed with a prompt_log.md in repo ... 4. I have around 6 more weeks ... 5. Can go CodeRabbit. For next steps 1. Suggest format for PROMPT_LOG.md 2. Help commit PROJECT_CONTEXT.md with changes described, README.md, CODING_STANDARDS

Result: Claude updated PROJECT_CONTEXT.md with the decisions, drafted README.md and a stack-agnostic CODING_STANDARDS.md, and proposed this log format.

Changes and why: Dropped Lovable so every stage of the workflow runs through Claude Code, which keeps the AI usage in one place for grading. The tech stack is still open.

Links: initial commit
