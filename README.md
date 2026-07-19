# BuildTrack AI — Construction Progress Analyzer

A production-grade, AI-powered SaaS platform that reads construction site
photos and drone footage the way a senior site inspector would — estimating
completion percentage, flagging safety/PPE violations, predicting delays, and
generating executive reports — developed as a full-stack engineering
portfolio project. The system demonstrates real vision-model integration,
multi-tenant RBAC, semantic search, billing, and a modern component-based
frontend end-to-end.

---

## Features

### Authentication & Roles
- Email/password auth (bcrypt + NextAuth JWT sessions) plus Google/GitHub OAuth
- Role-based access per organization: Owner, Admin, Project Manager, Engineer, Viewer
- Server-side RBAC enforcement on every mutating route, not just the UI

### Organizations, Projects & Sites
- Multi-tenant organizations, each with members, projects, and construction sites
- Projects track status, budget, timeline, and geolocation
- Sites hold weekly reports and all uploaded media

### AI Progress Analysis
- Real vision-model pipeline (GPT-4o) reads uploaded site photos and returns a
  strict, Zod-validated structured report: completion %, detected structures/
  materials/equipment/PPE, safety violations with severity, executive summary,
  risk analysis, delay analysis, and recommendations
- Video/drone footage support: `ffmpeg` extracts evenly-spaced frames, each is
  analyzed, and results are aggregated into one report
- Every analysis updates the project's progress history automatically

### Safety & Notifications
- Safety violations tracked with severity (Low/Medium/High/Critical) and resolution state
- In-app notifications on analysis completion and high-severity safety flags

### Dashboard & Reporting
- Org overview: active projects, open violations, average completion
- Per-project progress-over-time chart, open safety feed, per-site upload widget
- One-click PDF executive report export and multi-sheet Excel export

### Semantic Search
- OpenAI embeddings + Qdrant vector search across projects, AI analyses, and
  safety violations, scoped per organization

### Billing
- Stripe Checkout, customer billing portal, and webhook-driven subscription sync

### Responsive Design & Theming
- Custom "industrial blueprint" design system — deep teal/navy with safety-orange accents
- Dark mode by default, fully responsive across mobile, tablet, and desktop
- Custom 404/error boundaries, loading skeletons, and OG/favicon metadata

---

## Tech Stack Used

| Layer | Technology | Purpose |
|---|---|---|
| Framework | Next.js 14 (App Router), TypeScript | Full-stack app: pages + API routes |
| Database | PostgreSQL + Prisma ORM | Relational data storage, type-safe queries |
| Auth | NextAuth (JWT) + bcrypt | Credentials + OAuth, RBAC |
| Validation | Zod | Request and AI-response schema validation |
| Vision AI | OpenAI (`gpt-4o`, `text-embedding-3-small`) | Site photo/frame analysis, embeddings |
| Video | fluent-ffmpeg + ffmpeg-static | Frame extraction from drone/video uploads |
| Search | Qdrant | Vector similarity search |
| Billing | Stripe | Checkout, portal, subscription webhooks |
| Reports | pdfkit, exceljs | PDF and Excel executive report export |
| Storage | AWS S3 SDK (local-disk fallback) | Media storage abstraction |
| Styling | Tailwind CSS + Radix UI | Custom design-token system, dark mode |
| State | TanStack Query | Server state, polling |
| Charts | Recharts | Progress-over-time analytics |
| Containers | Docker + docker-compose | Postgres, Qdrant, and app, locally and in prod |

=
