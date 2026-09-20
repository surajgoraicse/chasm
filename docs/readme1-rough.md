
1. All-time solve counts are demotivating because someone with a 3-year head start is impossible to catch today. Instead, our leaderboard resets on a strict **rolling 7-day and 24-hour velocity window**.
2.

Goal :

1. What drives us is the visibility of peer momentum—the direct realization that someone else in our peer circle is outworking us right now.
2. Traditional competitive coding platforms emphasize all-time problem counts, which discourage late starters and mask current lack of effort. _Project Chasm_ leverages upward social comparison and loss aversion within a tight, private circle (3–8 peers) by tracking real-time **velocity** rather than accumulated historical totals.
3. Build an automated system that visibly surfaces peer momentum, quantifies our immediate deficit against the top performer, and pushes intrusive alerts when our standing slips.

---


## 2. Circle Dynamics & Scoping

- **Circle Size:** Restricted to 3–8 active peers.
- **Target Audience:** highly motivated dsa 
- **Frictionless Tracking:** Zero manual check-in required for basic functionality; problem submissions are scraped automatically via public handles.

## 3. Core Feature Specifications

### Feature A: The Rolling Velocity Leaderboard

- **Mechanism:** Ranks are calculated strictly over sliding time windows: **Rolling 24 Hours** and **Rolling 7 Days**. All-time scores are tucked away or hidden.
- **Scoring Weight Example:**
    - Easy: $1\text{ point}$
    - Medium: $3\text{ points}$
    - Hard: $7\text{ points}$
- **Concrete Example:**
    Suppose our peer Rohan solves 2 Mediums and 1 Hard between 10:00 PM and midnight. His 24-hour velocity score surges by $+13$ points. If our velocity remains at $0$, Rohan jumps from Rank 4 to Rank 1, pushing us down to the danger tier.

### Feature B: "The Chasm" (Quantified Relative Deficit HUD)

- **Mechanism:** The top of our dashboard does not display a generic greeting. Instead, it computes and highlights our exact mathematical deficit against the current circle leader.
- **Concrete Display Example:**
    > **Current Deficit: −16 Points (Rank 3 of 5)**
    >
    > _To overtake Priya (Rank 1) before the 24-hour window rolls over, we must solve either 2 Hard problems or 3 Mediums + 1 Easy._

### Feature C: "The Wire" (Real-Time Solve Stream + Proof-of-Work)

- **Mechanism:** A real-time timeline displaying every event ingested across the circle, paired with an optional but incentivized "Atomic Takeaway" note.
- **Concrete Example:**
    A card appears on the feed:
    > **11:24 PM** — _Aarav solved "Merge k Sorted Lists" (Hard)_
    >
    > **Invariant Logged:** _"Used a min-heap of size $k$; avoided pointer reassignment bugs by maintaining dummy head references."_
    >
    > Seeing a peer systematically dissecting complex problems late at night generates immediate urgency to open our editor.

### Feature D: Out-of-Band Overtake Alerts (Discord / Telegram)

- **Mechanism:** An asynchronous notification worker that monitors rank transitions and inactive streaks, pushing updates directly to our team's communication channel.
- **Concrete Example Message:**
    > _"🚨 **Rank Overtake Alert**: Rohan just solved 'Word Break' and overtook our team standing for Rank 2. Current 24h gap: 4 points. Time left before rollover: 3 hours."_

#### 1. The Automated "Dead Man’s Switch" (Public Failure Broadcast)

- **The Mechanic:** We define a weekly commitment contract (e.g., minimum 15 points of DSA velocity per week). At Sunday 11:59 PM, if our target is unmet, our system triggers an automated, uncancelable post directly to our LinkedIn feed.
- **The Psychology:** This weaponizes loss aversion and social stakes. Behavioral platforms like stickK demonstrate that the fear of public embarrassment and reputational damage is significantly more motivating than the prospect of a reward.
- **Concrete Example:** If our weekly score sits at 8 points on Sunday evening, the worker executes a scheduled post to our LinkedIn network:
    > _"Public Accountability Log: At the start of this month, we committed to solving 15 algorithmic problems weekly. This week, we fell short (8/15 solved). Logging this missed target publicly to enforce discipline and eliminate excuses."_
    >
    > Knowing this will appear in the feeds of colleagues, recruiters, and engineering peers creates immediate urgency to finish the remaining problems before the cutoff.

#### 2. Peer "Bounty" & Head-to-Head Challenges

- **The Mechanic:** Any member in our circle can stake velocity points by issuing an asynchronous bounty on a specific high-frequency problem (e.g., tagging a problem from the Blind 75).
- **The Psychology:** Challenges convert vague intent into a direct social challenge with a deadline.
- **Concrete Example:** A peer issues a 24-hour bounty on **"Trapping Rain Water (Hard)"** with a stake of 5 velocity points. If we fail to submit an accepted solution within 24 hours while our peer succeeds, our peer absorbs 5 points directly from our score.

#### 3. Dynamic "Stagnation" Status Badges (GitHub & LinkedIn Cards)

- **The Mechanic:** A self-updating SVG badge hosted by our service that we embed into our GitHub profile README or share as a weekly visual card on social media.
- **The Psychology:** Passive visibility. If we remain idle, our public status visibly degrades from "High Velocity (Top 10%)" to an amber or red "At Risk / Stagnant (Bottom Tier)".
- **Concrete Example:** When visitors open our GitHub profile, our header badge reads:
    `[DSA Status: Inactive for 48 Hours | Circle Rank: 5/5]`
    To turn that badge back to green, we must immediately push an accepted submission.

#### 4. The "Sliding Velocity Decay" Engine

- **The Mechanic:** Points earned are not static for 7 days; their value decays exponentially after 48 hours unless maintained by fresh solves.
- **The Psychology:** Prevents "weekend cramming." Cramming 6 problems on Sunday and going dormant from Monday to Thursday causes our rank to steadily bleed downward throughout the workweek.
- **Concrete Example:** If we solve **"LRU Cache"** on Monday for 3 points, that problem retains 3 points on Tuesday, drops to 1.5 points on Wednesday, and reaches 0 by Thursday, forcing daily consistency.

### How to Socialize This on LinkedIn (Step-by-Step Architecture)

To turn LinkedIn into an accountability surface, let us implement this workflow:

1. **The Initial Public Declaration (The Stake):** We write an opening post outlining the system:

    > _"We built an automated system that tracks our weekly coding velocity and hooks into the LinkedIn API. If our weekly problem threshold isn't met, our backend automatically publishes our failure metrics here every Sunday at midnight. No manual edits, no overrides."_

2. **Automated Visual Proof-of-Work (The Reward Post):** When we do succeed, our background worker uses headless Chromium (or an SVG template renderer) to generate a clean, dark-mode infographic card summarizing our weekly metrics:

    - 7-day velocity score
    - Hardest problem conquered (with our attached takeaway)
    - Current peer circle standing

3. **The Automated Failure Post (The Threat):** If the cutoff passes and our threshold is missed, the outbox worker dispatches the predefined failure post. The fear of this automated post going live in front of our professional network creates the necessary psychological stakes.
