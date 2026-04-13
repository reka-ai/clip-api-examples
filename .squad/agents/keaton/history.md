# Project Context

- **Owner:** Frank Boucher
- **Project:** clip-api-examples — examples of using the Reka Clips API across multiple languages
- **Stack:** Python, JavaScript (Node), C# (.NET), and now Rust
- **Created:** 2026-04-13

## Learnings

<!-- Append new learnings below. Each entry is something lasting about the project. -->

### Project Structure
- Each language lives in its own top-level directory: `python/`, `javascript/`, `dotnet/`, etc.
- Each directory contains: `clip_generator.{ext}`, `check_status.{ext}`, `README.md`, `assets/`
- The Rust example should follow this exact same pattern under `rust/`

### API Details
- Base URL: `https://vision-agent.api.reka.ai/v1/clips`
- Auth: `X-Api-Key` header with value from `REKA_API_KEY` env var
- clip_generator: POST to BASE_URL with streaming response (SSE: `data: {json}` lines)
- check_status: GET to `{BASE_URL}/{job_id}` polling every 30 seconds
- Job statuses: in-progress, completed, failed
- Output on completion: array of clips with title, video_url, caption, hashtags

### Existing Example Pattern (Python as reference)
- clip_generator: prompts user for YouTube URL, POSTs with streaming, prints Job ID + status updates, prints clip details on completion
- check_status: prompts user for Job ID, polls every 30s, prints results on completion or error on failure
- Both scripts print banner header, separator lines, "Done!" at end

## Implementation Log

### 2026-04-13: Rust Implementation Complete

**What was built:**
- Created `rust/` directory with full Reka Clips API implementation
- Two binaries: `clip_generator` and `check_status`
- Matches Python example structure and UX exactly

**Technical decisions:**
- Single Cargo package with two `[[bin]]` targets (simpler than workspace for this use case)
- `reqwest` with blocking mode (matches Python's synchronous style, cleaner than async for CLI tools)
- Dependencies: `reqwest` (0.12, features: json, blocking), `serde` (1.0, derive), `serde_json` (1.0)
- Proper error handling: all fallible operations use `Result` and `?`, no `unwrap()` in production paths
- SSE streaming: manual line-by-line parsing (reqwest blocking doesn't have built-in SSE, this approach is clean)
- Event deduplication: clone+compare previous event (same as Python's approach)
- Ctrl+C handling: natural interrupt via `std::thread::sleep` (idiomatic for Rust, no signal crate needed)

**File structure:**
```
rust/
├── Cargo.toml
├── assets/.gitkeep
└── src/bin/
    ├── clip_generator.rs
    └── check_status.rs
```

**Verification:**
- `cargo build` completed successfully
- Both binaries compiled: `target/debug/clip_generator` and `target/debug/check_status` (10MB each)
- Code follows Rust idioms: proper error propagation, borrowed strings where appropriate, no unsafe code
