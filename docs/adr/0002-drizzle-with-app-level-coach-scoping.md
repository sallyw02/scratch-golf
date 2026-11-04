# Drizzle with coach scoping in the app instead of row-level security

All database access goes through Drizzle ORM in one data module, and every function in that module takes the signed-in Coach's ID and filters by it. We chose this over Supabase's client with row-level security because the full schema lives in one readable TypeScript file and queries are typed, which makes the code easier for both me and an agent to follow. The trade-off is that Postgres itself does not block cross-coach reads, so tests must prove that one Coach cannot read or change another Coach's data.
