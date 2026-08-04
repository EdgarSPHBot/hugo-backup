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

## Promoted From Short-Term Memory (2026-08-02)

<!-- openclaw-memory-promotion:memory:memory/2026-07-29.md:20:22 -->
- Config Notes: OpenAI provider in `openclaw.json` has `baseUrl: https://api.openai.com/v1`; `organizationId` is NOT a valid OpenClaw config key for the OpenAI provider — do not use it; Org ID can be passed via curl header `OpenAI-Organization: <org-id>` for manual testing [score=0.806 recalls=0 avg=0.620 source=memory/2026-07-29.md:20-22]

## Promoted From Short-Term Memory (2026-08-03)

<!-- openclaw-memory-promotion:memory:memory/2026-07-29.md:6:9 -->
- Google Image Gen Fix: Erin was seeing: `Image generation failed: Google Generative AI baseUrl must be a valid https URL on generativelanguage.googleapis.com`; Root cause: Google provider config was missing an explicit `baseUrl`, causing the SDK to receive a bare hostname without `https://` scheme; Fix: Added `"baseUrl": "https://generativelanguage.googleapis.com"` to the Google provider in `openclaw.json`, restarted gateway; Resolved ✅ [score=0.861 recalls=0 avg=0.620 source=memory/2026-07-29.md:6-9]
<!-- openclaw-memory-promotion:memory:memory/2026-07-29.md:16:17 -->
- OpenAI Billing Hard Limit: Eventually resolved after Dave adjusted billing limits on platform.openai.com; Confirmed working: OpenAI `gpt-image-1.5` generated a great horned owl image successfully ✅ [score=0.829 recalls=0 avg=0.620 source=memory/2026-07-29.md:16-17]

## Promoted From Short-Term Memory (2026-08-04)

<!-- openclaw-memory-promotion:memory:memory/2026-07-29.md:12:15 -->
- OpenAI Billing Hard Limit: OpenAI image gen was failing with HTTP 400 `billing_hard_limit_reached`; The account had a very low hard spending cap (showed ~$0.01 in control panel); Dave regenerated the OpenAI API key (service account key, last 4 chars: `PJQA` was old key); Also added org ID `org-y6xNM0HEwClFSV6heMhMZn3t` — note: OpenClaw config doesn't support `organizationId` field (rejected as unrecognized key), had to remove it [score=0.844 recalls=0 avg=0.620 source=memory/2026-07-29.md:12-15]
