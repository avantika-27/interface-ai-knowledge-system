# Dupaco temporal knowledge system

Submission for the interface.ai Software Engineer II build assignment.

## Run

From the participant kit root (with snapshots available locally, not in this public repo):

```bash
python harness/run_eval.py --submission solution --eval eval/public_eval.jsonl
```

Public-eval score on this machine: **~0.97** accuracy, p95 answer latency **~0.05s**, no third-party packages or API keys.

## Layout

| File | Role |
|------|------|
| `solution.py` | `build()` → `ingest` / `answer` / `conflicts` |
| `requirements.txt` | Empty of third-party deps (stdlib only) |
| `NOTES.md` | Approach, authority rules, “current” semantics |

See `NOTES.md` for design details.
