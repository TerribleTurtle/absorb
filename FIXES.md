# Absorb Dev: Fixes, Features & Test Builds

Daily-driver fork of Nathan Poulson's ([`@pounat`](https://github.com/pounat)) [**Absorb**](https://github.com/pounat/absorb) targeting open issues and feature requests not yet addressed in the official build.

Every fix (`fix/*`) and feature (`feat/*`) lives on its own clean branch off `upstream/main` so it can be sent upstream as a pull request and dropped once it lands in the official app.

### How This Repo Is Organized

- **`main` mirrors [`pounat/absorb:main`](https://github.com/pounat/absorb) 1:1.** I never commit directly to `main` on GitHub so the default branch always stays even with upstream.
- **One issue or feature = one branch (`fix/*` or `feat/*`).** Every branch starts cleanly from `upstream/main` so it is easy to review or cherry-pick on its own.
- **Side-by-side `Absorb Dev` APK ([Releases](https://github.com/TerribleTurtle/absorb/releases)).** The `dev-ota` branch merges all active `fix/*` and `feat/*` branches on top of `upstream/main` and builds a signed `Absorb Dev` (`com.barnabas.absorb.dev`) APK for `arm64-v8a`. Because it uses the `.dev` package ID, it installs right alongside the official Absorb app without overwriting your main install.

---

## Active Branches (`11` Active, `1` Merged Upstream)

### 1. Open Upstream Pull Requests

| Issue | Branch & Diff | Upstream PR | Summary |
|---|---|---|---|
| [#430](https://github.com/pounat/absorb/issues/430) | [`fix/cold-start-resume-430`](https://github.com/TerribleTurtle/absorb/tree/fix/cold-start-resume-430) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/cold-start-resume-430), `+38/-28`) | [**PR #438**](https://github.com/pounat/absorb/pull/438) | **Resuming from a widget, headphones, or Android Auto losing progress from another device:** Starting a downloaded book outside the main app screen skipped checking the server for newer progress, so it resumed from the phone's older spot and overwrote the server. Now does a quick server check before starting. |
| Battery / Lifecycle | [`fix/background-pause-lifecycle`](https://github.com/TerribleTurtle/absorb/tree/fix/background-pause-lifecycle) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/background-pause-lifecycle), `+80/-7`) | [**PR #439**](https://github.com/pounat/absorb/pull/439) | **Background battery drain while paused:** Stops four background tasks that kept running after playback paused with the screen off: the shake-to-snooze motion sensor, periodic home-widget refreshes, local-network server pings after a book finishes, and idle Chromecast speaker scanning. |
| [#336](https://github.com/pounat/absorb/issues/336), [#262](https://github.com/pounat/absorb/issues/262) | [`fix/chapters-sheet-scroll-336`](https://github.com/TerribleTurtle/absorb/tree/fix/chapters-sheet-scroll-336) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/chapters-sheet-scroll-336), `+27/-19`) | [**PR #442**](https://github.com/pounat/absorb/pull/442) | **Chapters list opening far away from the current chapter in long books:** In books with hundreds of chapters or multi-line chapter titles, opening the Chapters sheet landed way above the playing chapter. Now measures the real height of each row so the list opens right on your current chapter. |

---

### 2. Staged Branches (Live on This Fork, Queued for Upstream PRs)

To avoid overwhelming the upstream PR queue, I keep these staged on their own branches until open PRs are reviewed. Each branch is rebased cleanly on `upstream/main` and can be cherry-picked independently:

| Issue | Branch & Diff | Status | Summary |
|---|---|---|---|
| [#344](https://github.com/pounat/absorb/issues/344) | [`fix/startup-progress-sync-344`](https://github.com/TerribleTurtle/absorb/tree/fix/startup-progress-sync-344) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/startup-progress-sync-344), `+49/-3`) | Staged *(waits on [PR #438](https://github.com/pounat/absorb/pull/438))* | **Multi-device progress sync and paused chapter rewinds snapping back:** Fixes progress not catching up on app launch after listening on another device, and stops rewinding to an earlier chapter while paused from jumping back to the old spot when playback resumes. |
| [#384](https://github.com/pounat/absorb/issues/384) | [`fix/ebook-keep-screen-on-384`](https://github.com/TerribleTurtle/absorb/tree/fix/ebook-keep-screen-on-384) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/ebook-keep-screen-on-384), `+18/-1`) | Staged | **Screen timing out while reading PDFs, comics, or MOBI/AZW3 books:** The "Keep screen awake while reading" setting only worked in the standard EPUB reader. Now keeps the screen awake across the PDF, comic, and Foliate readers too. |
| Discord `#beta-bug-reports` | [`fix/tag-genre-pill-navigation`](https://github.com/TerribleTurtle/absorb/tree/fix/tag-genre-pill-navigation) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/tag-genre-pill-navigation), `+12/-6`) | Staged | **Tapping a tag or genre pill on a book page not showing matching books:** Tapping a tag or genre chip from search results or inside a series/author sheet left the old search text or sheet open instead of switching to the filtered Books tab. |
| [#360](https://github.com/pounat/absorb/issues/360) | [`fix/aa-series-sort-360`](https://github.com/TerribleTurtle/absorb/tree/fix/aa-series-sort-360) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/aa-series-sort-360), `+4/-4`) | Staged | **Android Auto sorting series alphabetically instead of by book number:** Series with prefixes like "Book 1" or "Vol. 2" (or more than 50 books) sorted by title in Android Auto. Now parses the book number properly and loads the full series in reading order. |
| [#422](https://github.com/pounat/absorb/issues/422) | [`fix/auth-token-expiry-422`](https://github.com/TerribleTurtle/absorb/tree/fix/auth-token-expiry-422) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/auth-token-expiry-422), `+35/-10`) | Staged | **Live server sync dropping after the login token refreshes:** When the app woke up after its short-lived access token expired, the live connection reconnected with the old token and permanently dropped real-time sync until an app restart. Now refreshes the token before reconnecting. |
| [#396](https://github.com/pounat/absorb/issues/396) | [`fix/offline-podcast-shows-396`](https://github.com/TerribleTurtle/absorb/tree/fix/offline-podcast-shows-396) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/offline-podcast-shows-396), `+94/-31`) | Staged | **Downloaded podcasts showing as empty in Offline mode:** In Offline mode, downloaded podcast episodes showed up as empty shows on the Shows tab, left the Episodes tab blank, and cluttered the Absorbing screen with unstarted downloads. Now groups downloaded episodes under their show, populates the offline Episodes tab, and keeps unstarted episodes off the Absorbing deck. |
| [#444](https://github.com/pounat/absorb/issues/444) | [`fix/auth-refresh-storm-444`](https://github.com/TerribleTurtle/absorb/tree/fix/auth-refresh-storm-444) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:fix/auth-refresh-storm-444), `+55/-9`) | Staged | **Expired login retries triggering firewall bans (CrowdSec) and SSO-only login screens:** Stops the app from firing repeated failed token-refresh requests when a session is revoked (which could trip server rate-limiters/CrowdSec), and hides the username/password boxes on servers configured for Single Sign-On (OIDC) only. |
| [#441](https://github.com/pounat/absorb/issues/441) | [`feat/series-playback-speed-441`](https://github.com/TerribleTurtle/absorb/tree/feat/series-playback-speed-441) ([diff](https://github.com/pounat/absorb/compare/main...TerribleTurtle:absorb:feat/series-playback-speed-441), `+85/-5`) | Staged | **Playback speed per book series:** Books in the same series now share a playback speed, so changing the speed on any installment automatically carries over when advancing, skipping ahead, or re-reading earlier books in the series. |

---

### 3. Previously Merged Upstream

| Issue | Branch | Upstream PR | Summary |
|---|---|---|---|
| [#409](https://github.com/pounat/absorb/issues/409) | `fix/cancel-settings-timer-on-background` ([`3038c453`](https://github.com/pounat/absorb/commit/3038c453)) | [**PR #410**](https://github.com/pounat/absorb/pull/410) *(Merged in `v1.12.0`)* | **Background settings sync timer:** Stops the 45-second settings check timer from running while the app is in the background. |

---

## Using the `Absorb Dev` Test APK ([Releases](https://github.com/TerribleTurtle/absorb/releases))

If you are running into one of the issues listed above or want to try an unmerged feature before it lands in an official Absorb release:

1. Grab the latest `Absorb Dev` APK from [**Releases**](https://github.com/TerribleTurtle/absorb/releases) (or point [Obtainium](https://github.com/ImranR98/Obtainium) at `https://github.com/TerribleTurtle/absorb`).
2. It installs as **Absorb Dev** (`com.barnabas.absorb.dev`) alongside the official Absorb app so your normal setup stays untouched.
3. Each release is built automatically by GitHub Actions from [`dev-ota`](https://github.com/TerribleTurtle/absorb/tree/dev-ota), which is simply `upstream/main` (`v1.12.1+301`) plus the 11 active branches listed above.
4. **Please don't bug Nathan with issues specific to this test build** - if you notice something odd while using `Absorb Dev`, double-check whether it also happens on the official release from [`pounat/absorb`](https://github.com/pounat/absorb/releases) before opening an upstream issue.
