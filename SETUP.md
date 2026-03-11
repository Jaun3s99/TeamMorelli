# Daversa Search Excellence — Setup Guide
## Two pages: Admin logs points → Leaderboard shows them live

---

## Step 1 · Create Your Supabase Database (~5 min, free)

1. Go to **supabase.com** → Sign up free
2. Click **New Project** → name it `daversa-leaderboard` → set a database password → Create
3. Wait ~1 minute for it to spin up
4. In the left sidebar, click **SQL Editor**
5. Paste this SQL and click **Run**:

```sql
create table points (
  id          bigint generated always as identity primary key,
  created_at  timestamptz default now(),
  date        text,
  name        text,
  category    text,
  section     text,
  points      integer,
  week        integer,
  notes       text,
  is_bonus    boolean default false
);

alter table points enable row level security;

create policy "Public read"   on points for select using (true);
create policy "Public insert" on points for insert with check (true);
create policy "Public delete" on points for delete using (true);
create policy "Public update" on points for update using (true);
```

6. Go to **Settings → API** (left sidebar)
7. Copy these two values — you'll need them shortly:
   - **Project URL** (looks like `https://xxxx.supabase.co`)
   - **anon public** key (long string starting with `eyJ`)

---

## Step 2 · Deploy to Vercel (~3 min, free)

1. Go to **vercel.com** → sign up with GitHub (or email)
2. Click **Add New → Project**
3. Choose **Deploy without a Git repository** → drag the `daversa-leaderboard` folder in
4. Click **Deploy**
5. Vercel gives you a URL like `daversa-leaderboard.vercel.app` — share this with your team

---

## Step 3 · First-Time Admin Setup

1. Open `yoursite.vercel.app/admin.html`
2. Default password is: **`daversa2026`** — change it on the setup screen
3. Paste in your Supabase URL and anon key
4. Enter your team members (one per line, exactly as you want them shown)
5. Set the season kickoff date
6. Click **Save & Enter Admin Panel**

The leaderboard (`index.html`) will ask for the same Supabase credentials on first load — paste them in.

---

## Step 4 · Logging Points (Admin's Daily Use)

**Open `admin.html` → log points in 3 clicks:**

1. **Who** — click the team member's name chip (can select multiple for team awards)
2. **Category** — click a section, then the specific activity (point value shown on each card)
3. **Notes + Submit** — add optional context, hit Log Points

**Special cases:**
- **"All Team" button** — applies the same deduction or bonus to every team member at once (use for team-wide events like "general mismanagement")
- **Handoffs (both people earn)** — select both team members' name chips, then pick "Organized handoff" → logs +15 to each person
- **Bonus points** — click the "⭐ Bonus" section → enter custom point value + reason

**Deleting a mistake:** Recent entries appear on the right side of admin — click 🗑 to remove

---

## Scoring System Reference

### 🏗 Foundational Execution
| Activity | Points |
|----------|--------|
| Search call notes (night before) | +5 |
| Action items notes (≤1hr post search call) | +5 |
| Game plan articulation / proactive strategy with PL | +10 |

### 🤝 Collaboration / Team-First
| Activity | Points |
|----------|--------|
| Smart AI leverage shared with team | +10 |
| Recruited candidate for someone else's search | +15 |
| Organized handoff (both people earn) | +15 each |
| 3+ qualified candidates intro'd in one week | +15 |

### 🎯 Candidate Generation / Conversion
| Activity | Points |
|----------|--------|
| Networking → sourced candidate | +10 |
| Candidate into process (past first convo) | +15 |
| Kept candidate in process when they tried to pull | +15 |

### 💎 Search Quality
| Activity | Points |
|----------|--------|
| Proactive client touchpoint / meaningful recap | +10 |
| Got ahead of comp & backchannels proactively | +15 |
| In-person meeting → candidate sticks | +20 |
| Sincere client shout-out (appreciation / loved candidate) | +20 |

### 🏆 Search Outcomes
| Activity | Points |
|----------|--------|
| Search closed — originated candidate (helped manage/prep) | +30 |
| Search closed — new to firm | +50 |
| Clean close (no comp drama, no backchannel surprises) | +25 |
| Repeat work & strong reference | +50 |

### ❌ Deductions
| Activity | Points |
|----------|--------|
| Client asked for something we should have provided | −5 |
| General mismanagement (blindsided by candidate/meeting) | −5 |
| Candidate clearly misqualified entering process | −5 |
| Missed issue / bad backchannel surprise (post R2) | −10 |
| Too much "I" vs "We" on search call | −15 |

---

## Prizes
- **Weekly Prize:** $500 (biggest points gain in that week)
- **Season Winner:** $5,000 (most total points across 8 weeks)
- **Team Multiplier:** Close 4 projects as a team → week off before Labor Day

---

## Tips
- Points auto-appear on the leaderboard within seconds of logging — no refresh needed
- The leaderboard auto-refreshes every 5 minutes
- Change the admin password in Settings (⚙ gear icon, top right of admin page)
- To update team members mid-season: Settings → edit the list → Save
- The "Admin can throw points for exceptional behaviour" feature is the ⭐ Bonus section in admin
