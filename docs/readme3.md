## High-Level Design (HLD)

This is the system architecture for an app built with Next.js, Go, and PostgreSQL.

## 1. System Topology & Data Flow

```unset
                      ┌──────────────────────┐
                      │    Next.js Client    │
                      │  (Dashboard HUD / )   │
                      └──────────▲───────────┘
                                 │ HTTP / WebSockets
                      ┌──────────▼───────────┐
                      │    Go API Gateway    │
                      │  (Auth, Circle Mgmt) │
                      └────┬────────────┬────┘
                           │            │
             ┌─────────────┘            └──────────────┐
  Read/Write │                              RPC / Jobs │
             │                                         │
┌────────────▼─────────────┐             ┌─────────────▼─────────────┐
│  PostgreSQL Database     │             │    Asynchronous Worker    │
│ (Users, Submissions,     │             │   (Go-Craft/Work or Asynq)│
│  Circles & Logs)         │             └─────────────┬─────────────┘
└──────────────────────────┘                           │
                                      ┌────────────────┼────────────────┐
                                      │                │                │
                               ┌──────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐
                               │  Scrapers   │  │ Discord Bot │  │LinkedIn API │
                               │ (LC / CF)   │  │  (Webhooks) │  │  (OAuth 2)  │
                               └─────────────┘  └─────────────┘  └─────────────┘
```

---

## 2. Component Breakdown

## A. Next.js Frontend App

- Dashboard HUD: Built with React Server Components (RSC) for initial page load and Client Components for handling live updates.
- State & Live Updates: Uses native WebSockets or Server-Sent Events (SSE) coming from the Go backend to update the Deficit metric instantly when a peer completes a problem.
- Dynamic Badges: Fetches server-rendered SVG endpoints (`/api/users/:id/badge.svg`) generated dynamically by the backend for embedding in GitHub READMEs.

## B. Go Backend Services

- API Service: An HTTP multiplexer (using `chi` or `gin`) handling user authentication, circle creations, and the relative metric calculation formulas.
- Scraper Engine: Runs concurrency-safe routines (`goroutines`) powered by internal tickers to scrape LeetCode GraphQL and Codeforces API endpoints.
- Background Queue Manager: A redis-backed or in-memory job engine (using libraries like `asynq` or `go-craft/work`) that processes notifications, runs decay updates, and processes LinkedIn API payloads.

## C. Data Tier (PostgreSQL)

- Standard relational database storing core app states.
- Indexes are explicitly built on the `solved_problems` table across `(user_id, solved_at)` to keep sliding window calculations fast and efficient.

---

## 3. Core Engine Mechanics & Data Flows

## The Ingestion Pipeline (10-Minute Loop)

```unset
[Go Ticker] ──► Spawn Goroutine per User ──► Fetch LC/CF API ──► Filter New Submissions
                                                                         │
    ┌────────────────────────────────────────────────────────────────────┘
    ▼
[Upsert to Postgres] ──► Detect Rank Shift? ──► [True] ──► Dispatch Discord Hook
                                            ──► [False] ─► End Stream
```

## The Dead Man's Switch (Sunday 11:59 PM Cron)

```unset
[Cron Trigger] ──► Fetch Active Circles ──► Compute Weekly Velocity Score
                                                     │
       ┌─────────────────────────────────────────────┘
       ▼
[Score < Target?] ──► [Yes] ──► Pull Decrypted Token ──► Post Failure to LinkedIn
                  ──► [No]  ──► Render Dynamic SVG   ──► Post Performance Analytics
```

---

To continue detailing this system architecture, let me know:

- Which Go framework or library preference (`Gin`, `Fiber`, or `Standard Library`) you prefer for handling the HTTP layer.
- If you want to view the complete Go implementation pattern for parsing the LeetCode GraphQL API.
- If you want a specific name recommendation chosen from the list above to theme the project.