# GitHub README

# Football Player Database — SQL Analysis

**17-table normalized SQLite DB (27,343 players, 108,639 player-seasons) analyzed SQL-first.**

Repo: https://github.com/transparentsemimoltensand/Sql_Project_Football/tree/main

## Project
Mapped the schema from SQLite's catalog and foreign-key metadata, then built escalating
SQL analyses: multi-table JOINs, window functions, date logic, multi-hop joins, and a
capstone testing whether player wage relates to performance.

## Stack
SQL (SQLite), Python (connection + ipython-sql), Kaggle Notebook.

## Key findings
- **Naive result:** goals/90 barely varies by wage band (~0.01–0.03 gap) — looks like wages don't matter.
- **Diagnosis:** goals are position-biased (ST 0.349 → GK 0.000); pooling across positions
  dilutes the signal.
- **Correction:** position-adjusted `ability_score` rises +74 points per wage band
  (520 → 609 → 683) — wage relates to overall quality.
- **Supporting evidence:** assists rank M > AM > DM > ST — the opposite of goals — so no
  single stat measures performance.
- **Goalkeepers:** high-wage GKs make more saves (3.29 vs 2.66) and save a higher ratio
  (75.7% vs 70.1%) but prevent slightly fewer expected goals (−0.006 vs +0.075).
- **Thesis:** *wage tracks environment more than edge* — higher wage aligns with ability and
  raw volume, but not with quality-adjusted overperformance (xG, xGP).

## Skills demonstrated
- Multi-table JOINs and join-path planning from a foreign-key graph
- Window functions (`RANK`, `SUM() OVER`, running totals over aggregates)
- Date logic with `julianday()`; NULL handling
- Multi-hop joins; self-referential FKs (aliased `clubs`)
- Confound diagnosis: identifying position bias and switching to a position-adjusted outcome
- Data-quality judgement: identifying synthetic event tables and reporting patterns, not frequencies

## Limitations
- Event tables are 100% populated (synthetic by design) — reported patterns, not frequencies.
- No birthdate column; age from `player_seasons.age`.
- Wage-band differences are small (0.01–0.03 goals/90); directional, not significance-tested.


---

# Naukri — Project

**Title:**
SQL Analysis — Football Player Database (17 tables)

**Description:**
Analyzed a 17-table normalized SQLite DB (27k players, 108k player-seasons). Built
JOINs, window functions (RANK, running totals), date logic, and multi-hop joins.
Capstone: tested whether wage relates to performance — found goals/90 flat due to position
bias; position-adjusted ability rose +74/band. Findings are directional, not significance-tested.
Skills: SQL, SQLite, window functions, confound diagnosis.

**Skills tags:**
SQL, SQLite, Window Functions, Data Analysis, Joins, Python


---

# LinkedIn — Projects

**Project name:**
Football Player Database — SQL Analysis

**Description:**
Analyzed a 17-table normalized SQLite database (27,343 players, 108,639 player-seasons)
entirely in SQL. Mapped the schema via foreign-key metadata, then built escalating analyses:
multi-table joins, window functions (RANK, running totals over aggregates), date logic with
julianday, and multi-hop joins with self-referential keys.

Capstone: does wage relate to performance? The naive answer was flat — goals/90 barely varied
by wage. I diagnosed a position confound (strikers 0.349 goals/90 vs keepers 0.000), then
switched to a position-adjusted outcome where ability rose +74 points per wage band. Assists
rank midfielders above strikers — the opposite of goals — supporting that no single metric
captures performance. For goalkeepers, higher-wage keepers made more saves but prevented
slightly fewer expected goals.

Takeaway: wage aligns with overall ability and raw volume, but not with quality-adjusted
overperformance (xG/xGP). Results are directional; differences are small and not
significance-tested. Stack: SQL (SQLite), Python, Kaggle.

**Skills:**
SQL, SQLite, Window Functions, Data Analysis, Python


---

# Resume — 1–2 Line Bullet

**SQL Analysis — Football Player Database | SQL, SQLite, Window Functions**
• Analyzed a 17-table normalized DB (27k players) using joins, window functions, and date
  logic; diagnosed a position confound in wage-performance analysis, showing wage aligns
  with overall ability but not quality-adjusted overperformance (xG/xGP).
