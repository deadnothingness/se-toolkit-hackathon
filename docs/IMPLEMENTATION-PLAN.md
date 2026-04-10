# MediaFetch — Implementation Plan

## Product Vision

A universal web service that lets users download audio (MP3) and video (MP4) from **thousands of platforms** (YouTube, TikTok, VK, Rutube, Twitch, and more) with an **AI chat assistant** that understands natural language requests. Powered by `yt-dlp`.

## Version 1 — Core Feature

**One core thing done well:** Download media from a direct URL in the user's chosen format and quality, with an AI chat assistant that parses natural language requests.

**Status:** ✅ Implemented

**Key features:**

- Download MP3/MP4 by URL
- Task tracking with status updates
- AI chat assistant with regex fallback
- Error handling
- Docker deployment

## Version 2 — Improvements

**Status:** ✅ Implemented

**Added features:**

- ✅ Real‑time download progress (Server-Sent Events)
- ✅ Resolution‑specific quality (360p, 720p, 1080p, best)
- ✅ Audio bitrate selection (128k, 192k, 320k)
- ✅ Smart file naming (uses video title instead of task ID)
- ✅ Unified LLM configuration
- ✅ Persistent downloads volume (Docker volume mount)

## What Works

| Feature | Status |
|---------|--------|
| Download MP4 from any supported platform | ✅ |
| Download MP3 from any supported platform | ✅ |
| Quality selection (video) | ✅ (360p, 720p, 1080p, best) |
| Quality selection (audio) | ✅ (128k, 192k, 320k) |
| Download progress bar | ✅ (SSE) |
| Task list with auto-refresh | ✅ |
| AI chat assistant | ✅ (Qwen API + regex fallback) |
| Smart file naming | ✅ |
| Docker deployment | ✅ |
| Persistent storage | ✅ |

## Supported Platforms

`yt-dlp`, the download engine, supports thousands of platforms out of the box, including:

| Category | Platforms |
|----------|-----------|
| **Video Hosting** | YouTube, Vimeo, Dailymotion, Twitch, Rutube |
| **Social Media** | VK, TikTok, Facebook, Instagram, X (Twitter), Reddit |
| **Streaming** | Twitch clips, YouTube Live, VK Live |
| **File Sharing** | Dropbox, Google Drive, Яндекс.Диск |

> **Note:** VK, Rutube, and Twitch work directly from the university network. YouTube, TikTok, and Instagram require a VPN or proxy due to network restrictions. The code supports all platforms – only network limitations apply.

## Technical Decisions

| Decision | Rationale |
|----------|-----------|
| **FastAPI** | Async support for background downloads, automatic OpenAPI docs |
| **yt-dlp** | Supports thousands of platforms, active development |
| **PostgreSQL** | Reliable, supports concurrent connections, easy Docker setup |
| **SSE for progress** | Simpler than WebSockets, perfect for one-way progress updates |
| **Vanilla JS frontend** | No build step, easy to deploy, works everywhere |
| **Docker Compose** | Single-command deployment, consistent across environments |

## Known Limitations

- YouTube/TikTok/Instagram require VPN on university VM (network restriction, not code limitation)
- No search functionality (planned for future)
- No user authentication
- No automatic file cleanup
- No batch downloads

## Future Roadmap

| Feature | Priority |
|---------|----------|
| Direct AI download execution (no manual click) | High |
| Batch playlist downloads | High |
| User accounts and download history | Medium |
| File cleanup automation | Medium |
| Search by title | Medium |
| Telegram bot integration | Low |

## Deployment

See [README.md](../README.md) for step-by-step deployment instructions.

## License

MIT
