Here is a comprehensive summary of Project Chasm (or your chosen project name), structured to clearly define the problem space, the solution, and the core behavioral mechanics.

---

## Project Summary: Project Chasm

## 🚨 The Problem We Are Solving

Traditional competitive programming and data structures & algorithms (DSA) platforms suffer from a historical bias that degrades long-term user motivation.

- The Veteran Advantage: Leaderboards are dominated by cumulative, all-time solve counts. This makes it mathematically impossible for a late starter to ever catch up to someone with a multi-year head start.
- The Stagnation Mask: All-time point totals allow individuals to coast on past accomplishments. A user can completely stop practicing for months while still appearing at the top of a leaderboard, masking an immediate lack of effort.
- Lack of Real-Time Urgency: Generic coding platforms lack direct, intrusive accountability. They rely on vague personal intent rather than immediate, unavoidable peer momentum.

## 🎯 The Goals

1. Surface Peer Momentum: Shift focus entirely from _historical scale_ to _immediate momentum_. The system makes it impossible to ignore when someone in your close social circle is working harder than you right now.
2. Enforce Daily Consistency: Eliminate "weekend cramming" by introducing a system where points decay if a user remains inactive.
3. Weaponise Social Stakes: Convert your professional and social circles into accountability mechanisms using public exposure (LinkedIn) and direct competition (Discord/Telegram).

## ⚡ What is "Chasm"?

Chasm is an anti-gamification, web-based competitive companion platform that integrates with LeetCode and Codeforces. Instead of showing global stats, it confines users to tiny, high-stakes peer circles (3–8 members) and forces competition based on current activity.

It strips away all-time historical metrics and judges users purely on a rolling timeline (Rolling 24-Hour and 7-Day windows).

---

## 🛠️ Core Features & Mechanics

- The Rolling Velocity Leaderboard: Ranks fluctuate dynamically based on sliding time windows. Points are weighted by difficulty (Easy: 1, Medium: 3, Hard: 7).
- "The Chasm" HUD (Heads-Up Display): The dashboard bypasses generic greetings. Instead, it highlights the exact mathematical deficit between you and the current circle leader (e.g., _"You are -16 points behind Priya. To overtake her, you must solve 2 Hards or 3 Mediums + 1 Easy before her points roll over"_).
- "The Wire" (Solve Stream): A live activity timeline of your circle's submissions. Users are incentivized to post an Atomic Takeaway (a brief, low-overhead code invariant or architectural note) with their solve to share concise learning points.
- The "Sliding Velocity Decay" Engine: Points do not stay static for 7 days. They maintain full value for 48 hours and then exponentially decay to 0 by Day 4, forcing regular consistency and punishing dormancy.
- The Automated "Dead Man’s Switch": A high-stakes accountability contract. If a user sets a target (e.g., 15 points/week) and fails to hit it by Sunday at 11:59 PM, the backend uses the LinkedIn API to automatically publish an uncancelable post logging their failure to their professional network.
- Out-of-Band Overtake Alerts: A low-latency background worker that triggers automated ping notifications inside a private Discord channel the exact moment a peer overtakes your rank.

---

## 💻 Tech Stack Choice

- Frontend: Next.js (React Server Components for speed; WebSockets/SSE for real-time HUD updates).
- Backend: Go (Golang) (for highly concurrent scraping routines, handling data ingestion, and managing background job queues).
- Database: PostgreSQL (with explicit indexing on time boundaries to query rolling windows instantly).

Would you like to proceed with mapping out the Go backend architecture, or would you prefer to look at the database schema and query configurations for the point decay logic next?
