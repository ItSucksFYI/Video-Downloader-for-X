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

Technical development history for **Video Downloader for X**. The extension began as **Private X Video Downloader**, was later renamed **Simple X Video Downloader**, and is now **Video Downloader for X**.

This changelog intentionally focuses on meaningful technical changes, compatibility improvements, privacy-related changes, and feature development. Minor visual adjustments, icon revisions, spacing changes, wording tweaks, and other cosmetic work are omitted.

## 1.5.6 — September 29, 2026

Reliability and maintenance release.

- Prevented settings controls from being used before stored preferences finish loading.
- Added safer handling for overlapping preference writes.
- Restores the previous setting state if a save operation fails.
- Simplified duplicated video/image control code.
- Consolidated shared download-button construction and styling.
- Kept the existing video-resolution and image-download behavior unchanged.

### October 6, 2026 — Public naming update

- Renamed the extension from **Simple X Video Downloader** to **Video Downloader for X**.
- Kept version **1.5.6**.
- No permissions, download logic, settings, or feature behavior changed as part of the rename.

## 1.5.5 — August 21, 2026

Major compatibility and reliability hardening.

- Improved behavior during long X browsing sessions.
- Capped remembered GraphQL request URLs to avoid unnecessary growth.
- Improved rescanning when X dynamically changes `src`, `srcset`, inline styles, or media-player DOM structures.
- Prevented image download controls from attaching to video poster or cover elements.
- Improved detection of lightbox images and media without the expected wrapper structure.
- Strengthened original-image URL normalization.
- Added JPEG/PNG probing when WebP or AVIF previews do not map cleanly to an original asset.
- Added safer MIME-type and response-content validation for media probes.
- Improved Unicode-safe filename handling.
- Added support for additional retweet and `TweetDetail` metadata paths.
- Added timeouts and stronger fallback behavior for X metadata requests.
- Improved error reporting for rate limits, timeouts, interrupted downloads, and non-media responses.
- Added rescanning after bfcache restoration or tab suspension.
- Expanded page matching to X/Twitter subdomains.
- Reduced Chrome Web Store host permissions to the required X and `twimg.com` endpoints.

## 1.5.4 — August 21, 2026

Reworked optional image downloading while preserving the stable video engine.

- Kept the proven **1.3.7 video resolver** as the video-download base.
- Reintroduced the optional **Download images** feature.
- Changed image detection to use visible X photo media as the primary source of truth.
- Rejected video covers, profile images, card artwork, and other non-photo imagery.
- Added image discovery through standard image sources, `srcset`, CSS backgrounds, and lightbox media.
- Rewrote X preview URLs toward original-size assets where possible.
- Added format probing for difficult WebP and AVIF preview cases.
- Improved filename handling for emoji and other multi-codepoint characters.
- Improved fallback behavior so successful recovery paths do not create misleading Error Log entries.

## 1.5.3 — August 21, 2026

Temporary stability-focused revision.

- Returned video downloading to the stable **1.3.7 video engine** while the image-download implementation was being redesigned.
- Removed the experimental image-download path from this build.
- Preserved the existing video-download and local diagnostic behavior.

## 1.5.2 — August 20, 2026

Image and filename reliability update.

- Expanded discovery of X photo URLs from rendered page media.
- Improved handling when X rearranges photo markup dynamically.
- Strengthened original-image URL handling.
- Added safer fallback filenames for both videos and images.
- Improved handling of invalid filenames reported by Chrome.

## 1.4.0–1.4.3 — August 19–20, 2026

Image downloading and local settings were added.

### 1.4.0

- Added optional image downloading.
- Added independent **Download videos** and **Download images** settings.
- Added local preference storage using `chrome.storage.local`.
- Kept image downloading disabled by default.
- Added original-size image handling and image-specific filenames.

### 1.4.1

- Refactored shared video/image button creation.
- Improved fallback photo discovery.
- Added stricter validation for X post IDs used by the syndication fallback.
- Added the extension version to diagnostic output.

### 1.4.2–1.4.3

- Clarified and cleaned up the implementation around X session metadata.
- Documented the use of the page-visible `ct0` CSRF value.
- No significant downloader behavior change.

## 1.3.7 — August 18, 2026

Video resolver compatibility update.

- Improved MP4 recognition using both URL structure and MIME information.
- Improved HLS rejection using both `.m3u8` URLs and HLS MIME types.
- Preserved content-type information from VMAP media entries.
- This version later became the stable video engine reused by the 1.5.x line.

## 1.3.0–1.3.3 — August 17–18, 2026

Reduced dependence on X internals and added local diagnostics.

### 1.3.0

- Replaced active JavaScript bundle parsing with a passive **Resource Timing** fallback.
- Reused X's own observed `TweetResultByRestId` request structure where available.
- Reduced reliance on hardcoded GraphQL operation details.

### 1.3.1

- Added a temporary per-tab **Error Log**.
- Stores a small number of recent failures in content-script memory.
- Records errors only when the complete resolution attempt fails, avoiding noise from successful fallback paths.
- Added popup access to the diagnostic log.

### 1.3.2–1.3.3

- Refined diagnostic behavior and reporting.
- Clarified that diagnostic information is copied manually and is never transmitted automatically.

## 1.2.0–1.2.8 — August 17, 2026

Added the popup and established the first public release identity.

### 1.2.0

- Added the toolbar popup.
- Added privacy information and a link to the project article.
- Kept the popup local, with no analytics, tracking, or external settings service.

### 1.2.6

- Renamed the extension from **Private X Video Downloader** to **Simple X Video Downloader**.

### 1.2.8

- Improved reliability of the injected media control over X's interface.

## 1.1.0–1.1.3 — August 17, 2026

Major hardening of the original video-only downloader.

### 1.1.0

- Added readable filenames based on post text and video resolution.
- Improved reinsertion when X rebuilds video-player DOM nodes.
- Improved GraphQL operation discovery.
- Added quoted-post support to the syndication fallback.
- Made VMAP parsing namespace-safe.
- Set the minimum supported Chrome version to 150.
- Preserved Chrome's normal **Save As** workflow.

### 1.1.1

- Replaced the externally loaded button asset with inline SVG construction.
- Removed the need to expose that asset as a web-accessible resource.
- Improved resilience across extension reloads and updates.

## 1.0.0 — August 17, 2026

Initial release as **Private X Video Downloader**.

- First working Manifest V3 build.
- Added a download control directly to X video players.
- Selected the highest-resolution direct MP4 available from X.
- Used bitrate as a tie-breaker when multiple variants had the same resolution.
- Did not limit downloads to the quality currently being played in the browser.
- Added multiple media-resolution paths, including GraphQL, guest-token, VMAP, and syndication fallbacks.
- Restricted background downloads to X media.
- Used Chrome's normal download system and **Save As** dialog.
- Included no analytics, telemetry, account system, external downloader service, or cloud backend.


## Responsible Use

Saving a file does not make it yours. Respect the creator's rights and get permission when needed before republishing or redistributing their work.

The extension is intended for lawful personal use. You are responsible for how downloaded content is used.

## Disclaimer

Video Downloader for X is an independent project and is not affiliated with, sponsored by, or endorsed by X Corp.
