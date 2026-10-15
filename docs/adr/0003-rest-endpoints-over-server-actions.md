# REST endpoints instead of server actions

Data operations are REST route handlers under `/api`, and pages call them, even though Next.js server actions would be the shorter path. REST endpoints map directly onto the API design in the technical spec, are easy to test in isolation, and keep a clear line between UI and backend. The Student reply link also needs a public endpoint, so REST was required somewhere regardless.
