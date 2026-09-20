
## Product Specification: Project Chasm

## 1. Executive Summary & Core Philosophy

Project Chasm is a high-stakes, anti-gamification competitive data structures and algorithms (DSA) platform. Traditional competitive coding platforms emphasize cumulative, all-time problem counts, which discourage late starters and mask current stagnation.

This platform shifts the focus entirely to peer momentum within a tight, hyper-focused ecosystem. By replacing historical totals with rolling short-term velocity windows, the platform weaponizes loss aversion and upward social comparison to force daily consistency.

## Core Objectives

- Eliminate Historical Bias: Erase the advantage of early starters to ensure today's effort dictates today's rank.
- Surface Peer Momentum: Provide inescapable visibility into the immediate activity of close peers.
- Quantify the Deficit: Show the exact, actionable effort required to capture the top spot.
- Automate Accountability: Leverage public reputation risk to eliminate excuses and behavioral drift.

---

## 2. Circle Dynamics & Scoping

- Circle Size: Restricted to 3–8 active peers to maximize interpersonal accountability.
- Target Audience: Highly motivated DSA students and engineers preparing for technical interviews.
- Frictionless Tracking: Zero manual check-ins. The platform automatically scrapes problem submissions via public LeetCode, Codeforces, or GitHub handles.

---

## 3. Core Feature Specifications

## Feature A: The Rolling Velocity Leaderboard

Ranks are calculated strictly over sliding time windows: a Rolling 24-Hour window and a Rolling 7-Day window. Cumulative all-time scores are completely hidden from the main view.

- Scoring Architecture:
    - Easy: 1 point
    - Medium: 3 points
    - Hard: 7 points
- Velocity Behavior: If a peer solves 2 Mediums and 1 Hard problem within a two-hour window, their score surges by +13 points. If your velocity remains at 0, they immediately leapfrog your standing, dropping you into the danger zone.

## Feature B: "The Chasm" (Relative Deficit HUD)

The main dashboard bypasses generic greetings. Instead, it features a prominent Heads-Up Display (HUD) highlighting your exact mathematical deficit against the current circle leader.

```text
Current Deficit: −16 Points (Rank 3 of 5)

To overtake Priya (Rank 1) before the 24-hour window rolls over:
[ ] Solve 2 Hard problems OR
[ ] Solve 3 Mediums + 1 Easy problem
```

## Feature C: "The Wire" (Real-Time Solve Stream)

A real-time, low-latency timeline that broadcasts every event ingested across the circle. It incentivizes the submission of a micro-review called an Atomic Takeaway.

- Event Sample:
    > 11:24 PM — Aarav solved _“Merge k Sorted Lists”_ (Hard)Atomic Takeaway: _"Used a min-heap of size k; avoided pointer reassignment bugs by maintaining dummy head references."_

## Feature D: Out-of-Band Overtake Alerts

An asynchronous notification engine that monitors rank changes and pushes immediate updates to the circle's private communications channel (Discord or Telegram).

- Alert Sample:
    > 🚨 Rank Overtake Alert: Rohan just solved _'Word Break'_ and pushed you down to Rank 3. Current 24h gap: 4 points. Time left before rolling expiration: 3 hours.

---

## 4. Advanced Behavioral Triggers

## 1. The Automated "Dead Man’s Switch"

Users sign a weekly commitment contract requiring a baseline velocity (e.g., 15 DSA points per week).

- The Trigger: Every Sunday at 11:59 PM, the system evaluates the weekly target.
- The Penalty: If the target is missed, an automated background worker publishes an uncancelable failure log directly to the user's LinkedIn profile via API.
- Failure Post Template:
    > _"Public Accountability Log: At the start of this month, I committed to solving 15 algorithmic points weekly. This week, I fell short (8/15 points achieved). Logging this missed target publicly to enforce discipline and eliminate excuses."_

## 2. Peer "Bounty" & Head-to-Head Challenges

Any member can stake their own velocity points by issuing an asynchronous challenge on a high-frequency problem (e.g., the Blind 75 list).

- The Staking Mechanic: A peer places a 5-point bounty on _"Trapping Rain Water"_ with a 24-hour deadline.
- The Outcome: If you fail to submit an accepted solution within the window while the challenger succeeds, 5 points are transferred directly from your velocity balance to theirs.

## 3. Dynamic "Stagnation" Status Badges

A self-updating dynamic SVG badge hosted by the platform server, designed to be embedded in GitHub profile READMEs or shared on social media.

- Visual States:
    - Active: `[DSA Status: High Velocity | Circle Rank: 1/5]` (Green)
    - Stagnant: `[DSA Status: Inactive 48h | Circle Rank: 5/5]` (Red)

## 4. The "Sliding Velocity Decay" Engine

To eliminate "weekend cramming" and encourage daily consistency, points earned do not remain static for the duration of the 7-day window.

- The Decay Curve: Points retain full value for 48 hours, then decay exponentially.
- Decay Example: A Medium problem solved on Monday yields 3 points. By Wednesday, it decays to 1.5 points. By Thursday, it hits 0 points, dropping your rank unless replaced by fresh solves.

---

## 5. Automated LinkedIn Socialization Engine

To convert professional networks into an accountability surface, the platform executes a strict three-phase publishing architecture:

1. The Stake (Initial Public Declaration): An automated announcement post detailing the rules, the target goals, and the API integration to validate commitment transparency.
2. The Reward (Visual Proof-of-Work): Upon a successful week, a headless browser worker generates a dark-mode infographic card displaying the user's 7-day velocity score, their hardest conquered problem, and their circle rank.
3. The Threat (Automated Failure Post): If the weekly cron job detects a missed threshold at midnight on Sunday, the system bypasses user confirmation and dispatches the predefined failure post.

---

To take this platform draft to the next stage, let me know:

- Which social media or chat APIs (e.g., LeetCode scraping, Discord webhooks, LinkedIn API) you want to map out first.
- If you want to refine the mathematical formula for the exponential point decay engine.
- If you want to design a database schema for handling the rolling 24-hour/7-day windows.
