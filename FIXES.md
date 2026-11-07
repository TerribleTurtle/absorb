# Absorb Dev: Upstream Staging, Fixes & Side-by-Side Test Builds

Upstream-tracking staging repository and side-by-side Android test build (**Absorb Dev**, `com.barnabas.absorb.dev`) for Nathan Poulson's ([`@pounat`](https://github.com/pounat)) [**Absorb**](https://github.com/pounat/absorb).

I use this fork to reproduce issues reported on the [official issue tracker](https://github.com/pounat/absorb/issues) and Discord, road-test fixes and community-requested enhancements on my phones, and stage clean, single-purpose branches for upstream pull requests. Once a fix lands in the official app (or is solved upstream), its branch here is retired.

### How This Repo Is Organized

- **`main` mirrors [`pounat/absorb:main`](https://github.com/pounat/absorb) 1:1.** I never commit directly to `main` on GitHub so the default branch always stays even with upstream.
- **Surgical bug fixes (`fix/*`) vs. feature enhancements (`feat/*`).** Bug fixes that restore expected stock behavior live on small `fix/*` branches (`<100` lines added). Feature requests from the issue tracker live on separate `feat/*` branches so bug fixes can always be reviewed or taken on their own without bundling extra scope.
- **Respectful PR pacing (at most 3 open PRs at a time).** To avoid flooding the upstream review queue, I keep at most 3 pull requests open on `pounat/absorb` at once and hold finished branches in the staged tables below until a slot opens.
- **Side-by-side `Absorb Dev` APK ([Releases](https://github.com/TerribleTurtle/absorb/releases)).** The [`dev-ota`](https://github.com/TerribleTurtle/absorb/tree/dev-ota) branch merges all active branches below on top of `upstream/main` and builds a signed `Absorb Dev` (`com.barnabas.absorb.dev`) APK for `arm64-v8a` that installs right alongside the official Absorb app without touching your main install.

### For `@pounat` & Contributors: Inspecting or Cherry-Picking Any Branch

Every pushed `fix/*` and `feat/*` branch starts directly from `upstream/main` (`v1.12.1+304`) with zero cross-branch dependencies. You do not need to wait for me to open a PR if a staged branch below is useful right now - click **`diff`** in any row to inspect the exact changes on GitHub, or pull any single branch into a `pounat/absorb` checkout in one command:

```sh
git fetch https://github.com/TerribleTurtle/absorb.git <branch-name>
git cherry-pick main..FETCH_HEAD
```

---

## Active Scorecard (`12` Active in `Absorb Dev`, `1` Merged Upstream)

### 1. Open Upstream Pull Requests (`3`)

| Issue | Branch & Diff | Upstream PR | Summary |
|---|---|---|---|
| [#430](https://github.com/pounat/absorb/issues/430) | [`fix/cold-start-resume-430`](https://github.com/TerribleTurtle/absorb/tree/fix/cold-start-resume-430) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/cold-start-resume-430), `+38/-28`) | [**PR #438**](https://github.com/pounat/absorb/pull/438) | **Resuming from a widget, headphones, or Android Auto losing progress from another device:** Starting a downloaded book outside the main app screen skipped checking the server for newer progress, so it resumed from the phone's older spot and overwrote the server. Now does a quick server check before starting. |
| Battery / Lifecycle | [`fix/background-pause-lifecycle`](https://github.com/TerribleTurtle/absorb/tree/fix/background-pause-lifecycle) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/background-pause-lifecycle), `+80/-7`) | [**PR #439**](https://github.com/pounat/absorb/pull/439) | **Background battery drain while paused:** Stops four background tasks that kept running after playback paused with the screen off: the shake-to-snooze motion sensor, periodic home-widget refreshes, local-network server pings after a book finishes, and idle Chromecast speaker scanning. |
| [#336](https://github.com/pounat/absorb/issues/336), [#262](https://github.com/pounat/absorb/issues/262) | [`fix/chapters-sheet-scroll-336`](https://github.com/TerribleTurtle/absorb/tree/fix/chapters-sheet-scroll-336) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/chapters-sheet-scroll-336), `+31/-22`) | [**PR #442**](https://github.com/pounat/absorb/pull/442) | **Chapters list opening far away from the current chapter in long books:** In books with hundreds of chapters or multi-line chapter titles, opening the Chapters sheet landed way above the playing chapter. Now measures the real height of each row so the list opens right on your current chapter. |

---

### 2. Staged Bug Fixes - `fix/*` (`7`)

Small, self-contained bug fixes (`<100` lines added) rebased on `upstream/main` and ready to cherry-pick or open as upstream PRs as review slots free up:

| Issue | Branch & Diff | Status | Summary |
|---|---|---|---|
| [#344](https://github.com/pounat/absorb/issues/344) | [`fix/startup-progress-sync-344`](https://github.com/TerribleTurtle/absorb/tree/fix/startup-progress-sync-344) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/startup-progress-sync-344), `+49/-3`) | Staged *(waits on [PR #438](https://github.com/pounat/absorb/pull/438))* | **Multi-device progress sync and paused chapter rewinds snapping back:** Fixes progress not catching up on app launch after listening on another device, and stops rewinding to an earlier chapter while paused from jumping back to the old spot when playback resumes. |
| [#384](https://github.com/pounat/absorb/issues/384) | [`fix/ebook-keep-screen-on-384`](https://github.com/TerribleTurtle/absorb/tree/fix/ebook-keep-screen-on-384) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/ebook-keep-screen-on-384), `+18/-1`) | Staged | **Screen timing out while reading PDFs, comics, or MOBI/AZW3 books:** The "Keep screen awake while reading" setting only worked in the standard EPUB reader. Now keeps the screen awake across the PDF, comic, and Foliate readers too. |
| Discord `#beta-bug-reports` | [`fix/tag-genre-pill-navigation`](https://github.com/TerribleTurtle/absorb/tree/fix/tag-genre-pill-navigation) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/tag-genre-pill-navigation), `+11/-4`) | Staged | **Tapping a tag or genre pill on a book page not showing matching books:** Tapping a tag or genre chip from search results or inside a series/author sheet left the old search text or sheet open instead of switching to the filtered Books tab. |
| [#360](https://github.com/pounat/absorb/issues/360) | [`fix/aa-series-sort-360`](https://github.com/TerribleTurtle/absorb/tree/fix/aa-series-sort-360) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/aa-series-sort-360), `+4/-4`) | Staged | **Android Auto sorting series alphabetically instead of by book number:** Series with prefixes like "Book 1" or "Vol. 2" (or more than 50 books) sorted by title in Android Auto. Now parses the book number properly and loads the full series in reading order. |
| [#422](https://github.com/pounat/absorb/issues/422) | [`fix/auth-token-expiry-422`](https://github.com/TerribleTurtle/absorb/tree/fix/auth-token-expiry-422) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/auth-token-expiry-422), `+35/-10`) | Staged | **Live server sync dropping after the login token refreshes:** When the app woke up after its short-lived access token expired, the live connection reconnected with the old token and permanently dropped real-time sync until an app restart. Now refreshes the token before reconnecting. |
| [#396](https://github.com/pounat/absorb/issues/396) | [`fix/offline-podcast-shows-396`](https://github.com/TerribleTurtle/absorb/tree/fix/offline-podcast-shows-396) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/offline-podcast-shows-396), `+94/-31`) | Staged | **Downloaded podcasts showing as empty in Offline mode:** In Offline mode, downloaded podcast episodes showed up as empty shows on the Shows tab, left the Episodes tab blank, and cluttered the Absorbing screen with unstarted downloads. Now groups downloaded episodes under their show, populates the offline Episodes tab, and keeps unstarted episodes off the Absorbing deck. |
| [#444](https://github.com/pounat/absorb/issues/444), [#456](https://github.com/pounat/absorb/issues/456) | [`fix/auth-refresh-storm-444`](https://github.com/TerribleTurtle/absorb/tree/fix/auth-refresh-storm-444) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/auth-refresh-storm-444), `+55/-9`) | Staged | **Expired login retries triggering firewall bans (CrowdSec) and SSO-only login screens:** Stops the app from firing repeated failed token-refresh requests when a session is revoked (which could trip server rate-limiters/CrowdSec), and hides the username/password boxes on servers configured for Single Sign-On (OIDC) only. |

---

### 3. Community-Requested Enhancements - `feat/*` (`1`)

Quality-of-life enhancements requested on the official issue tracker, kept on isolated `feat/*` branches off `upstream/main` so bug fixes in Section 2 stay pure:

| Issue | Branch & Diff | Status | Summary |
|---|---|---|---|
| [#441](https://github.com/pounat/absorb/issues/441) | [`feat/series-playback-speed-441`](https://github.com/TerribleTurtle/absorb/tree/feat/series-playback-speed-441) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:feat/series-playback-speed-441), `+85/-5`) | Staged | **Playback speed per book series:** Books in the same series now share a playback speed, so changing the speed on any installment automatically carries over when advancing, skipping ahead, or re-reading earlier books in the series. |

---

### 4. In Progress / Active Testing (`1`)

Work currently being built, refined, or road-tested locally in the `Absorb Dev` APK before pushing a standalone branch for upstream review:

| Issue | Branch & Scope | Status | Summary |
|---|---|---|---|
| [#318](https://github.com/pounat/absorb/issues/318) | `feat/android-auto-absorbing-queue-318` (`+97/-8`, local test branch) | In Progress / Testing | **Absorbing queue in Android Auto and CarPlay:** Shows your full Absorbing queue (including unstarted books and multiple queued podcast episodes per show) in exact queue order on the Android Auto and CarPlay Continue tab, updates live when you edit the queue on your phone, and populates the Android Auto Now Playing Queue drawer when listening to podcasts or other audio without chapters. |

---

### 5. Previously Merged Upstream (`1`)

| Issue | Branch | Upstream PR | Summary |
|---|---|---|---|
| [#409](https://github.com/pounat/absorb/issues/409) | `fix/cancel-settings-timer-on-background` ([`3038c453`](https://github.com/pounat/absorb/commit/3038c453)) | [**PR #410**](https://github.com/pounat/absorb/pull/410) *(Merged in `v1.12.0`)* | **Background settings sync timer:** Stops the 45-second settings check timer from running while the app is in the background. |

---

## Installing the Side-by-Side `Absorb Dev` APK ([Releases](https://github.com/TerribleTurtle/absorb/releases))

If you are running into one of the bugs listed above or want to help test an upcoming fix or enhancement alongside your normal Absorb setup:

1. Download the latest `Absorb Dev` APK from [**Releases**](https://github.com/TerribleTurtle/absorb/releases) (or point [Obtainium](https://github.com/ImranR98/Obtainium) at `https://github.com/TerribleTurtle/absorb`).
2. It installs as **Absorb Dev** (`com.barnabas.absorb.dev`) alongside the official Absorb app so your primary install and local data stay separate.
3. Each release is built automatically by GitHub Actions from [`dev-ota`](https://github.com/TerribleTurtle/absorb/tree/dev-ota), which combines `upstream/main` (`v1.12.1+304`) with the 12 active branches in Sections 1-4 above.
4. **Feedback & Issue Reporting:** If you spot a bug or regression while using `Absorb Dev`, please verify whether it also reproduces on the official release from [`pounat/absorb`](https://github.com/pounat/absorb/releases) before filing an upstream ticket, or report fork-specific test feedback directly on [`TerribleTurtle/absorb`](https://github.com/TerribleTurtle/absorb).
