# Approach

## What “current” means

Snapshots are ingested oldest → newest. For a question with no `as_of`, answers come from the **latest snapshot** (`05_…_latest`). With `as_of`, only snapshots whose `taken_on` is on or before that date are used, and we take the newest allowed version of each URL.

## Authority rules

Not every page that mentions a rate is equal:

1. **Official product / rate pages** (`/personal/loans/…`, `/personal/savings-account`, credit-card pages, `/contact`, `/about/join`) rank highest.
2. **Calculators, switch-and-earn promos, blogs, and old newsroom boilerplate** rank lower — they often keep stale APRs (e.g. auto 5.34% vs official 5.39%).
3. When the same fact key (product + term + tier + metric) appears with different values, we pick the highest-authority value and record a conflict.

Tiers are treated as different facts: 48-month vs 60-month, Share Savings `$10k–$24,999` vs `$25k+`, mortgage `$100k` vs `$832,750`, standard vs jumbo certificates, rate vs APR/APY.

## How answering works

1. Parse markdown **tables** into structured facts at ingest time.
2. Extract **entities** (routing number, branch counts, hours, closures, Forbes awards, URLs, etc.).
3. **Route** the question by intent (rates, hours, membership, refuse cases, …) over those structures.
4. Fall back to lightweight **BM25** retrieval over pages, still biased by authority.
5. **Refuse** when the site does not publish the asked value (e.g. 7/1 ARM rate, construction-loan rate, Mullan Avenue hours).

## Conflicts

`conflicts()` groups disagreeing values for the same fact key in the latest snapshot, plus known entity conflicts (branch-count boilerplate vs current 22 after Hy-Vee closure; Forbes “fourth” vs “fifth”).

## Dependencies / API keys

**None.** Standard library only — no embeddings API, no LLM at answer time — so answers stay fast (well under the 2s p95 target) and reproducible in a clean Python 3.11 environment.
