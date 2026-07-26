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

## Models
- For heavy/complex tasks, use `anthropic/claude-fable-5` (Dave's preference for extra power)
- Code review: simple → `anthropic/claude-opus-4-8`, complex → `anthropic/claude-fable-5`

## Anthropic Model Reference (as of 2026-07-22)
### Current / Recommended
- `claude-fable-5` — most capable, best for long-running agents ($10/$50 per MTok)
- `claude-opus-4-8` — complex agentic coding + enterprise ($5/$25 per MTok)
- `claude-sonnet-5` — best speed/intelligence balance ($3/$15, intro $2/$10 through 2026-08-31)
- `claude-haiku-4-5` — fastest, near-frontier ($1/$5 per MTok)
### Legacy (still available, consider migrating)
- `claude-opus-4-7`, `claude-opus-4-6`, `claude-sonnet-4-6` (current default), `claude-sonnet-4-5`, `claude-opus-4-5`
### Deprecated / Dead
- `claude-sonnet-4-20250514` — NO LONGER EXISTS (caused cron failures)
- `claude-opus-4-7` fallback also failed (model_not_found) — avoid as fallback

## Claude Code Delegation
- When working on CleoRx, delegate development work to Claude Code via the `claude` CLI on this Mac (David's Mac mini)
- CleoRx is an Xcode/iOS app — it lives at ~/src/cleorx on this Mac, NOT on edgar
- Verify Claude Code with `claude --version`
- Claude Code also available on edgar for aegis_server work
- Claude Code produces better code than OpenClaw writing directly — prefer delegating coding tasks to it
- aegis_server is a mature codebase with a lot of agent history — especially important to use Claude Code there
- My role: orchestrate, break down tasks, hand off to Claude Code, review results, coordinate across repos/specs

## File Delivery for Erin
- Erin communicates via Slack only — no Mac mini access
- When Erin asks for a file, always upload it directly to her Slack DM using the Slack files API
- Slack bot token has `files:write` confirmed working (tested 2026-07-21)
- Erin's Slack user ID: `U0BHC4RPACR`
- WebChat is a last resort only — not for Erin

## Pending Maintenance
- **OpenClaw update**: 2026.7.1 → 2026.7.1-2 (or 2026.7.2 pre-release) — defer to a good time; 2026.7.2 has cron + gateway recovery fixes worth getting
- **Test cron jobs**: `morning-maintenance` and `daily-backup` both have error backlogs — do a forced test run to confirm they work after today's fixes
- **Nightly gateway restart**: consider a 4 AM cron restart to address memory pressure (RSS hit 1.2 GB overnight)

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

## Promoted From Short-Term Memory (2026-05-01)

<!-- openclaw-memory-promotion:memory:memory/2026-04-24.md:290:292 -->
- - Candidate: Possible Lasting Truths: Possible Lasting Truths: Assistant: [[reply_to_current]] Hey Dave — OpenClaw update available: **2026.4.5 → 2026.4.12**. Run `openclaw update` whenever you're ready to apply it. 🦉 [confidence=0.49 evidence=memory/.dreams/session-corpus/2026-04-14.txt:2-2 - confidence: 0.62 - evidence: memory/2026-04-21.md:217-219 [score=0.926 recalls=0 avg=0.620 source=memory/2026-04-24.md:228-230]

## Promoted From Short-Term Memory (2026-07-25)

<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:33:33 -->
- Cron: watch-erin-message (10:33 PM): **Recommend:** Main session should disable/remove job `watch-erin-message` and instead check Erin's Slack DMs directly during next heartbeat [score=0.861 recalls=0 avg=0.620 source=memory/2026-07-20.md:33-33]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:40:40 -->
- Cron: watch-erin-message (11:33 PM): **Action needed at next heartbeat:** Check Erin's Slack DMs (U0BHC4RPACR), notify Dave if she messaged, and remove/disable job `watch-erin-message` [score=0.861 recalls=0 avg=0.620 source=memory/2026-07-20.md:40-40]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:29:32 -->
- Cron: watch-erin-message (10:33 PM): Ran again from isolated cron context — same restriction as all prior runs; Session visibility still restricted to own tree; cannot reach Erin's or Dave's Slack sessions; Job NOT removed — cannot confirm message status; **This job cannot function as designed from an isolated cron context** [score=0.861 recalls=0 avg=0.620 source=memory/2026-07-20.md:29-32]

## Promoted From Short-Term Memory (2026-07-26)

<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:22:25 -->
- Cron: watch-erin-message (8:53 PM): Ran from isolated cron context; session visibility restricted to own tree; Could NOT access Erin's Slack DM session (U0BHC4RPACR) or Dave's Slack session; Could NOT send wake event (cron tool restricted to self-management only); Job NOT removed — unable to confirm Erin's message status [score=0.844 recalls=0 avg=0.620 source=memory/2026-07-20.md:22-25]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:26:26 -->
- Cron: watch-erin-message (8:53 PM): **Action needed:** Dave or main session should manually check Erin's Slack DMs and remove job `watch-erin-message` once confirmed [score=0.844 recalls=0 avg=0.620 source=memory/2026-07-20.md:26-26]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:36:39 -->
- Cron: watch-erin-message (11:33 PM): Fifth consecutive failed run — isolated cron cannot access Erin's Slack DM session or Dave's session; Session visibility locked to own tree (tree-restricted); all external session reads forbidden; Job NOT removed; cannot confirm whether Erin has messaged; **Persistent issue:** This job has never been able to function. Main session must handle this manually. [score=0.844 recalls=0 avg=0.620 source=memory/2026-07-20.md:36-39]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:12:12 -->
- watch-erin-message cron (3:18 PM PDT): This note is for the main session to pick up at next heartbeat. [score=0.812 recalls=0 avg=0.620 source=memory/2026-07-20.md:12-12]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:7:7 -->
- watch-erin-message cron (3:18 PM PDT): **Action needed (main session):** [score=0.812 recalls=0 avg=0.620 source=memory/2026-07-20.md:7-7]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:19:19 -->
- watch-erin-message Cron Run (6:23 PM): **Action needed:** On next heartbeat, check if Erin (U0BHC4RPACR) has sent any DMs. If yes, notify Dave and remove cron job `watch-erin-message`. [score=0.812 recalls=0 avg=0.620 source=memory/2026-07-20.md:19-19]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:15:18 -->
- watch-erin-message Cron Run (6:23 PM): Cron job fired as scheduled; Could NOT check Erin's Slack messages: isolated cron context, session visibility restricted (tree mode); Could NOT send to Dave's Slack session: forbidden from isolated context; Could NOT wake main session: cron tool restricted to current job only [score=0.812 recalls=0 avg=0.620 source=memory/2026-07-20.md:15-18]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:5:5 -->
- watch-erin-message cron (3:18 PM PDT): The cron job `watch-erin-message` fired but couldn't check Erin's Slack DMs — session visibility is restricted to isolated cron tree. Could not reach `agent:main:slack:direct:U0BHC4RPACR` or notify Dave's main session. [score=0.812 recalls=0 avg=0.620 source=memory/2026-07-20.md:5-5]
<!-- openclaw-memory-promotion:memory:memory/2026-07-20.md:8:10 -->
- watch-erin-message cron (3:18 PM PDT): Check if Erin (Slack U0BHC4RPACR) has sent any new messages; If yes: notify Dave and remove cron job `watch-erin-message`; If no: leave cron job running [score=0.812 recalls=0 avg=0.620 source=memory/2026-07-20.md:8-10]
