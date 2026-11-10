# Football Player Database — SQL Analysis

**A 17-table normalized SQLite database of 27,343 football players, analyzed SQL-first.**

## Dataset
- 27,343 players, 108,639 player-seasons (~4 per player)
- Star schema: hubs `players` and `player_seasons`; 5 vertically-partitioned stat tables;
  dimensions `clubs → divisions`, `nations`, `positions`, `seasons`, `agents`

## What I built (in order)
1. **Schema map** — traced foreign keys from SQLite's catalog; documented the star schema and join paths
2. **Player-season overview** — JOIN from the fact table outward; 1:1 stats joins (no fan-out)
3. **Top scorers per season** — `RANK() OVER (PARTITION BY season ORDER BY goals_per_90)`, min-900-min filter
4. **Injury downtime** — `julianday()` date math; NULL handling for ongoing injuries
5. **Transfer spend by division** — multi-hop JOIN; self-referential FK (`to_club_id`)
6. **Cumulative injuries** — `SUM(COUNT()) OVER (ORDER BY ...)`; caught a reversed-ordering bug
7. **Capstone: wage vs. performance** — see below

## Capstone: does wage buy performance?

**Naive answer:** barely. Goals/90 is nearly flat across wage bands (~0.01–0.03 gap).

**Diagnosis:** goals are position-biased — ST 0.349 vs GK 0.000. Pooling across
positions dilutes any wage signal.

**Corrected outcome:** `ability_score` (position-adjusted) rises **+74 points per wage band**
(520 → 609 → 683). Wage *does* buy quality.

**Proof of confound:** assists rank M > AM > DM > ST (the *opposite* of goals) —
so no single stat measures "performance."

**Goalkeepers:** high-wage GKs make more saves (3.29 vs 2.66) and save a higher ratio
(75.7% vs 70.1%) — but prevent *fewer* expected goals (−0.006 vs +0.075). They face
harder shots; only the quality-adjusted metric tells the truth.

## Thesis
**Wage buys environment, not edge.** Higher wage tracks higher overall ability and more
raw volume (goals, saves), but does **not** improve quality-adjusted overperformance
(xG, xGP). Expensive players are in better systems, not better relative to expectation.
Any wage–performance analysis using raw volume metrics will overstate expensive players.

## Debugging notes
- **Caught a silent ordering bug:** the cumulative-injury window initially counted
  *backward* in time — `season_order` ran descending. Verified against known rows and
  added `DESC`. Silent ordering bugs in window functions produce plausible but inverted output.
- **Verified column locations before joining:** stats are split across 5 themed tables;
  goals live in `player_stats_attacking`, rating in `player_stats_general`.

## Limitations
- Event tables (transfers, injuries) are **100% populated** — synthetic by design.
  Reported *patterns* (rank, duration, distribution), not *frequencies*.
- No birthdate column; age taken from `player_seasons.age`.
- `player_positions` is player-level, not season-level → position breakdown counts players.
- Differences across wage bands are small (0.01–0.03 goals/90); results are directional,
  not significance-tested.
