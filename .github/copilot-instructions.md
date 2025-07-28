# Copilot Instructions for Mica Music Android

## Project Overview
- **Purpose:** Android app to play local playlists via Spotify, supporting Spanish/English song selection with a three-column UI.
- **Core Data:** Artist/song data is loaded from `app/src/main/assets/artists.json` (see README for format).
- **Spotify Integration:** Uses Spotify Web API and App Remote SDK (`app/libs/spotify-app-remote-release-0.8.0.aar`).

## Architecture & Key Files
- **UI:** Modern Material Design, three columns (artist, Spanish, English). Unavailable songs are grayed out/disabled.
- **Service Layer:** Spotify authentication and playback logic in `app/src/main/java/com/micamusic/app/service/SpotifyService.kt`.
- **Assets:** Artist/song data in JSON, images loaded from URLs.
- **Build System:** Gradle (see `build.gradle`, `app/build.gradle`).
- **CI/CD:** GitHub Actions builds APKs/releases, uses secrets for Spotify and signing keys.

## Developer Workflows
- **Build:**
  - Android Studio: Open, sync Gradle, run.
  - CLI: `./gradlew build`, `./gradlew installDebug`, APKs in `app/build/outputs/apk/`
- **Test:** `./gradlew test`
- **Release:** `./gradlew assembleRelease`
- **Troubleshooting:** See `BUILD_TROUBLESHOOTING.md` for network, SDK, and CI issues.
- **Spotify Setup:** Place AAR in `app/libs/`, set credentials in `local.properties` and `SpotifyService.kt`.

## Conventions & Patterns
- **Language Toggle:** UI logic disables/grays out unavailable songs per language.
- **Environment Config:** Secrets/keys in `local.properties` (local) and GitHub Actions (CI).
- **Minimum SDK:** API 24; check `AndroidManifest.xml` for permissions.
- **Debugging:** Use `adb logcat` for crash logs; enable verbose logging via `local.properties`.

## Integration Points
- **Spotify:** Requires installed Spotify app and valid credentials.
- **Network:** Build requires access to `dl.google.com`, `repo1.maven.org`, `services.gradle.org`.
- **CI/CD:** Automated builds/releases on tag push; secrets required for signing and Spotify.

## Examples
- **Artist JSON:** See `app/src/main/assets/artists.json` for structure.
- **SpotifyService:** Update `CLIENT_ID` in `SpotifyService.kt` for your app.
- **AAR SDK:** Download and place in `app/libs/` as described in `app/libs/README.md`.

## References
- [README.md](../README.md) — setup, architecture, troubleshooting
- [BUILD_TROUBLESHOOTING.md](../BUILD_TROUBLESHOOTING.md) — build/network issues
- [app/libs/README.md](../app/libs/README.md) — Spotify SDK setup

---
**Feedback:** If any section is unclear or missing, please specify so it can be improved for future agents.
