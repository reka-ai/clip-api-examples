# Project Context

- **Owner:** Frank Boucher
- **Project:** clip-api-examples — examples of using the Reka Clips API across multiple languages
- **Stack:** Python, JavaScript (Node), C# (.NET), and now Rust
- **Created:** 2026-04-13

## Learnings

<!-- Append new learnings below. Each entry is something lasting about the project. -->

### README Pattern (from Python)
- H1: "{Language} Clip Tools"
- Brief one-liner description
- ## Setup section: numbered steps (install deps, set env var)
- ## Scripts section: subsections per script with usage command and description
- Each script subsection mentions: what it does, how to run it, what happens (Job ID, polling, etc.)
- Sample Output: screenshot reference `![description](assets/screenshot.png)` — placeholder if no screenshot yet
- ## Links section: Reka API Docs + Reka Discord

### Key Details for Rust README
- Install: `cargo build` (or `cargo run`)
- Env var: `export REKA_API_KEY=your_key_here`
- Run clip_generator: `cargo run --bin clip_generator`
- Run check_status: `cargo run --bin check_status`

## Work Log

### 2026-04-13: McManus created rust/README.md
- Created `/rust/README.md` matching Python README structure exactly
- Setup: rustup link, cargo build, API key export
- Scripts section: clip_generator and check_status with cargo run commands
- Sample output image placeholders ready for Keaton's assets
- Links section complete
