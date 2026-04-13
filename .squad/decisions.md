# Squad Decisions

## Active Decisions

### Rust Implementation Approach (2026-04-13)

**Author:** Keaton (Lead / Rust Dev)  
**Status:** Implemented

#### 1. Blocking vs Async HTTP

**Decision:** Use `reqwest` with blocking mode rather than async with `tokio`.

**Rationale:**
- CLI tools with linear user interaction don't benefit from async
- Blocking code is simpler and matches the Python reference implementation's synchronous style
- No concurrency needed for single-request-at-a-time workflows
- Smaller binary size and faster compilation

#### 2. Single Package vs Workspace

**Decision:** Single Cargo package with two `[[bin]]` targets.

**Rationale:**
- No shared library code between the two binaries
- Simpler project structure (no nested `Cargo.toml` files)
- Both binaries use identical dependencies
- Easier for users to understand and modify

#### 3. SSE Parsing Approach

**Decision:** Manual line-by-line parsing of SSE events.

**Rationale:**
- `reqwest` blocking mode doesn't have built-in SSE support
- Adding an SSE library would require async or additional complexity
- The SSE format is simple: `data: {json}` lines
- Manual parsing is straightforward Rust code

#### 4. Error Handling Strategy

**Decision:** Propagate errors with `?` and display user-friendly messages at the top level.

**Rationale:**
- No `unwrap()` or `expect()` in production paths (Rust best practice)
- Connection errors return `Result<_, String>` with descriptive messages
- Main function prints errors to stderr and exits with code 1
- Matches error handling UX of Python examples

#### 5. Ctrl+C Handling

**Decision:** Natural interrupt via `std::thread::sleep`, no signal handling.

**Rationale:**
- On Unix/macOS, Ctrl+C naturally interrupts blocking syscalls
- No need for `ctrlc` crate or signal handlers
- Simpler code, fewer dependencies

**Dependencies Locked:**
- `reqwest = { version = "0.12", features = ["blocking", "json"] }`
- `serde = { version = "1.0", features = ["derive"] }`
- `serde_json = "1.0"`

---

## Governance

- All meaningful changes require team consensus
- Document architectural decisions here
- Keep history focused on work, decisions focused on direction
