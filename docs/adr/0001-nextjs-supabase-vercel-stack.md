# Next.js, Supabase and Vercel as the stack

Scratch is a single Next.js app in TypeScript, with Supabase for Postgres and coach sign-in, deployed on Vercel. One language and one codebase cover frontend, backend and tests, everything runs on free tiers, and the whole app deploys in one step. That matters for a solo six-week project where most code is written by an agent and reviewed by me.

## Considered Options

Django was the runner-up. It would have kept the project in Python, my strongest language, and it ships with auth and an admin panel. It lost because its free hosting on Render sleeps when idle and the UI would take longer to polish. FastAPI with a separate React frontend was rejected because it means two codebases and two languages.
