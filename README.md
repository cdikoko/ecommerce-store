# Atelier Store

Building an Ecommerce website to practice fundamentals and try out new tools.

Next.js eCommerce app — project skeleton.

## Stack

- [Next.js 16](https://nextjs.org) (App Router, `src/` dir, Turbopack) + TypeScript
- [Tailwind CSS v4](https://tailwindcss.com)
- [Better Auth](https://better-auth.com) (Drizzle adapter, `nextCookies` plugin)
- [Drizzle ORM](https://orm.drizzle.team) + drizzle-kit
- [Neon](https://neon.tech) serverless Postgres (HTTP driver)
- [Zod](https://zod.dev) for env validation

## Getting started

1. Install dependencies:

   ```bash
   npm install
   ```

2. Create `.env.local` from the example and fill it in:

   ```bash
   cp .env.example .env.local
   ```

   - `DATABASE_URL` — Neon connection string (pooled)
   - `BETTER_AUTH_SECRET` — generate with `npx auth secret`
   - `BETTER_AUTH_URL` — app origin, `http://localhost:3000` in dev

3. Generate the Better Auth tables, re-export them from `src/db/schema/index.ts`
   (`export * from "./auth";`), then create and apply a migration:

   ```bash
   npm run auth:generate
   npm run db:generate
   npm run db:migrate
   ```

4. Start the dev server:

   ```bash
   npm run dev
   ```

## Scripts

| Script                  | Description                                          |
| ----------------------- | ---------------------------------------------------- |
| `npm run dev`           | Start the dev server                                 |
| `npm run build`         | Production build                                     |
| `npm run lint`          | ESLint                                               |
| `npm run typecheck`     | TypeScript check                                     |
| `npm run auth:generate` | Generate Better Auth Drizzle schema into `src/db/schema/auth.ts` |
| `npm run db:generate`   | Generate SQL migrations from the schema into `drizzle/` |
| `npm run db:migrate`    | Apply pending migrations                             |
| `npm run db:push`       | Push schema directly (prototyping only)              |
| `npm run db:studio`     | Open Drizzle Studio                                  |

## Structure

```
src/
  app/
    api/auth/[...all]/route.ts  Better Auth route handler
    layout.tsx, page.tsx        Placeholder shell
  db/
    index.ts                    Drizzle client (Neon HTTP)
    schema/index.ts             Schema barrel — add tables here
  lib/
    auth.ts                     Better Auth server instance
    auth-client.ts              Better Auth React client
  env.ts                        Zod-validated server env
drizzle/                        Generated migrations
drizzle.config.ts               drizzle-kit config
```
