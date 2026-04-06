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
- Key databases: `sph_focus`, `fdb_20260219` (latest FDB snapshot), `hedis_2025_valuesets`, `medicare_formulary_20250821`, `snomed_ct_us_1000124_20250301`
- Connect: `mongosh "mongodb+srv://[MONGO_USER:MONGO_PASS]@dev-fdb-01.qpkxl.mongodb.net/"`

## MongoDB (HEDIS Certification - sph-cloud.net)
- URI: `mongodb://mongo-hedis.sph-cloud.net:27017/`
- Purpose: HEDIS MY2025 certification testing — one DB per measure (AAB, CBP, EED, etc.) with SAMPLE and TEST_A decks
- Also has: `hedis_2025_valuesets`, `amp_2025_valuesets`, `ltss_2025_valuesets`, `sh2025_cms_hcc`
- Connect: `mongosh "mongodb://mongo-hedis.sph-cloud.net:27017/"`

Add whatever helps you do your job. This is your cheat sheet.
