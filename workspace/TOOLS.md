# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

## AWS Q Business (QB)
- Shorthand: "QB" = this service
- Application ID: `1b2dcad6-c48e-4f28-ba6e-b10e4a8e476f`
- Region: `us-west-2`
- Access: MCP server via Docker on edgar (`mcp/amazon-qbusiness-anonymous-mcp-server`)
- Config: OpenClaw MCP server named `qbusiness`, pipes via `ssh edgar docker run ...`
- Env: `~/.aws/qbusiness.env` (on both this Mac and edgar)
- Purpose: Spectator Health knowledge base — FDB specs, formularies, and other internal docs
- Usage: Query via the `chat_sync` MCP tool; say "QB" to mean this service

## Figma MCP Server
- Local endpoint: `http://127.0.0.1:3845/mcp`
- Requires: Figma desktop app open + Dev Mode (Shift+D) + MCP server enabled
- Connect: `mcporter list http://127.0.0.1:3845/mcp --allow-http`
- Key tools: get_design_context, get_screenshot, get_variable_defs, get_metadata
- Usage: Select a frame in Figma → ask me to implement it → I pull specs via MCP

## Figma REST API
- Personal access token: `[FIGMA_PAT]`
- Scopes: Files (read/write), Design systems (read)
- Project: MiniMobile (need file key from URL)
- File key: `TYhFhRAzs1nTokclbQBJK6` (MiniMobile, Page 1)
- File key: `cr2l2yq0YFn6PGR3luD1tk` (Mobile App — iOS app reference, page: "Mobile Screens")
- File key: `FF0O3AiVbjlIr6tuk2RavO` (Responsive-UI — pages: "Screens - New", "Components", "Styles", "Screens - Old", "Screens - Old 2", "Screens - Old 3")

## MongoDB (Atlas - Dev Cluster)
- URI: `mongodb+srv://[MONGO_USER:MONGO_PASS]@dev-cluster-02.qpkxl.mongodb.net/`
- Key databases: `aegis-qa` (largest/main), `aegis-cert`, `aegis-demo`, `aegis-test`, `aegis-master-dev`
- Connect: `mongosh "mongodb+srv://[MONGO_USER:MONGO_PASS]@dev-cluster-02.qpkxl.mongodb.net/"`

## MongoDB (Focus DB - Atlas dev-fdb-01)
- URI: `mongodb+srv://[MONGO_USER:MONGO_PASS]@dev-fdb-01.qpkxl.mongodb.net/`
- Purpose: State data / "focus database" — FDB drug snapshots, formularies, value sets, SNOMED CT
- Key databases: `sph_focus`, `fdb_20260709` (latest FDB snapshot), `hedis_2025_valuesets`, `medicare_formulary_20250821`, `medicare_formulary_2026_20260331`, `snomed_ct_us_1000124_20250301`
- Connect: `mongosh "mongodb+srv://[MONGO_USER:MONGO_PASS]@dev-fdb-01.qpkxl.mongodb.net/"`
- Note: mongosh runs locally on this Mac (v2.7.0); also accessible from edgar via SSH

## MongoDB (HEDIS Certification - sph-cloud.net)
- URI: `mongodb://mongo-hedis.sph-cloud.net:27017/`
- Purpose: HEDIS MY2025 certification testing — one DB per measure (AAB, CBP, EED, etc.) with SAMPLE and TEST_A decks
- Also has: `hedis_2025_valuesets`, `amp_2025_valuesets`, `ltss_2025_valuesets`, `sh2025_cms_hcc`
- Connect: `mongosh "mongodb://mongo-hedis.sph-cloud.net:27017/"`

Add whatever helps you do your job. This is your cheat sheet.

## Aegis Server (CleoRx Project)
- *Repo:* `git@github.com:SpectatorHealth/aegis_server.git`
- *Working branch:* `master`
- *Server host:* `edgar` (SSH via ~/.ssh/config → 100.70.3.21, user: david)
- *Checkout:* `edgar:~/src/aegis_server`
- *Mobile BFF:* `src/aegis_mobile/` — port 15170, Pistache + Cognito JWT, flat JSON (no envelope)
- *Build:* `~/src/aegis_server/scripts/build-aegis.sh` (general build; aegis_mobile is part of it)
  - Can be called from anywhere in the repo tree, e.g. `../../scripts/build-aegis.sh` from `src/aegis_mobile/`
  - Fast mode auto-detected (checks for new #includes, untracked/renamed sources); override with `--fast` / `--no-fast`
  - Automatically applies `--max-drift=1 --implicit-deps-unchanged` when safe
  - `sb` alias on edgar = hedis fast build (different target, not for mobile)
- *Figma project:* CleoRx — file key `R4yrbcFrVb0OYydf8CEESt` (token: `[FIGMA_PAT]`)
- *Collaborator:* Erin (UI/UX, Figma) — Slack `U0BHC4RPACR`
- *Workflow:* Erin updates Figma → tells me in Slack → I update iOS + aegis_mobile API as needed

## CleoRx iOS App
- *Repo:* `git@github.com:SpectatorHealth/cleorx.git`
- *Working branch:* `main`
- *Checkout:* `edgar:~/src/cleorx`
- *Stack:* SwiftUI, XcodeGen (`project.yml` → `.xcodeproj`; never hand-edit the project file)
- *Build:* `xcodebuild build -project CleoRx.xcodeproj -scheme CleoRx -destination 'generic/platform=iOS Simulator'`
- *API:* All data via `aegis_mobile` BFF (flat JSON, no envelope) — never query MongoDB directly
- *Auth:* Cognito JWT via `AuthService` → `oauth-v2.sph-dev.net`
- *Figma spec:* File key `R4yrbcFrVb0OYydf8CEESt` — "00 - Read Me (for Claude Code)" frame is the living build spec
- *Screens built:* Splash, Login, Drug Search, Drug Forms, Drug Packages, Bottom tab bar, More
- *Next up:* Drug Search Rx-tab endpoints in aegis_mobile + remaining screens per Figma build order
