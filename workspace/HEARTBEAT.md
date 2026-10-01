# HEARTBEAT.md

Keep this short. Checks to rotate through during heartbeats.

## Backup size (once a day is enough)
- Run `bash /Users/edgar/.openclaw/workspace/scripts/check-backup-size.sh`
- Exit 0: say nothing. Exit 1 (WARNING, >= 75 MB) or 2 (CRITICAL, >= 90 MB / repo missing): tell Dave which file and its size.
- GitHub rejects files over 100 MB, which would break the daily `openclaw-backup-scheduled` push. Biggest risk: `memory_embedding_cache.jsonl` (61 MB on 2026-09-30).
- Record the run in memory/heartbeat-state.json under lastChecks.backupSize.
