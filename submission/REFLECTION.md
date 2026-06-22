# Lab 18 Reflection — Top 5 Lakehouse Anti-Patterns

## Which anti-pattern would our team be most at risk of, and why?

Among the Top 5 Lakehouse Anti-Patterns, our team would be most at risk of the
**Small-File Problem** (Anti-Pattern #3: Inconsistent / Ad Hoc Ingestion).

In an LLM observability pipeline like the one built in this lab, every API call
to Claude Haiku, Sonnet, or Opus generates a near real-time event. A naive
streaming approach — appending one micro-batch per inference call — would quickly
create hundreds of thousands of tiny Parquet files, exactly the scenario we
reproduced in NB2 with 200 back-to-back appends. Before OPTIMIZE + Z-ORDER, a
simple point-query on `user_id` had to open and scan every file. After compaction
and Z-ordering, the same query skipped all but a handful of files, achieving a
files-pruned ratio well above the 10× target.

The root cause is architectural: high-frequency, low-volume writes are the
natural shape of LLM traffic, yet Delta Lake's performance depends on having
reasonably sized files with accurate min/max statistics. Without a scheduled
OPTIMIZE job (or auto-compaction), the table degrades silently — queries slow
down, storage costs grow, and engineers only notice when dashboards time out.

The fix is to treat compaction as a first-class pipeline step, not an afterthought.

*(Word count: ≈ 190)*
