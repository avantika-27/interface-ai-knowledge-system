# interface.ai knowledge-system assignment

Temporal knowledge system over five Dupaco website snapshots: answers what’s true *now*, resolves conflicts, cites sources, and refuses when the site doesn’t say.

## Submission folder

```
solution/
  solution.py      # build() → ingest / answer / conflicts
  requirements.txt # stdlib only — no API keys
  NOTES.md         # approach & authority rules
```

## Score (public eval)

```bash
python harness/run_eval.py --submission solution --eval eval/public_eval.jsonl
```

| Pillar | Result |
|--------|--------|
| Accuracy | ~0.97 |
| Consistency | 1.0 (× accuracy) |
| Speed | p95 ~0.05–0.09s |
| Final (public, no conflicts-gold) | **~0.97** |

## Notes

- Website snapshots are **not** in this repository (per assignment rules). Graders use their own copy.
- No paid APIs or environment variables required.
