# Rust Clip Tools

Simple Rust binaries to create video clips using the Reka AI API.

## Setup

1. Install Rust: Visit [rustup.rs](https://rustup.rs) and follow the installation instructions
2. Build the project: `cargo build`
3. Set your API key: `export REKA_API_KEY=your_key_here`

## Scripts

### clip_generator

Creates a clip from a YouTube video.

```bash
cargo run --bin clip_generator
```

Enter the video URL when prompted. The script streams progress and shows the Job ID (save it if interrupted).

**Sample Output:**

![clip generator output](assets/clip_generator.png)

### check_status

Check the status of a clip job using its Job ID.

```bash
cargo run --bin check_status
```

Enter the Job ID when prompted. Checks every 30 seconds until complete. Press `Ctrl+C` to stop.

![Check status output](assets/check_status.png)

## Links

- [Reka API Docs](https://docs.reka.ai/vision/highlight-reel-generation)
- [Reka Discord](https://link.reka.ai/discord)
