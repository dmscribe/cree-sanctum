# Cree Sanctum Cryptographic Messaging — Project Map

**Author:** Daniel Scribe · [github.com/dmscribe](https://github.com/dmscribe) · [x.com/danRydr](https://x.com/danRydr)  
**Updated:** 2026-09-10

Cree Sanctum Cryptographic Messenger (CS/CM) "Cree Sanctum", "Sanctum" or "Cree Messenger" is a sealed desk, not a feed.

Keys live on the device. Words travel as ciphertext. Voice dies in twenty-four hours. The graph is an edge list you can cut — block, remove, stealth — not a score you cannot see. Discover is nine cards and a lesson: chat never trains the radar.

Two layers hold the lock. One layer ranks the room. C++ is the law; the browser is only the window. Ghosts keep the desk alive so a human seat is never empty. Poles watch the horizon. Starters sit at the bottom of Contacts and stay servants, not people.

Built to remember who you spoke to, never what you said. Built so a search is not a marriage, a profile open is not a claim, and a lodge is not a plantation. Thunderbird on teal glass. Mail that does not work for the algorithm.

C++ is the source of truth for the mailbox, identity binding, and Discover engine. The web cockpit is the desk: a windowed web OS. This file lists the product tree. Each line is a file and what it does. 

---

## Logo

Logo **Cree Sanctum Insignia**, inspired by the Pimicikamak flag (*Bird of Thunder*) — Cross Lake Cree Nation, Manitoba: red thunderbird, three stars for Cryptography, Privacy, and Language. The messenger is the bird.

Artists may use the logo as a base for beadwork medallions and sell them for $150.00 or more, so long as they explain what the logo is for and where it came from.  It was meant to stand parallel with Indigenous art.

---

## Root

| File | Role |
|---|---|
| `AGENTS.md` | App-builder sandbox contract (preview port, auth, skills) |
| `LICENSE` | Apache 2.0 licence text |
| `LICENSE-MIT` | MIT licence text (dual MIT / Apache 2.0, © 2026 Daniel Scribe) |
| `Makefile` | C++ test / bench / `sanctumd` / zip targets |
| `README.md` | Human README for the tree |
| `PROJECTMAP.TXT` | This map |
| `startup.sh` | Revive contract: start `npm run dev` on `0.0.0.0:8080` if down |
| `package.json` | Web cockpit scripts and dependencies |
| `package-lock.json` | Locked npm graph |
| `tsconfig.json` | TypeScript paths (`@/` → `src/`) |
| `vite.config.ts` | TanStack Start / Vite; port 8080 |
| `eslint.config.mjs` | Lint rules |

---

## C++ (source of truth)

| Path | Role |
|---|---|
| `libsanctum/include/sanctum/sanctum.hpp` | **Layer A.** Ciphertext packet, voice TTL 24h, size caps, ECIES info string |
| `libpgpbind/include/pgpbind/bind.hpp` | **Layer B.** Canonical device-binding string. Secret keys never on the wire |
| `libsuggest/include/suggest/suggest.hpp` | **Layer C.** PYMK: generate → score → filter → slot. Chat must never call `on_open` |
| `libsuggest/tests/fixtures.cpp` | C++ fixtures for the ranking engine |
| `libsuggest/tests/bench.cpp` | Ranking-engine microbench |
| `sanctumd/main.cpp` | Thin C++ daemon sketch. Prints the HTTP surface the tree must expose |

---

## Schema

| Migration | Role |
|---|---|
| `migrations/0001_auth.sql` | Better Auth tables (copy of `migrations/auth/`) |
| `migrations/0002_sanctum.sql` | Mailbox, profiles, conversations, ciphertext |
| `migrations/0003_ghosts.sql` | `ghost_vaults`, `network_memberships`, `algorithm_logs` |
| `migrations/0004_desk.sql` | Desk extras (presence / seat) |
| `migrations/0005_identity.sql` | Unsigned seats, throwaway, GPS, gravelogs, expiry |
| `migrations/0006_desk_media.sql` | Picture / video ciphertext columns |
| `migrations/0007_edges.sql` | Edge-list columns on friendships / friend_requests |
| `migrations/0008_ghost_pings.sql` | `\|\|` command: delayed ghost notification pings |
| `migrations/auth/0001_auth.sql` | Canonical auth schema; copied to `0001_auth.sql` |

---

## Web cockpit — routes

| Path | Role |
|---|---|
| `src/router.tsx` | `getRouter()`; default error component |
| `src/routeTree.gen.ts` | Generated TanStack route tree. Do not hand-edit |
| `src/routes/__root.tsx` | Document shell, `AuthProvider`, no `og:*` tags |
| `src/routes/index.tsx` | `/` — Landing if signed out, Desktop if signed in |
| `src/routes/login.tsx` | Email / key-file / throwaway sign-in page |
| `src/routes/_app.tsx` | Authed layout: Desktop plus hidden Outlet |
| `src/routes/_app/chat.$peerId.tsx` | Legacy `/chat/:id` (Outlet is hidden; desk owns chat) |
| `src/routes/_app/console.tsx` | Ryder node log (also `NodeLogWin` on the desk) |
| `src/routes/_app/discover.tsx` | Discover radar page (`DiscoverWin` wraps the panel) |
| `src/routes/_app/friends.tsx` | Friends list page (desk Contacts is the live seat) |
| `src/routes/_app/identity.tsx` | Identity page (`IdentityWin` wraps the panel) |
| `src/routes/_app/map.tsx` | Debug map of servants |
| `src/routes/_app/source.tsx` | C++ zip download page |
| `src/routes/_app/views.tsx` | Who opened you (`ViewsWin` wraps the panel) |
| `src/routes/api/auth/$.ts` | Better Auth HTTP handler |

---

## Web cockpit — desk (the product)

### Windows

| Path | Role |
|---|---|
| `src/components/desk/Desktop.tsx` | Window host + taskbar. First-run maximised |
| `src/components/desk/Win.tsx` | Square window chrome, Fit, clamp above taskbar |
| `src/components/desk/Taskbar.tsx` | Start menu, apps, GPS, audio/mic, clock, Fit/−/+ |
| `src/components/desk/ContactsSeat.tsx` | Humans-first home. Requests (tester ghost), presence groups, starter ghosts at the bottom. Servants are not painted as people. Polls pings + unread |
| `src/components/desk/RoomsWin.tsx` | Poles, regional networks, ciphertext rooms |
| `src/components/desk/ChatWin.tsx` | Chat wrapper; arms `\|\|` pings when the room closes |
| `src/components/desk/CardWin.tsx` | Person card: block / remove / last-active / GPS |
| `src/components/desk/MoodsWin.tsx` | 48h mood board. Time, not a feed |
| `src/components/desk/DiscoverWin.tsx` | Radar lesson wrapped for the desk |
| `src/components/desk/ViewsWin.tsx` | Who opened your card |
| `src/components/desk/IdentityWin.tsx` | Keys, Code Talker, receipts, links |
| `src/components/desk/AboutWin.tsx` | Guide downloads, C++, donations, legal ledger |
| `src/components/desk/NodeLogWin.tsx` | Ryder ranking log |
| `src/components/desk/SqPortrait.tsx` | Square portrait + presence dot |

### Desk libs

| Path | Role |
|---|---|
| `src/lib/desk/store.ts` | Zustand window manager, marks, Fit, focus no-op |
| `src/lib/desk/chime.ts` | Sign-on sine vs receive triangle; mic/audio flags |
| `src/lib/desk/identity.ts` | Seat labels, last-active buckets, unsigned copy |
| `src/lib/desk/identity.test.ts` | Seat-label tests |
| `src/lib/desk/mates.ts` | Client helper around desk people (thin) |

---

## Web cockpit — panels / chrome

| Path | Role |
|---|---|
| `src/components/Landing.tsx` | Signed-out home. Throwaway + key file + email |
| `src/components/FirstRun.tsx` | Before you speak: name, city, nine-card lesson |
| `src/components/ChatThread.tsx` | Sealed thread, warning, emotes, media, ghost `\|\|` |
| `src/components/DiscoverPanel.tsx` | Nine-card radar. Chat never trains `on_open` |
| `src/components/ViewsPanel.tsx` | Discover views list |
| `src/components/FriendsPanel.tsx` | Legacy friends list (desk Contacts replaced it) |
| `src/components/IdentityPanel.tsx` | Long-term key, binding, Code Talker, stealth |
| `src/components/RoomsHome.tsx` | Old cockpit Rooms page (`RoomsWin` is live) |
| `src/components/AppShell.tsx` | Unused nav chrome; desk Taskbar is the OS |
| `src/components/AlgorithmConsole.tsx` | Ryder algorithm log viewer |
| `src/components/SanctumProvider.tsx` | Seat, vault, stealth, first-run, profile |
| `src/components/ServantCard.tsx` | Network-servant card. `onChat` opens a desk room |
| `src/components/ServantSheet.tsx` | Process overlay. Embedded mode for desk Rooms |
| `src/components/Emotes.tsx` | Large emoticons. Satire mark is a middle finger |
| `src/components/MediaBubble.tsx` | Picture/video bubble; blacked until Open |
| `src/components/VoiceBubble.tsx` | Walkie-talkie playback (24h TTL) |
| `src/components/VoiceRecorder.tsx` | Hold-to-talk recorder. Audio / Mute mic |
| `src/components/VerifyRitual.tsx` | Fingerprint compare |
| `src/components/Portrait.tsx` | Round-ish portrait used off the desk |
| `src/components/LogoMark.tsx` | Thunderbird + cyan diamond wordmark |
| `src/components/preview-host-bridge.tsx` | Live-preview host bridge |
| `src/components/ui/button.tsx` | Shared button |
| `src/components/ui/input.tsx` | Shared input (`suppressHydrationWarning`) |

---

## Web cockpit — crypto / protocol

| Path | Role |
|---|---|
| `src/lib/sanctum/crypto.ts` | ECIES P-256 + HKDF-SHA-256 + AES-GCM |
| `src/lib/sanctum/pgp.ts` | Ed25519 identity, binding, sign/verify |
| `src/lib/sanctum/pgp.test.ts` | Binding and signature tests |
| `src/lib/sanctum/protocol.ts` | Wire types, caps, `InnerPlaintext` |
| `src/lib/sanctum/vault.ts` | IndexedDB device vault + trust state |
| `src/lib/sanctum/session.ts` | Seat bundle, export, download helpers |
| `src/lib/sanctum/seat-key.ts` | Throwaway / key-file seat helpers |
| `src/lib/sanctum/links.ts` | Conservative link allow-list |

---

## Web cockpit — server functions

| Path | Role |
|---|---|
| `src/lib/db.ts` | Neon or PGLite. Applies `migrations/*.sql` |
| `src/lib/server/ids.ts` | UUID, slug username, `nowIso` |
| `src/lib/server/session.ts` | `fetchSessionUser` for route loaders |
| `src/lib/server/profile.ts` | Profile, first-run, GPS, stealth, self-delete |
| `src/lib/server/mailbox.ts` | Ciphertext send/list, friend edges, requests |
| `src/lib/server/ghosts.ts` | Seed servants, 5s mirror, `\|\|` pings, tester request |
| `src/lib/server/edges.ts` | Friend / block / remove / request-source stamps |
| `src/lib/server/mates.ts` | Desk people, presence, starter mates (Mara / Eli / Pip) |
| `src/lib/server/radar.ts` | Discover slots, views, block |
| `src/lib/server/ledger.ts` | Async timestamp seal for the legal ledger |
| `src/lib/server/gravelog.ts` | Gravelogs (who you talked to, not the words) |
| `src/lib/server/ratelimit.server.ts` | IP boot/msg caps. Loopback exempt |
| `src/lib/ghosts/catalog.ts` | 2 poles + 10 regional servants. Tester pool helper |
| `src/lib/suggest/engine.ts` | JS port of `libsuggest` for the live radar |
| `src/lib/suggest/engine.test.ts` | Ranking tests |
| `src/lib/geo/reverse.ts` | Device GPS → admin1 / country (consent-gated) |
| `src/lib/utils.ts` | `cn()` class merge |
| `src/lib/env.server.ts` | Server env reads |
| `src/lib/error-component.tsx` | `AppErrorComponent` (keeps `error.message`) |
| `src/lib/preview-host-bridge.ts` | Preview embedder origin helpers |
| `src/lib/preview-embedder-origin.ts` | Allowed embedder origins |
| `src/lib/og/site.json` | Custom OG card identity (not `x:game`) |

---

## Auth (Better Auth on)

| Path | Role |
|---|---|
| `src/lib/auth/client.ts` | Browser auth client |
| `src/lib/auth/server.ts` | Better Auth instance |
| `src/lib/auth/middleware.ts` | `authMiddleware` — scopes every server fn by `userId` |
| `src/lib/auth/provider.tsx` | `AuthProvider` |
| `src/lib/auth/providers.ts` | Email / anonymous / key-file providers |
| `src/lib/auth/gates.tsx` | `RedirectToSignIn`, `UserButton` |
| `src/lib/auth/email-password.ts` | Email+password helpers |
| `src/lib/auth/use-current-user.ts` | Current user hook |
| `src/lib/auth/preview.ts` | Preview-only auth helpers |
| `src/lib/auth/pglite-dialect.ts` | Kysely dialect for PGLite |
| `src/lib/auth/isolation.server.ts` | Per-user isolation helpers |
| `src/lib/auth/popup.server.ts` | Popup sign-in helper |
| `src/lib/auth/gate-session.server.ts` | Gate session cookie |
| `src/lib/auth/gate-session-marker.ts` | Client marker for a gate session |
| `src/lib/auth/gate-identity.server.ts` | Gate identity |
| `src/lib/auth/gate-identity.test.ts` | Gate identity tests |
| `src/lib/auth/sign-in-gate.ts` | Sign-in gate copy / flow |
| `src/lib/auth/sign-in-gate.test.ts` | Sign-in gate tests |
| `src/lib/auth/verify.server.ts` | Session verify |

---

## App-data / multiplayer (platform stubs, unused by the desk)

| Path | Role |
|---|---|
| `src/lib/app-data/*` | Connector readiness (calendar/mail). Not the product |
| `src/lib/multiplayer/index.ts` | P2P stub |
| `src/lib/multiplayer/p2p.ts` | P2P stub |

---

## Styles

| Path | Role |
|---|---|
| `src/styles.css` | Tailwind v4 + desk tokens (`--taskbar-h`, teal desk) |

---

## Scripts

| Path | Role |
|---|---|
| `scripts/with-app-env.mjs` | Injects `VITE_AUTH_ENABLED`. `npm run dev` goes through this |
| `scripts/with-app-env.test.mjs` | Tests |
| `scripts/preview.mjs` | Start/stop the preview on 8080 |
| `scripts/preview.test.mjs` | Tests |
| `scripts/preview-thumbnail.mjs` | Thumbnail helper |
| `scripts/migrate.mjs` | Apply migrations to `DATABASE_URL` on deploy |
| `scripts/migration-plan.mjs` | Pending-migration order |
| `scripts/migration-plan.test.mjs` | Tests |
| `scripts/qa-desk.mjs` | Playwright desk QA (rooms, tester request, chat, stealth) |
| `scripts/qa-ghosts.mjs` | Ghost-network Playwright checks |
| `scripts/debug-chat.mjs` | Chat-click diagnosis |
| `scripts/write-guide-pdf.mjs` | Build `public/cree-sanctum-guide.pdf` from guide-source |
| `scripts/write-atomic.mjs` | Atomic file write |
| `scripts/write-atomic.test.mjs` | Tests |
| `scripts/brand-check.mjs` | Brand / OG checks |
| `scripts/brand-check.test.mjs` | Tests |
| `scripts/browser-smoke.mjs` | Browser smoke |
| `scripts/browser-smoke-verdict.mjs` | Smoke verdict |
| `scripts/browser-smoke-verdict.test.mjs` | Tests |
| `scripts/browser-guard.mjs` | Browser-only import guard |
| `scripts/check-auth-invariant.mjs` | Auth-on invariant (`authMiddleware` on server fns) |
| `scripts/check-auth-invariant.test.mjs` | Tests |
| `scripts/sign-out-plan.mjs` | Sign-out flow checks |
| `scripts/sign-out-plan.test.mjs` | Tests |
| `scripts/app-env-plugin.mjs` | Vite plugin for app-env |
| `scripts/install-page.html` | Platform install tutorial HTML |

---

## Docs

| Path | Role |
|---|---|
| `docs/PROJECT_MAP.md` | Architecture map. Points here for the file list |
| `docs/THREAT_MODEL.md` | Honest threat model |
| `docs/guide-source.txt` | British-English user guide source (double-spaced) |
| `docs/admin-ledger-secret.txt` | Admin ledger passphrase (workspace only) |
| `docs/system-diagram.svg` | Layer A/B/C diagram |
| `docs/system-diagram.png` | Raster of the same |

---

## Public

| Path | Role |
|---|---|
| `public/logo.png` | Red thunderbird + cyan diamond. Use as-is |
| `public/favicon.svg` | Favicon |
| `public/og.jpg` | Custom Open Graph card |
| `public/bc.png` | Brand mark extra |
| `public/cree-sanctum-guide.txt` | Shipped user guide (TXT) |
| `public/cree-sanctum-guide.pdf` | Shipped user guide (PDF) |
| `public/cree-sanctum-cpp.zip` | Downloadable C++ tree |
| `public/LICENSE-APACHE.txt` | Apache 2.0 for the download |
| `public/LICENSE-MIT.txt` | MIT for the download |
| `public/system-diagram.svg` | Diagram for About / source |
| `public/system-diagram.png` | Raster diagram |


## How the live pieces fit

1. New account → first-run → generate identity.
2. `profile.completeFirstRun` befriends three starter ghosts (**Mesa Index**, **Harbor Ledger**, **Tide Mesh**) and one **random tester ghost** sends a friend request (Discover or username source). Poles stay off Contacts home.
3. **Contacts** is humans (Mara, Eli, Pip). **Rooms** (Start menu) is poles + regional networks + ciphertext rooms.
4. Ordinary ghost text is mirrored after five seconds.
5. A line starting with `||` does not 5s-mirror. The ghost acks “Armed.” Closing or minimising that room arms a ping that fires 15–30 seconds later so the mail mark and receive chime can be demonstrated.
6. **Stealth** greys Discover and Views in the Start menu (they still launch) and blocks inbound friend requests.
7. Edge list (friendships / requests / bans) is the graph. Block, remove, and request source live on those rows.

---

## Ghosts

**Poles (exclusive):** Ryder (North), Charlie (South)

**Starter set (every seat):** Mesa Index, Harbor Ledger, Tide Mesh

**Tester pool (one random):** Rain Cache, Fault Feed, Horizon Queue, Freshwater Graph, Ridge Signal, Nickel Wire, Aurora Buffer
