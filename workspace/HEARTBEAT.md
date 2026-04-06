# HEARTBEAT.md

# Keep this file empty (or with only comments) to skip heartbeat API calls.

# Add tasks below when you want the agent to check something periodically.

## Morning Backup (run once per day, first heartbeat after 08:00 PST)
- Check memory/heartbeat-state.json to see if backup has run today
- If not: git add -A, commit "Morning backup - YYYY-MM-DD", push to hugo-backup
- Update heartbeat-state.json with backup timestamp
