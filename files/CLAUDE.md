# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About

**workita-stepbystep** is an AI-powered step-by-step job application companion. It guides users through the job application process using Google Gemini (via Genkit) to provide intelligent, contextual assistance at each stage.

## Journeys

These are the main user journeys that the app supports:

**Registration / Log in**

- Users can create an account and log in to save their progress and access personalized features.
- The app uses JWT-based authentication for secure access to user data.
- Users will register and log in using Google SSO, leveraging their existing Google accounts for a seamless experience.
- If users have not registered, they will be prompted to do so when they first access the app. Once registered, they can log in using their Google credentials.
- Unless users log in, they can still explore the app and access general information, but personalized features and progress saving will be unavailable.
- On registration via Google SSO, the app will create a new user profile in the database using the information retrieved from the user's Google account (e.g., name, email). This allows for a personalized experience and enables users to save their progress and access it across devices.

**Onboarding**

- After the user is registered and logged in, they will be guided through an onboarding process where they can input their job preferences: Role, Seniority, Industry, Location, preferred companies, Presencial/Remote/Hybrid, salary expectations.
- The app will ask the user to upload their extended CV. This CV will be used to tailor the job application guidance and AI interactions to the user's specific background and experience.
  - The app will analyze the uploaded CV to extract relevant information such as skills, experience, and education. This information will be used to provide personalized recommendations for job applications, interview preparation, and networking opportunities.
  - The app will also use the information from the CV to identify potential gaps or areas for improvement in the user's profile. This may include suggestions for additional skills to acquire, certifications to pursue, or ways to better highlight existing experience.
  - The app will simulate how the user's CV would be parsed by common Applicant Tracking Systems (ATS) and provide feedback on how to optimize the CV for better visibility in these systems. This may include recommendations for formatting, keyword usage, and overall structure to increase the chances of passing through ATS filters.
- The app will also ask the user to input their LinkedIn profile URL. This information will be used to further customize the job application guidance and AI interactions based on the user's professional background and network.
  - The app will present recommendations for improving the user's LinkedIn profile based on the information provided in the CV and LinkedIn URL. This may include suggestions for optimizing the profile summary, adding relevant skills, or improving the overall presentation to make the profile more suitable for LinkedIn algorithms (recruiter search, consistency with CV, Application Tracking Systems filtering). The app will also present the user with the summary of recommendations and the rationale behind them, as well as a quick summary of how LinkedIn works for candidates.

**New Candidature**

- The user can start a new job application process by sharing the link to the job description (e.g. from LinkedIn, company website, etc).
- The app will analyze the job description to extract and present key information such as:
  - Required skills, experience, and expected salary, presented to the user in a structured format. This will help the user understand the requirements and expectations for the role.
  - Based on the candidate profile (CV + LinkedIn) and the job description, the app will perform the following:
    - **% Match:** The app will calculate a percentage match between the user's profile and the job requirements.
    - **Strengths:** The app will identify and highlight the user's strengths in relation to the job requirements.
    - **Gaps:** The app will identify any gaps or areas where the user's profile may not fully meet the job requirements, providing insights into potential areas for improvement or additional focus in the application process.
    - **Candidate Key differentiators:** The app will identify key differentiators in the user's profile that can be emphasized in the application to make it stand out to recruiters and hiring managers.
    - **Keywords for ATS:** The app will extract relevant keywords from the job description that are important for passing through Applicant Tracking Systems (ATS) and provide recommendations on how to incorporate these keywords effectively into the user's CV and application materials.
    - **Recommendations for LinkedIn profile:** Based on the analysis of the job description and the user's LinkedIn profile, the app will provide specific recommendations for optimizing the LinkedIn profile to increase visibility and attractiveness to recruiters and hiring managers for the specific role.
    - **Recommendations for CV:** The app will provide tailored recommendations for optimizing the user's CV to better align with the job description and increase the chances of passing through ATS filters. This may include suggestions for formatting, keyword usage, and overall structure to make the CV more appealing to recruiters and hiring managers.

## Commands

```bash
# Start both client (port 8080) and server (port 3001) with hot-reload
npm run dev

# Start individually
npm run dev:client   # Vite dev server
npm run dev:server   # Express + Genkit with tsx watch

# Build for production
npm run build        # compiles TypeScript + Vite bundle

# Lint
npm run lint

# Database
npm run db:generate  # generate migration files from schema changes
npm run db:migrate   # apply migrations to the database
npm run db:push      # push schema directly (dev only, skips migration files)
npm run db:studio    # open Drizzle Studio in browser

# Genkit Developer UI (inspect and test AI flows)
npm run genkit:ui
```

## Architecture

This is a full-stack TypeScript web app with three layers:

```
src/          → React 19 frontend (Vite)
server/       → Express 5 backend (Node.js)
  ai/         → Genkit AI flows
  db/         → Drizzle ORM + PostgreSQL
```

### Request flow

In **development**: Vite dev server (`:8080`) proxies `/api/*` requests to the Express server (`:3001`) — configured in `vite.config.ts`.

In **production (Docker)**: nginx serves the built frontend and proxies `/api/*` to the Express container — configured in `nginx.conf`.

### AI layer (`server/ai/`)

- `genkit.ts` — initialises the shared `ai` Genkit instance using `@genkit-ai/google-genai` with `gemini-2.0-flash` as the default model.
- `flows.ts` — defines Genkit flows using `ai.defineFlow(...)`. Each flow has typed Zod input/output schemas. Add all new AI logic here as additional flows.
- Flows are imported and called directly from Express route handlers in `server/index.ts`.

Requires `GOOGLE_GENAI_API_KEY` in the environment.

### Database layer (`server/db/`)

- `schema.ts` — single source of truth for the database schema using Drizzle's TypeScript DSL. Adding or changing a table here requires running `npm run db:generate` then `npm run db:migrate`.
- `index.ts` — exports the `db` Drizzle instance (backed by a `pg` connection pool) and the raw `pool`. Import `db` wherever queries are needed.
- Migrations output to `drizzle/migrations/`.
- Requires `DATABASE_URL` (PostgreSQL connection string) in the environment.

### Docker Compose

Two compose files:

| File | Purpose |
|---|---|
| `docker-compose.yml` | Production — builds from Dockerfiles, nginx on port 8080 |
| `docker-compose.dev.yml` | Development overlay — mounts source for hot-reload |

Run dev stack:

```bash
docker compose -f docker-compose.yml -f docker-compose.dev.yml up --build
```

The `server` service waits for the `db` healthcheck before starting. The `client` nginx container proxies `/api/` to the `server` container by hostname.

### Environment variables

Copy `.env.example` to `.env`. Key variables:

| Variable | Used by |
|---|---|
| `GOOGLE_GENAI_API_KEY` | Genkit / Gemini |
| `DATABASE_URL` | Drizzle db connection |
| `POSTGRES_USER/PASSWORD/DB` | Docker Compose postgres service |

### TypeScript setup

The project has two separate TS configs:

- Root `tsconfig.json` / `tsconfig.app.json` — for the Vite frontend (ESNext, bundler module resolution).
- `server/tsconfig.json` — for the Express backend (ES2022, NodeNext module resolution). Server imports must use `.js` extensions (e.g. `import { db } from './db/index.js'`).
