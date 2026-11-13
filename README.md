# Absorb Dev: Community Build, Fixes & Branches

[![Latest Release](https://img.shields.io/github/v/release/TerribleTurtle/absorb?include_prereleases&style=for-the-badge&logo=github&label=Download%20APK)](https://github.com/TerribleTurtle/absorb/releases) [![Get it on Obtainium](https://img.shields.io/badge/Obtainium-Absorb_Dev-teal?style=for-the-badge)](https://apps.obtainium.imranr.dev/redirect?r=obtainium://add/https://github.com/TerribleTurtle/absorb) [![Upstream Repo](https://img.shields.io/badge/Upstream-pounat%2Fabsorb-blue?style=for-the-badge&logo=github)](https://github.com/pounat/absorb)

**Absorb Dev** (`com.barnabas.absorb.dev`) is a signed Android companion build of [**Absorb**](https://github.com/pounat/absorb) that merges all `12` pending fixes and enhancements below into a daily-driver APK ([**Releases**](https://github.com/TerribleTurtle/absorb/releases) / [Obtainium](https://apps.obtainium.imranr.dev/redirect?r=obtainium://add/https://github.com/TerribleTurtle/absorb)). It uses a separate package name so it installs alongside the official app without touching your existing setup, and each branch is retired once it lands upstream.

### What You Get in Absorb Dev (At a Glance)

| Feature / Fix | What's Improved in `Absorb Dev` |
|---|---|
| **Android Auto & CarPlay Queue** | Full Absorbing queue on Continue + chapterless Now Playing Queue drawer ([#318](https://github.com/pounat/absorb/issues/318)) |
| **Android Auto Series Order** | Sorts book series by book number instead of alphabetically ([#360](https://github.com/pounat/absorb/issues/360)) |
| **Series Playback Speed** | Speed changes on one book carry over to the rest of the series ([#441](https://github.com/pounat/absorb/issues/441)) |
| **Startup Sync & Paused Rewinds** | Catches up on launch and stops paused chapter rewinds from jumping back ([#344](https://github.com/pounat/absorb/issues/344)) |
| **Chromecast & Nest Speakers** | Plays `.m4b` books on Nest speakers, pre-loads saved chapters, fixes laggy controls & sleep timers ([#404](https://github.com/pounat/absorb/issues/404), [#473](https://github.com/pounat/absorb/issues/473), [#260](https://github.com/pounat/absorb/issues/260)) |
| **Offline Podcast Shows** | Groups downloaded episodes under their show and fills the offline Episodes tab ([#396](https://github.com/pounat/absorb/issues/396)) |
| **Long-Book Chapters Sheet** | Opens right on your playing chapter even in books with 200+ chapters ([#336](https://github.com/pounat/absorb/issues/336), [#262](https://github.com/pounat/absorb/issues/262)) |
| **Keep Screen Awake (All Readers)** | Keeps the screen on in PDF, comic, and MOBI/AZW3 readers, not just EPUB ([#384](https://github.com/pounat/absorb/issues/384)) |
| **Background Battery Saver** | Stops idle background sensors and timers while playback is paused ([PR #439](https://github.com/pounat/absorb/pull/439)) |
| **Live Sync After Token Refresh** | Refreshes expired login tokens before reconnecting live server sync ([#422](https://github.com/pounat/absorb/issues/422)) |
| **CrowdSec & SSO-Only Login** | Stops expired-session retry storms that trip CrowdSec and hides password boxes on SSO-only servers ([#444](https://github.com/pounat/absorb/issues/444), [#456](https://github.com/pounat/absorb/issues/456)) |
| **Tag & Genre Pill Navigation** | Tapping a tag or genre chip on a book page jumps straight to matching books |

### Quick Install & Settings Import ([Releases](https://github.com/TerribleTurtle/absorb/releases))

1. **Export from the main app:** Open **Settings -> Backup & Restore -> Back up** and pick **Yes, include accounts**.
2. **Install & import:** Install `Absorb Dev` from [**Releases**](https://github.com/TerribleTurtle/absorb/releases) or [Obtainium](https://apps.obtainium.imranr.dev/redirect?r=obtainium://add/https://github.com/TerribleTurtle/absorb), then tap **Import** on the sign-in screen.
3. **Sign out of the unused app:** Log out or Force Stop the app you aren't actively using so it doesn't wake up in the background and sync an older cached position.
4. **Issues & feedback:** Check whether a bug also happens on the [official release](https://github.com/pounat/absorb/releases) before filing upstream, or open an issue / discussion [here on the fork](https://github.com/TerribleTurtle/absorb/issues).

### How This Repo Is Organized

- **`main` mirrors [`pounat/absorb:main`](https://github.com/pounat/absorb) 1:1.** Small `<100`-line bug fixes live on `fix/*` branches and enhancements live on `feat/*` branches.
- **Small PR queue (at most 3 open PRs at a time).** To keep reviews manageable, I keep at most 3 pull requests open at a time and hold finished branches below until a slot opens - while merging all of them into `Absorb Dev` so listeners can use them today.

### Standalone Branches & Cherry-Picking

Every pushed `fix/*` and `feat/*` branch starts cleanly from `upstream/main` (`v1.12.1+305`) with zero cross-branch dependencies. Feel free to inspect any diff below, cherry-pick an individual branch whenever it is useful, or reach out on GitHub or Discord if you ever want to chat about a change or have anything adjusted:

```sh
git fetch https://github.com/TerribleTurtle/absorb.git <branch-name>
git cherry-pick main..FETCH_HEAD
```

---

## Included in Absorb Dev (`12` Active in `Absorb Dev`, `2` Merged Upstream)

### 1. Open Upstream Pull Requests (`2`)

| Issue | Branch & Diff | Upstream PR | Summary |
|---|---|---|---|
| Battery / Lifecycle | [`fix/background-pause-lifecycle`](https://github.com/TerribleTurtle/absorb/tree/fix/background-pause-lifecycle) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/background-pause-lifecycle), `+80/-7`) | [**PR #439**](https://github.com/pounat/absorb/pull/439) | **Background battery drain while paused:** Stops four background tasks that kept running after playback paused with the screen off: the shake-to-snooze motion sensor, periodic home-widget refreshes, local-network server pings after a book finishes, and idle Chromecast speaker scanning. |
| [#336](https://github.com/pounat/absorb/issues/336), [#262](https://github.com/pounat/absorb/issues/262) | [`fix/chapters-sheet-scroll-336`](https://github.com/TerribleTurtle/absorb/tree/fix/chapters-sheet-scroll-336) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/chapters-sheet-scroll-336), `+31/-22`) | [**PR #442**](https://github.com/pounat/absorb/pull/442) | **Chapters list opening far away from the current chapter in long books:** In books with hundreds of chapters or multi-line chapter titles, opening the Chapters sheet landed way above the playing chapter. Now measures the real height of each row so the list opens right on your current chapter. |

---

### 2. Staged Bug Fixes - `fix/*` (`8`)

Small, self-contained bug fixes (`<100` lines added) rebased on `upstream/main`, included in `Absorb Dev` now, and ready to cherry-pick or open as upstream PRs as review slots free up:

| Issue | Branch & Diff | Status | Summary |
|---|---|---|---|
| [#344](https://github.com/pounat/absorb/issues/344) | [`fix/startup-progress-sync-344`](https://github.com/TerribleTurtle/absorb/tree/fix/startup-progress-sync-344) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/startup-progress-sync-344), `+49/-3`) | Staged | **Multi-device progress sync and paused chapter rewinds snapping back:** Fixes progress not catching up on app launch after listening on another device, and stops rewinding to an earlier chapter while paused from jumping back to the old spot when playback resumes. |
| [#384](https://github.com/pounat/absorb/issues/384) | [`fix/ebook-keep-screen-on-384`](https://github.com/TerribleTurtle/absorb/tree/fix/ebook-keep-screen-on-384) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/ebook-keep-screen-on-384), `+18/-1`) | Staged | **Screen timing out while reading PDFs, comics, or MOBI/AZW3 books:** The "Keep screen awake while reading" setting only worked in the standard EPUB reader. Now keeps the screen awake across the PDF, comic, and Foliate readers too. |
| Discord `#beta-bug-reports` | [`fix/tag-genre-pill-navigation`](https://github.com/TerribleTurtle/absorb/tree/fix/tag-genre-pill-navigation) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/tag-genre-pill-navigation), `+11/-4`) | Staged | **Tapping a tag or genre pill on a book page not showing matching books:** Tapping a tag or genre chip from search results or inside a series/author sheet left the old search text or sheet open instead of switching to the filtered Books tab. |
| [#360](https://github.com/pounat/absorb/issues/360) | [`fix/aa-series-sort-360`](https://github.com/TerribleTurtle/absorb/tree/fix/aa-series-sort-360) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/aa-series-sort-360), `+4/-4`) | Staged | **Android Auto sorting series alphabetically instead of by book number:** Series with prefixes like "Book 1" or "Vol. 2" (or more than 50 books) sorted by title in Android Auto. Now parses the book number properly and loads the full series in reading order. |
| [#422](https://github.com/pounat/absorb/issues/422) | [`fix/auth-token-expiry-422`](https://github.com/TerribleTurtle/absorb/tree/fix/auth-token-expiry-422) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/auth-token-expiry-422), `+35/-10`) | Staged | **Live server sync dropping after the login token refreshes:** When the app woke up after its short-lived access token expired, the live connection reconnected with the old token and permanently dropped real-time sync until an app restart. Now refreshes the token before reconnecting. |
| [#396](https://github.com/pounat/absorb/issues/396) | [`fix/offline-podcast-shows-396`](https://github.com/TerribleTurtle/absorb/tree/fix/offline-podcast-shows-396) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/offline-podcast-shows-396), `+94/-31`) | Staged | **Downloaded podcasts showing as empty in Offline mode:** In Offline mode, downloaded podcast episodes showed up as empty shows on the Shows tab, left the Episodes tab blank, and cluttered the Absorbing screen with unstarted downloads. Now groups downloaded episodes under their show, populates the offline Episodes tab, and keeps unstarted episodes off the Absorbing deck. |
| [#444](https://github.com/pounat/absorb/issues/444), [#456](https://github.com/pounat/absorb/issues/456) | [`fix/auth-refresh-storm-444`](https://github.com/TerribleTurtle/absorb/tree/fix/auth-refresh-storm-444) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/auth-refresh-storm-444), `+55/-9`) | Staged | **Expired login retries triggering firewall bans (CrowdSec) and SSO-only login screens:** Stops the app from firing repeated failed token-refresh requests when a session is revoked (which could trip server rate-limiters/CrowdSec), and hides the username/password boxes on servers configured for Single Sign-On (OIDC) only. |
| [#404](https://github.com/pounat/absorb/issues/404), [#473](https://github.com/pounat/absorb/issues/473), [#260](https://github.com/pounat/absorb/issues/260) | [`fix/cast-buffering-sleep-timer-404`](https://github.com/TerribleTurtle/absorb/tree/fix/cast-buffering-sleep-timer-404) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/cast-buffering-sleep-timer-404), `+95/-33`) | Staged | **Chromecast button stuck on Play, laggy Play/Pause/Stop/Disconnect controls, sleep timer freezing, and .m4b books failing on Google Home / Nest Mini:** Audio-only Cast speakers often report a buffering state while audio is playing, which left the card button on Play and froze or reset the sleep timer. Tapping Play, Pause, Stop Casting, or Disconnect also lagged or needed a second tap while waiting on server syncs and native session teardown, starting a Cast session flashed Chapter 1 before loading your saved spot, direct-play URLs sent .m4b audiobooks as MP3s, and Google Play Services route refreshes dropped first-tap connects. Now updates Cast controls and disconnects immediately, tracks live playback progress, pre-loads your saved chapter, sends the right MP4 audio format, and automatically completes first-tap connections. |

---

### 3. Community-Requested Enhancements - `feat/*` (`1`)

Quality-of-life enhancements requested on the official issue tracker, included in `Absorb Dev` and kept on isolated `feat/*` branches off `upstream/main` so bug fixes in Section 2 stay self-contained:

| Issue | Branch & Diff | Status | Summary |
|---|---|---|---|
| [#441](https://github.com/pounat/absorb/issues/441) | [`feat/series-playback-speed-441`](https://github.com/TerribleTurtle/absorb/tree/feat/series-playback-speed-441) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:feat/series-playback-speed-441), `+85/-5`) | Staged | **Playback speed per book series:** Books in the same series now share a playback speed, so changing the speed on any installment automatically carries over when advancing, skipping ahead, or re-reading earlier books in the series. |

---

### 4. In Progress / Active Testing (`1`)

Work currently included in the `Absorb Dev` APK for daily-driver testing before publishing a standalone branch:

| Issue | Branch & Scope | Status | Summary |
|---|---|---|---|
| [#318](https://github.com/pounat/absorb/issues/318) | `feat/android-auto-absorbing-queue-318` (`+251/-51`, in testing) | In Progress / Testing | Shows the full in-app Absorbing queue (including unstarted books and multiple queued episodes from the same podcast) in exact queue order on the Android Auto and CarPlay Continue shelf both online and offline, updates the car list immediately when adding, reordering, or removing items, and populates the Android Auto Now Playing queue drawer with the active queue highlight when playing chapterless podcast episodes. |

---

### 5. Previously Merged Upstream (`2`)

| Issue | Branch | Upstream PR | Summary |
|---|---|---|---|
| [#409](https://github.com/pounat/absorb/issues/409) | `fix/cancel-settings-timer-on-background` ([`3038c453`](https://github.com/pounat/absorb/commit/3038c453)) | [**PR #410**](https://github.com/pounat/absorb/pull/410) *(Merged in `v1.12.0`)* | **Background settings sync timer:** Stops the 45-second settings check timer from running while the app is in the background. |
| [#430](https://github.com/pounat/absorb/issues/430) | `fix/cold-start-resume-430` ([`ef88e17a`](https://github.com/pounat/absorb/commit/ef88e17a)) | [**PR #438**](https://github.com/pounat/absorb/pull/438) *(Merged)* | **Resuming from a widget, headphones, or Android Auto losing progress from another device:** Starting a downloaded book outside the main app screen skipped checking the server for newer progress, so it resumed from the phone's older spot and overwrote the server. Now checks the server first (up to 2s) once the phone's last save is more than 5 minutes old; quicker re-presses still start instantly. |
