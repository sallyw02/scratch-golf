# Project Context: Scratch (Golf Coach Management Tool)

This file gives a new Claude Code session the background on this project. Read it fully before doing anything else.

## Who I am and how to work with me

- I am Sally, a student in CS146S: The Modern Software Developer (Stanford, fall 2026). This is my solo final project.
- I am a beginner with agent harnesses like Claude Code. Explain what you are about to do and why, in plain language, before you do it. When you use a skill, tell me which one and what it will produce.
- Keep me in control. Ask before large or hard-to-undo changes, and prefer small steps I can review.
- My strongest language is Python. I am open to a TypeScript web stack if it fits the project better, but explain the tradeoff.
- Write in a concise, straightforward way with full sentences. Avoid em dashes and keep semicolons and colons to a minimum.

## Course objectives for this project

The project is graded on both the product and how I use AI tools across the development lifecycle. I need to:

- Build a working MVP web app that solves a real problem.
- Use AI tools at every stage (prototyping, planning, code generation, testing, review, CI/CD).
- Keep a log of my real prompts, including how and why they changed. Help me capture notable prompts and decisions as we go.
- Open a pull request for every change, with AI review on each one.

## The product

**Problem.** Independent golf coaches, often coaching from home studios or indoor simulators, run their business through a patchwork of tools: an outdated website, WhatsApp and WeChat, and several payment methods. Scheduling is slow, lesson notes are scattered or never written, follow-ups depend on memory, and it is hard to see student progress or business growth. Coaches lose time on admin, students get an inconsistent experience, and coaches miss students who are drifting away. Existing golf tools focus on either booking or video analysis, so coaches stitch several together.

**Target user.** The independent coach who already has students. Not new coaches looking for leads. Students are a possible secondary user, but student-facing features are stretch goals.

**Use case.** The app works like a lightweight CRM. The coach adds each student, schedules and records lessons, and sends notes and follow-ups by email. The value is less admin time, a clear record of every student, and fewer missed follow-ups.

**Working name:** Scratch.

## MVP features (in priority order)

Priority 1
1. **Student profiles and history view.** Create and manage a profile per student. Each profile shows a timeline of lessons and notes, and the coach can open any lesson for detail.
2. **Lesson calendar.** Schedule and manage all lessons in one calendar. Each lesson links to the student's profile. Students are notified by email.

Priority 2

3. **Post-lesson notes.** Notes written from a template with a focus area, drills assigned, and a swing video link, then sent to the student.
4. **Lesson follow-up threads.** A simple message thread per lesson with email notifications. Lighter than a full chat app.
5. **Student groups and a "needs attention" list.** Segment students (for example frequent vs one-off). The list flags students who have not booked in a set number of days, using simple rules and not AI.

**Stretch goals:** student login (view upcoming lessons, read notes, confirm times), online payments, a business dashboard (lessons per month, active students), real-time chat.

**Planned screens (from my sketch):** landing page with login, schedule view ("Welcome back" with upcoming lessons), lesson card (agenda, notes, copy-to-clipboard or send to student), students overview grid with search, filter and sort by group, and a student card (most recent lesson, lessons this month).

## Tools I plan to use

- **Claude Code** for every agentic workflow: planning, prototyping, implementing features one at a time, testing and review. I follow a research, plan, implement structure (RePPIT). I am not using Lovable.
- **Playwright** for end-to-end tests, plus unit tests. AI drafts tests, I review them.
- **CodeRabbit** review on every PR, compared against my own review and the skill-based review below.
- **GitHub Actions** to run tests on every PR, and **Vercel or Render** for deployment.
- **Resend** for email. For the MVP, emails are logged instead of sent, and real sending comes later.

Stack (decided October 14, 2026): Next.js in TypeScript, Supabase for Postgres and auth, Drizzle ORM, Tailwind with shadcn/ui, FullCalendar, Vitest and Playwright, deployed on Vercel. The reasoning is in `docs/adr/`.

## Timeline

About six weeks remain as of October 14, 2026, so the target is late November 2026. The goal is to finish as much of Priority 1 and Priority 2 as possible, with Priority 1 done first.

## Prompt log

`PROMPT_LOG.md` in the repo records notable prompts and decisions as we go. Add an entry whenever a prompt changes direction, produces a key artifact, or needed rewording to work.

## How I want to use Matt Pocock's engineering skills

I installed (or will install) the skills from https://github.com/mattpocock/skills with:

```
claude plugin install mattpocock-skills@claude-plugins-official
```

My priorities are research, understanding the codebase, and code review. Here is the workflow I want to follow.

1. **One-time setup.** Run `/setup-matt-pocock-skills` in this repo to configure the issue tracker (GitHub Issues, so it lines up with my PR-per-change workflow) and the domain doc layout.
2. **Sharpen the plan.** Run `/grill-with-docs` on the product description above. It should produce a `GLOSSARY.md` (terms like Student, Lesson, Note, Thread, Group, "needs attention") and ADRs for key decisions.
3. **Spec and tickets.** In the same session, without clearing, run `/to-spec` and then `/to-tickets` to break the MVP into small tickets, starting with Priority 1.
4. **Build one ticket at a time.** Run `/implement` per ticket, which drives `/tdd` and ends with `/code-review`. Clear context between tickets.
5. **Review and PR.** Use `/code-review` against `main` and `/pr` for the PR description. Then compare with CodeRabbit's review.
6. **As needed.** Use `/research` for technical decisions (it writes cited notes into the repo), `/diagnosing-bugs` for stubborn bugs, and `/retro` after sessions that went badly.

**For understanding the codebase** (especially after a large chunk of generated code lands): use the built-in Explore agent to walk me through how data flows, `/teach` to explain concepts I don't know yet, and `/improve-codebase-architecture` for a visual report of the structure and weak spots.

**Skip for now:** `/wayfinder`, `/implement-spec`, `/triage`.

I also want a short `CODING_STANDARDS.md` early on so `/code-review` has standards to check against.

## Where I am now

- The proposal is written and the scope above is settled.
- Email (Resend, logged for the MVP), PR review (CodeRabbit) and tooling (Claude Code only) are decided.
- The stack is decided. `CONTEXT.md` (the glossary), five ADRs and `CLAUDE.md` are written. No app code exists yet.
- Next: write the technical spec assignment, then run `/to-spec` and `/to-tickets` for Priority 1.
