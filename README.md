# MediaFetch

> Download audio (MP3) and video (MP4) from **thousands of platforms** – YouTube, TikTok, VK, Rutube, Twitch, Vimeo, Facebook, X (Twitter), Reddit, and more – with real-time progress tracking and AI chat assistant.

## Demo

[Video Demonstration](https://docs.google.com/videos/d/1w1D_I9Xwp-NM1e8cayu9JTEflUBtp4-XMHWcqrxxl7Y/edit?scene=id.p#scene=id.p)

## Product Context

### End Users

Students, educators, content creators, researchers, and anyone who needs to save online media (lectures, tutorials, music, streams) for offline access without ads or third-party download sites.

### Problem

Downloading media from different platforms requires navigating ad-heavy websites, using unreliable browser extensions, or switching between multiple tools. Users need a single, clean interface that works across various sources.

### Solution

A web-based service powered by `yt-dlp` – a powerful download engine that supports thousands of websites out of the box. Users can paste any video URL, choose format (MP3/MP4) and quality (360p-1080p / 128k-320k), and download the file with real-time progress tracking. An AI chat assistant can parse natural language requests to auto-fill the form.

## Supported Platforms (Partial List)

| Category | Platforms |
|----------|-----------|
| **Video Hosting** | YouTube, Vimeo, Dailymotion, Twitch, Rutube |
| **Social Media** | VK, TikTok, Facebook, Instagram, X (Twitter), Reddit |
| **Streaming** | Twitch clips, YouTube Live, VK Live |
| **File Sharing** | Dropbox, Google Drive, Яндекс.Диск |
| **… and thousands more** | Any site supported by yt-dlp |

> **Note:** VK, Rutube, and Twitch work directly from the university network. YouTube, TikTok, and Instagram require a VPN or proxy on the VM due to network restrictions. The code supports all platforms – only network limitations apply.

## Features

### Implemented (v2)

- ✅ Download MP3/MP4 from any supported platform
- ✅ Resolution-specific quality (360p, 720p, 1080p, best)
- ✅ Audio bitrate selection (128k, 192k, 320k)
- ✅ Real-time download progress bar (SSE)
- ✅ Smart file naming (uses video title, not task ID)
- ✅ Task list with status tracking
- ✅ AI chat assistant (Qwen API + regex fallback)
- ✅ Docker deployment with persistent storage

### Not Yet Implemented

- ⬜ Batch downloads (multiple URLs at once)
- ⬜ User authentication
- ⬜ Download history per user
- ⬜ File cleanup (automatic deletion of old files)
- ⬜ Direct download execution from AI assistant (no manual click)

## Usage

1. Open `http://localhost:8000` in your browser
2. Paste a video URL from any supported platform (e.g., `https://vkvideo.ru/video-xxxxx_xxxxx`, `https://youtube.com/watch?v=...`)
3. Select format: **MP4 (Video)** or **MP3 (Audio)**
4. Select quality:
   - For video: 360p, 720p, 1080p, Best
   - For audio: 128k, 192k, 320k
5. Click **Start Download**
6. Watch progress bar fill, then click **Download File** when complete

### AI Chat Assistant

Type natural language requests in the chat widget, e.g.:

- `"download this video as MP4: https://vkvideo.ru/video-..."`
- `"save audio from this link in high quality"`

The assistant will auto-fill the form – just click Start Download.

**Future vision:** The assistant will soon start downloads directly, handle batch requests like "download this whole playlist", and suggest content based on your history.

## Deployment

### Requirements

- **OS:** Ubuntu 24.04 (or any Linux with Docker support)
- **CPU:** 2+ cores
- **RAM:** 4+ GB
- **Disk:** 10+ GB free space
- **Network:** Access to target platforms (VPN may be required for some)

### Prerequisites on VM

```bash
# Install Docker and Docker Compose
sudo apt update
sudo apt install -y docker.io docker-compose
sudo usermod -aG docker $USER
# Log out and back in

# Install ffmpeg (required for audio conversion)
sudo apt install -y ffmpeg
