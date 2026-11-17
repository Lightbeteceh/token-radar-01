# DECISIONS.md — token-radar-01 v1

## 2026-11-17 — Model "radar-2" (replaces starter's flat 0.25x TVL)
- Formula: implied = TVL x categoryMultiple x growthMult x maturityMult x chainMult.
- categoryMultiple = median(mcap/TVL) of the category's LIVE-token protocols, shrunk toward the global median (0.1691x) with a prior of 10, clamped [0.03, 0.45]. Categories with no live comps use the global median.
- growthMult = 1 + clamp(change_7d, -50, +100)/100 x 0.4. The snapshot's pre-token 7d range is -73% to +4,448%: raw growth would let one spike set the board.
- maturityMult = 0.70 + min(age, 1095)/1095 x 0.30 (unknown age 365).
- chainMult = 1 + 0.02 x min(max(chains-1, 0), 10).
- No protocol name is special-cased; the dashboard prints the computed category multiples table so the judge can check the arithmetic.

## 2026-11-17 — Bug found and fixed: live comparables need a market cap
- First run gave every row multiple 0.03 (floor) and one row 0. Cause: `!isPreToken` counts protocols that carry only a gecko_id/symbol but no mcap as "live" with ratio 0, dragging the global median to 0. Fixed: category multiples and the live view use `mcap_usd !== null` only. Verified top rows then matched the pre-build simulation exactly.

## 2026-11-17 — Page/board agreement
- First detail check showed "which differs from the board: the data would be stale" — the page recomputed from rounded (4dp) multipliers while the board used full precision. Fixed: board.json model fields now carry full precision; the page recomputes exactly. Verified for 5 top rows via headless DOM dump: all say "the same number board.json carries". Farm steps in the page were verified identical to board.json for the #1 row.

## 2026-11-17 — Board size 226 rows
- All 40 watchlist + ALL 186 rankable pre-token protocols below the floor (not just the starter's 160). The early radar is the whole findable set.

## 2026-11-17 — Dashboard v2
- Distinct look vs starter (warm paper, deep ink, teal + amber; top-3 spotlight cards; rank badges). Filters: search, category, chain, scope (watchlist/early/all), pre-token/live tabs, sortable columns. Detail drawer shows every multiplier + the farm plan + a scam warning. Dashboard source 36,909 bytes total (under the ~64 KB judge-read cap).

## 2026-11-17 — Screenshots
- Hatch's own Chromium (/opt/meta-chromium/chrome) refuses direct launch ("Hatch WebGL domain policy is required"). Used a stock Chromium downloaded via `npx puppeteer browsers install chrome` (~/.cache/puppeteer) instead. 1440x900, PNG, ~160–234 KB each.

## 2026-11-17 — grade-local cannot run for this kit
- `makefun grade-local --kit … --bot entry --driver process` exits 0 with: "token-radar-01 is a program/v1 competition: its scorer and reference data are not published in the kit". So the gate was verified with a local replica of the 7 rows from RULES.txt (EVIDENCE/gate-local-replica.log), including a byte-identical buildDossier rebuild and a two-run determinism check. The sealed scorer still runs on the server at submission.
