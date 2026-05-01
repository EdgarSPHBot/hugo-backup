# MEMORY.md - Long-Term Memory

## Accounts & Identity
- **Apple ID:** hugo@spectatorhealth.com (set 2026-02-24)
- **GitHub:** HugoSPHBot (hugo@spectatorhealth.com, set 2026-02-24) — SSH key at ~/.ssh/id_ed25519, confirmed working

## People
- **Dave** — my human. Has another OpenClaw install named Edgar. Timezone: America/Los_Angeles (PST).

## GitHub Repos
- **hugo-backup** — private repo, workspace backup. Remote: git@github.com:HugoSPHBot/hugo-backup.git. Back up every morning.
- **hugo-tools** — private repo, custom tools & scripts source. Push new tools here when created.

## Gateway
- Installed as a proper LaunchAgent service (as of 2026-02-25, v2026.2.24)
- Start: `openclaw gateway start`
- Stop: `openclaw gateway stop`
- Restart: `openclaw gateway restart`
- Status: `openclaw gateway status`
- Auto-starts on login via ~/Library/LaunchAgents/ai.openclaw.gateway.plist

## Morning Routine
1. `cd /Users/edgar/.openclaw/workspace && git add -A && git commit -m "Morning backup - YYYY-MM-DD" && git push` → hugo-backup
2. Check HEARTBEAT.md for any pending tasks

## Behavior Notes
- **iMessage etiquette:** Always acknowledge receipt of a message first before jumping into any work. Don't silently start executing tasks.

## Notes

## LaunchAgent Fix (2026-02-26)
After switching node versions (nvm), the LaunchAgent plist had the wrong node path, causing SIGTERM crash loops and gateway not surviving reboots.

**Fix sequence (must source nvm first or commands won't find the right node):**
```
source ~/.nvm/nvm.sh
nvm use default
npm install -g openclaw
openclaw gateway stop
openclaw gateway install
```

Also added a bootstrapper plist (`ai.openclaw.gateway.bootstrap`) at `~/Library/LaunchAgents/` that calls `launchctl bootstrap` on every login — workaround for macOS Sequoia bug where `openclaw gateway stop` calls `launchctl bootout` and permanently unregisters the service.

**iMessage fix (updated 2026-04-02):** Two permissions required when node version changes:
1. **Full Disk Access** — add `/Users/edgar/.nvm/versions/node/<version>/bin/node` in System Settings → Privacy & Security → Full Disk Access
2. **Automation** — approve Messages.app control in System Settings → Privacy & Security → Automation (this may prompt interactively; approve it)
After granting both, restart the gateway. Note: `imsg` is legacy — BlueBubbles is the recommended iMessage connector going forward.

## Promoted From Short-Term Memory (2026-04-26)

<!-- openclaw-memory-promotion:memory:memory/2026-04-19.md:172:174 -->
- - Candidate: Possible Lasting Truths: User: Read HEARTBEAT.md if it exists (workspace context). Follow it strictly. Do not infer or repeat old tasks from prior chats. If nothing needs attention, reply HEARTBEAT_OK. When reading HEARTBEAT.md, use workspace file /Users/edgar/.openclaw/workspace - confidence: 0.62 - evidence: memory/2026-04-18.md:242-244 [score=0.845 recalls=0 avg=0.620 source=memory/2026-04-19.md:18-20]

## Promoted From Short-Term Memory (2026-04-28)

<!-- openclaw-memory-promotion:memory:memory/2026-04-22.md:237:239 -->
- - Candidate: Possible Lasting Truths: Possible Lasting Truths: Assistant: [[reply_to_current]] Hey Dave — OpenClaw update available: **2026.4.5 → 2026.4.12**. Run `openclaw update` whenever you're ready to apply it. 🦉 [confidence=0.49 evidence=memory/.dreams/session-corpus/2026-04-14.txt:2-2 - confidence: 0.62 - evidence: memory/2026-04-21.md:217-219 [score=0.879 recalls=0 avg=0.620 source=memory/2026-04-22.md:18-20]

## Promoted From Short-Term Memory (2026-04-29)

<!-- openclaw-memory-promotion:memory:memory/2026-04-23.md:257:259 -->
- - Candidate: Possible Lasting Truths: Possible Lasting Truths: Assistant: [[reply_to_current]] Hey Dave — OpenClaw update available: **2026.4.5 → 2026.4.12**. Run `openclaw update` whenever you're ready to apply it. 🦉 [confidence=0.49 evidence=memory/.dreams/session-corpus/2026-04-14.txt:2-2 - confidence: 0.62 - evidence: memory/2026-04-21.md:217-219 [score=0.879 recalls=0 avg=0.620 source=memory/2026-04-23.md:148-150]

## Promoted From Short-Term Memory (2026-05-01)

<!-- openclaw-memory-promotion:memory:memory/2026-04-24.md:290:292 -->
- - Candidate: Possible Lasting Truths: Possible Lasting Truths: Assistant: [[reply_to_current]] Hey Dave — OpenClaw update available: **2026.4.5 → 2026.4.12**. Run `openclaw update` whenever you're ready to apply it. 🦉 [confidence=0.49 evidence=memory/.dreams/session-corpus/2026-04-14.txt:2-2 - confidence: 0.62 - evidence: memory/2026-04-21.md:217-219 [score=0.926 recalls=0 avg=0.620 source=memory/2026-04-24.md:228-230]
