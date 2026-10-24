# 🎬 GrabClip — yt-dlp Command Generator

[![Web Tool](https://img.shields.io/badge/Web%20Tool-Live%20Demo-8A2BE2?style=for-the-badge)](https://hamimtalukder.github.io/GrabClip/)
[![Made with](https://img.shields.io/badge/Made%20with-HTML%2FCSS%2FJS-orange?style=for-the-badge)]()

**GrabClip** is a lightweight, single-page web tool that instantly generates ready-to-use [`yt-dlp`](https://github.com/yt-dlp/yt-dlp) commands for downloading video and audio from **Facebook, YouTube, Instagram**, and other sources — no more memorizing or hand-typing complex terminal flags.

Pick a platform, paste a link, choose your quality/format and options, and GrabClip builds the exact command you need to paste into your terminal.

👉 **Try it live:** [hamimtalukder.github.io/GrabClip](https://hamimtalukder.github.io/GrabClip/)

---

## ✨ Features

- **Multi-platform** — Facebook, YouTube, Instagram, and a generic "Others" tab for any direct link, each with automatic link cleanup (strips tracking junk from FB/IG URLs).
- **Video + Audio, Video Only, or Audio Only** — download a full merged video, a video-only stream, or extract audio in your preferred format (MP3 at 3 quality tiers, AAC/M4A, Opus, FLAC, or best native audio).
- **7 quality presets** — 144p up to 4K (2160p).
- **Normal or Fast Download mode** — Fast mode uses `aria2c` with 8 parallel connections for higher download speed.
- **Extras** — optionally embed subtitles (English + Bangla) or embed thumbnail & metadata into the downloaded file.
- **One-click copy** — generated command is copied straight to your clipboard.
- **Private & local** — everything runs client-side in your browser; no links, cookies, or files are ever uploaded anywhere.

---

## 🚀 Quick Start

1. Open the [GrabClip web tool](https://hamimtalukder.github.io/GrabClip/).
2. Select a source tab (Facebook / YouTube / Instagram / Others) and paste your video link.
3. Choose content type (Video+Audio / Video Only / Audio Only), quality/format, download mode, and any extras.
4. Copy the generated command and run it in your terminal (setup required — see below).

---

## 🛠️ Environment Setup

GrabClip only *generates* the command — you need a few tools installed locally to actually run it. You'll need **Python**, **yt-dlp**, **FFmpeg** (to merge separately-downloaded video/audio streams), and **aria2c** (only if you plan to use Fast Download mode).

### Step 1 — Install Python
1. Download from [python.org](https://www.python.org/downloads/).
2. Run the installer.
3. ⚠️ **Important:** check **"Add Python to PATH"** before clicking **Install Now**.
4. Verify:
   ```bash
   python --version
   ```

### Step 2 — Install yt-dlp
```bash
pip install -U yt-dlp
```
Verify:
```bash
python -m yt_dlp --version
```
> 💡 If the bare `yt-dlp` command isn't recognized (common with the Microsoft Store version of Python on Windows), always run it as `python -m yt_dlp ...` instead — that's the form GrabClip's generated commands use.

### Step 3 — Install FFmpeg (required for merging audio + video)
yt-dlp often downloads video and audio as separate streams for higher quality; FFmpeg merges them into one `.mp4`/`.mkv` file.

**Option A — Windows Package Manager (easiest):**
```bash
winget install FFmpeg
```

**Option B — Manual install:**
1. Download a build from [gyan.dev/ffmpeg/builds](https://www.gyan.dev/ffmpeg/builds/) (`ffmpeg-release-full.7z`).
2. Extract it to `C:\ffmpeg`.
3. Add `C:\ffmpeg\bin` to your system **Environment Variables → PATH**.
4. Verify:
   ```bash
   ffmpeg -version
   ```

### Step 4 — Install aria2c (required only for Fast Download mode)
Enables multi-connection downloading for much higher speed.

**Option A — Winget (easiest):**
```bash
winget install aria2
```

**Option B — Manual install:**
1. Download from [aria2 GitHub Releases](https://github.com/aria2/aria2/releases).
2. Extract to a folder (e.g. `C:\aria2`).
3. Add that folder to your system **PATH**.
4. Verify:
   ```bash
   aria2c --version
   ```

---

## 🍪 Setting up `cookies.txt` (required for Facebook & private/restricted videos)

Facebook, Instagram, and age-restricted/private YouTube videos need an authenticated session to download. GrabClip's commands use a `cookies.txt` file for this instead of reading your browser's cookie database directly (which runs into decryption issues on modern Chrome).

1. **Install a cookie-export extension:**
   - Chrome / Edge / Brave: [Get cookies.txt LOCALLY](https://chromewebstore.google.com/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc)
   - Firefox: [Get cookies.txt LOCALLY](https://addons.mozilla.org/en-US/firefox/addon/get-cookies-txt-locally/)
2. **Export cookies:**
   - Log into Facebook (or YouTube) in your browser.
   - Click the extension icon → **Export** / **Export Cookies**.
3. **Name and place the file:**
   - Save it exactly as `cookies.txt`.
   - Place it in the **same folder** you'll run your commands from.

```
MyDownloads/
├── cookies.txt
└── (downloaded videos will appear here)
```

> ⚠️ On Windows, run the command from a plain, non-cloud-synced folder (not inside OneDrive/Desktop/Documents/Pictures) — Windows Defender's "Controlled folder access" can silently block writes there. Also run from a **non-Administrator** terminal so Chrome's cookie decryption works correctly.

---

## 📋 Example

Generate a command on [GrabClip](https://hamimtalukder.github.io/GrabClip/), then run it in your terminal from inside your working folder:

```bash
python -m yt_dlp --cookies cookies.txt -f "bv*[height<=1080]+ba/b[height<=1080]" --downloader aria2c --downloader-args "aria2c:-j 8 -x 8 -s 8" -o "%(title)s [%(id)s].%(ext)s" "https://www.youtube.com/watch?v=example"
```

---

## ⚠️ Disclaimer

GrabClip is a personal-use command generator built for downloading content you have the right to access (e.g. your own paid class recordings). It doesn't host, proxy, or store any video — it just formats a command around the open-source `yt-dlp` project. Respect the copyright and terms of service of the platforms you download from.

---

## 👤 Author

Built by **Hamim Talukder Soton**

- 🌐 Live app: <a href="https://hamimtalukder.github.io/GrabClip/" target="_blank">GrabClip</a>
- 📘 Facebook: <a href="https://www.facebook.com/hamim.talukder.soton" target="_blank">Hamim Talukder Soton</a>
- 💼 LinkedIn: <a href="https://www.linkedin.com/in/hamim-talukder" target="_blank">Hamim Talukder</a>

---

## 📄 License

This project is licensed under the [MIT License](LICENSE) — you're free to use, copy, modify, and distribute it, as long as the original copyright notice is kept.
