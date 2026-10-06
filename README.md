# Video Downloader for X

A lightweight Chrome extension for downloading videos and optional images directly from X.com.

**No external downloader website. No conversion service. No account. No subscription. No ads. No analytics.**

The extension adds a download button directly to supported media on X. Click it, choose where to save the file using Chrome's normal **Save As** dialog, and you're done.

![Video Downloader for X](video-downloader-chrome-extension-for-x-com.png)

> **Current version:** 1.5.6  
> **Platform:** Chrome / Chromium, Manifest V3  
> **Minimum Chrome version:** 150

## Features

- Downloads the **highest available direct MP4** exposed by X.
- Uses resolution first and bitrate as a tie-breaker.
- Adds the download control directly to supported X video players.
- Can optionally add download buttons to X photos.
- Image downloading is **off by default**.
- Attempts to retrieve the original-size image rather than simply saving the resized preview shown on the page.
- Uses readable filenames based on post text when available.
- Keeps Chrome's normal **Save As** dialog enabled.
- Stores extension preferences locally.
- Includes a small temporary **Error Log** for troubleshooting.
- Uses no external downloader or conversion service.

## How It Works

For videos, the extension identifies the X post behind the player, checks the media information available from X, and selects the best direct MP4 variant it can find.

The quality currently playing in the browser is not used as the quality limit. If X exposes several direct MP4 variants, the extension selects the largest available resolution. When two variants have the same resolution, the higher bitrate wins.

For images, the extension looks for genuine X photo media and attempts to request the original-size asset from X's image infrastructure.

Downloads are handed to Chrome using the browser's normal downloads system.

## Settings

The popup contains two independent options:

- **Download videos** — enabled by default.
- **Download images** — disabled by default.

These preferences are stored locally in `chrome.storage.local`.

No account or cloud settings service is used.

## Privacy

Video Downloader for X is deliberately designed without analytics, telemetry, advertising, tracking, or an external downloader backend.

The extension communicates with X only when necessary to identify or retrieve media. Some video-resolution paths may use the page-visible X `ct0` CSRF value from the active browser session. The extension does **not** read your X password or `auth_token`.

Downloaded media comes directly from X's media infrastructure.

Nothing from the temporary Error Log is automatically sent to the developer.

## Error Log

If a download fails, the popup can show a small temporary Error Log for the current X tab.

The log is local and temporary. It is cleared when the relevant tab is reloaded or closed.

If you report a problem, you can manually copy the useful error details and include them with your report.

## Manual Installation

For development or testing:

1. Download and extract the extension ZIP.
2. Open `chrome://extensions`.
3. Enable **Developer mode**.
4. Click **Load unpacked**.
5. Select the folder containing `manifest.json`.
6. Open or refresh X.com.

For normal use, install the published Chrome Web Store release when available.

## Article, Documentation & Support

For the full article, usage information, screenshots, updates, and support:

**[Video Downloader for X | Free Chrome Extension for X.com](https://www.itsucks.fyi/video-downloader-for-x/)**

Developed as part of the **[IT SUCKS!](https://www.itsucks.fyi/)** project.

## Changelog

Development started under the name **Private X Video Downloader**, later became **Simple X Video Downloader**, and is now **Video Downloader for X**.

The project evolved from a tiny video-only downloader into a more polished extension with optional image downloads, local settings, diagnostics, stronger X compatibility, and a tighter privacy model.

See the full history in **[changelog.md](changelog.md)**.

## Responsible Use

Saving a file does not make it yours. Respect the creator's rights and get permission when needed before republishing or redistributing their work.

The extension is intended for lawful personal use. You are responsible for how downloaded content is used.

## Disclaimer

Video Downloader for X is an independent project and is not affiliated with, sponsored by, or endorsed by X Corp.
