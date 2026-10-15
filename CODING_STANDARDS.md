# Coding Standards

These standards apply to all code in this repo and are what `/code-review` checks against. Stack-specific rules will be added once the tech stack is chosen.

## General

Keep functions small and focused on one job. Name things after the domain terms in the glossary, so a lesson is a `Lesson` and not an `Appointment`. Prefer clear code over clever code, and add a comment only when the reason behind the code is not obvious.

Don't leave dead code, commented-out blocks or unused imports. Remove debugging output before opening a PR.

## Data and security

Never commit secrets. API keys and database URLs live in environment variables, and `.env` files stay out of git. A `.env.example` lists the variables with placeholder values.

Every query that reads or changes student or lesson data must be scoped to the signed-in coach. A coach must never see another coach's students.

Validate all user input on the server, even when the form also validates it.

## Email

All email goes through one module. During the MVP that module logs the message instead of sending it, so switching to real Resend sending is a change in one place.

## Testing

New behavior comes with tests. Business rules such as the "needs attention" logic get unit tests. Each main user flow (add a student, schedule a lesson, write a note) gets a Playwright end-to-end test. Tests must pass in CI before a PR is merged.

## Pull requests

Each PR covers one ticket or one small change. The description says what changed, why, and how it was tested. PRs are reviewed by CodeRabbit and by `/code-review` before merging.

## Stack-specific rules

To be added after the stack decision.
