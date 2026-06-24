# Changelog

## 2026 compatibility repair

- Added a modern compatibility layer that runs alongside the original YouTube Center Developer Build code instead of replacing it.
- Added MutationObserver-based DOM detection so controls can be re-injected after YouTube updates the page dynamically.
- Added YouTube SPA navigation support using `yt-navigate-finish`, `yt-page-data-updated`, `popstate`, and wrapped `history.pushState` / `history.replaceState` hooks.
- Added guarded startup and feature execution helpers so feature failures are logged as warnings and do not crash the whole userscript.
- Added `[YouTubeCenter]`-prefixed console logging and a startup compatibility report.
- Added a feature registry that records successful feature runs and failures.
- Added a temporary floating debug panel showing script loaded status, current video ID, button injection count, and recent errors.
- Added modern custom controls for repeat, theater mode, lights-off mode, player resizing, aspect ratio cycling, download handoff, stream diagnostics, and settings.
- Added a small settings panel backed by localStorage for compatibility-layer settings.
- Added modern selectors for YouTube Polymer/SPA pages, including `ytd-watch-flexy`, `ytd-player`, `#movie_player`, `#top-level-buttons-computed`, `#actions-inner`, and `#below`.
- Added duplicate-injection protection by reusing fixed element IDs for the compatibility controls, settings panel, lights overlay, style block, and debug panel.
- Added modern userscript metadata for current YouTube hosts, `GM.*` APIs, and cross-origin request permissions.
- Added Promise-based fallbacks for modern `GM.getValue`, `GM.setValue`, and `GM.xmlHttpRequest` while preserving the original legacy paths.
- Added a secondary modern cookie write with unencoded domain handling and `SameSite=Lax` / HTTPS `Secure` attributes while preserving the original cookie write.

## Feature status

### Successfully modernized

- Settings panel: a modern fallback settings panel is available from the injected controls.
- Custom buttons: modern controls are injected on current YouTube watch pages and re-injected after SPA navigation.
- Repeat button: toggles the HTML5 video element's `loop` property.
- Theater controls: applies modern `ytd-watch-flexy` theater state and compatibility styling.
- Lights-off mode: adds a modern overlay while keeping the player above the dimmed page.
- Player resize controls: cycles modern width presets via CSS variables.
- Aspect ratio controls: cycles modern aspect-ratio presets via CSS variables.
- Stream detection: logs currently available HTML5 media stream details and playback quality diagnostics.

### Partially functional

- Download button: opens the current YouTube URL as a safe handoff point for external downloader integrations; direct stream downloads are restricted by YouTube's signed URLs, CORS, and DRM/protected formats.
- Audio extraction integrations: no direct extraction is performed in-browser; integrations must use external tools or services.
- Legacy comments and Google+ integrations: original code remains, but modern YouTube removed or changed these APIs.

### No longer possible or restricted

- Direct, reliable extraction of all video/audio streams from the browser page is restricted by signed URLs, CORS, adaptive streaming, and protected media paths.
- Google+ comment integrations are obsolete because Google+ and the old YouTube comment widgets are no longer available.
- Legacy YouTube Data API flows that depend on removed endpoints or unavailable API keys may not function without replacement services.
