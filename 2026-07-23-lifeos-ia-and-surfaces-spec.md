# LifeOS iOS app — IA & surface map — Design Spec

> **Provenance.** Authored by Nick Vyhouski as part of **LifeOS**, an independent
> personal life-management system he has designed and built for his own use since
> **April 2026**. This document is published unmodified in substance from the original
> dated working spec held in a private version-controlled repository
> (`weeeha/LifeOS`, initial commit 2026-04-25). Only private links, internal
> cross-references, and file paths have been removed. Published 2026-08-11.
>
> LifeOS and all derivatives of it remain the property of the author.

---


**Date:** 2026-07-23
**Owner:** Nick
**Status:** Draft (approved direction; wireframe rework pending)
**Related:** Life Game concept spec · mobile app design

## Problem

The Life Game model defines **12 economy objects** (5 vitals · 3 stocks · 4 readouts) and **5 entity types** (Areas, People, Tasks/Projects/Quests, Skills, Journey nodes). The 12 wireframes drawn on 2026-07-22 surface **5 of the 12** — the vitals strip — and one entity type is missing entirely (People). Meanwhile three concrete IA faults surfaced in review: the (+) is a center FAB notching the tab bar, **Projects** is rendered inside Area Detail but has no home of its own, and **Me** occupies a full tab despite being the one thing already represented everywhere (the avatar).

Both problems have the same fix, which is why they're specced together: a model object with no surface is a model object that will quietly stop being true, and the tab bar has exactly one slot's worth of room to fix it.

## Users & JTBD

- **Primary user:** Nick. Single-player, personal. iOS, one-handed, mostly in-the-moment.
- **Job to be done:** *"Show me an honest picture of where my life is and who I'm becoming — and pull me toward the next right action."* Emotional job = **mirror + motivate**, not dopamine.
- **Constraint that shapes everything:** capture must cost ~nothing (thumb-reachable, one tap), because a system fed by hand is a system that dies.

## Approach

**Five tabs, one avatar, one capture button, three overlays.**

```
┌ avatar (top-left) ──────────────── screen title ── [⋯] ┐   → Me / Avatar
│                                                        │
│                     tab content                        │
│                                                        │
│                                            ( + )       │   → Capture sheet
├────────────────────────────────────────────────────────┤   (bottom-right,
│   Home    Tasks    Chats    Areas    People            │    above the bar)
└────────────────────────────────────────────────────────┘
```

**1. Me stops being a tab and becomes the avatar in the top-left.** The avatar is already the Home hero and the face of the vitals; a tab pointing at "you" in an app that is *entirely* about you is a tautology spending a scarce slot. Tapping it opens Me — and Me is the hub for the three overlays (Journey · Skills · Resources) plus Experience/history.

**2. The freed slot goes to People.** Not a nicety: People drive the Stability vital and compute the Social Support readout, so the model's most human input currently has no surface at all.

**3. Tasks gets sub-navigation for the three altitudes.** The concept spec says task (minutes) / challenge (weeks) / life project (years) are *the same loop at three zoom levels*. So the segmented control isn't three features bolted together — it's one object at three altitudes: **Today · Projects · Quests**. This also gives Projects the home it lacks (Area Detail already lists them).

**4. The (+) moves to a floating bottom-right button above the tab bar.** Standard iOS placement, thumb-reachable, and it stops mutilating the tab bar.

### Alternatives considered

| Option | Why not |
|---|---|
| **Six tabs** (keep Me, add People) | 6 tabs is the point where a tab bar becomes a menu; iOS crowds badly at 6 with labels. |
| **People folded into the Areas grid** | An Area is a domain with a balance bar; a person is an entity with closeness, recency, and a live effect on Stability. This is precisely how the Relationship Map got lost the first time. |
| **People as an overlay off Me** (keep Me tab) | Buries the one entity that's a daily-cadence object behind two taps, and leaves the tautological Me tab in place. |
| **Keep the center FAB notching the tab bar** | Non-standard on iOS, competes with the 5 tabs for the same visual band, and was already flagged as unresolved at the end of the wireframe session. |
| **Resources as a 6th tab** | It's a *readout* surface — reference, not daily. Overlay off the avatar is the right frequency. |

## Surface map

Every object in the model, and the one place it lives. **If a row has no surface, the model object isn't real.**

| # | Object | Layer | Primary surface | Also appears |
|---|---|---|---|---|
| 1 | **Energy** | Vital | Vitals strip — Home | Me, Resources, Check-in |
| 2 | **Clarity** | Vital | Vitals strip — Home | Me, Resources, Check-in |
| 3 | **Willpower** | Vital | Vitals strip — Home | Me, Resources, Check-in |
| 4 | **Stability** | Vital | Vitals strip — Home | Me, Resources, **People** |
| 5 | **Inspiration** | Vital | Vitals strip — Home | Me, Resources, Check-in |
| 6 | **Experience** | Stock | **Experience / history** (new) | XP on quest + task-complete |
| 7 | **Skills** | Stock | Skill Map overlay | Area Detail, quest rewards |
| 8 | **Money** | Stock | Finance area | **Rewards** (new) — the spend side |
| 9 | **Joy** ★ | Readout | Weekly Review (new) — trend only | Avatar state (glow) |
| 10 | **Confidence** | Readout | Resources overlay (new) | Me |
| 11 | **Momentum** | Readout | Home | Weekly Review |
| 12 | **Social Support** | Readout | **People** tab header | Resources overlay |
| E1 | **Areas** (14) | Entity | Areas tab | Area Detail |
| E2 | **People** | Entity | **People** tab (new) | Person Detail (new), Stability |
| E3 | **Tasks / Projects / Quests** | Entity | Tasks tab (3 altitudes) | Task Detail, Journey |
| E4 | **Skills** | Entity | Skill Map overlay | Area Detail |
| E5 | **Journey nodes** | Entity | Journey overlay | Home quest strip |
| — | **Avatar** | The hub | Top-left, every screen | Home hero, Me, Journey |
| — | **Cards** | Interpretation | Home feed | Check-in, notifications |

Deliberate absences: **Joy never gets a meter** (it's the optimized outcome, never a currency) — it appears only as a trend in Weekly Review and as the avatar's glow. **No person ever gets a score.**

## Key flows / screens

**Rework (existing 12 — `10:652`):**

- **All frames** — (+) → floating bottom-right above the tab bar; avatar → top-left of the nav bar; tab bar → Home · Tasks · Chats · Areas · People.
- **01 Home** — unchanged except chrome. (Density stays a known risk — see Open Questions.)
- **02 Tasks** — add segmented control **Today · Projects · Quests**; Projects list = name, area, next action, progress; Quests = cost/reward cards.
- **05 Me** — no longer a tab; reached from the avatar. Becomes the hub: vitals, stat tiles, and entries into **Journey · Skills · Resources · Experience**.
- **03 Chats · 04 Areas · 06 Capture · 07 Chat Thread · 08 Task Detail · 09 Area Detail · 10 Journey · 11 Skill Map · 12 Check-in** — chrome only.

**New (row 3):**

- **13 People** — closeness rings (inner · close · active · periphery), Social Support readout in the header, drift surfaced as elapsed time (never as a broken streak).
- **14 Person Detail** — ring, last contact, shared areas, linked threads/memories, cadence intent; the restore/drain note lives here and is private.
- **15 Resources** — the full three-layer economy on one screen: 5 vitals (spendable) · 3 stocks (growing) · 4 readouts (computed, visually distinct from the first two).
- **16 Experience / history** — the readable past: what happened, what it cost, what it grew. Answers "history is cheap, it disappears."
- **17 Weekly Review** — the pattern, named. Joy trend, vital rhythm, what moved on the journey.
- **18 Rewards** — the spend side of Money-stock on real, self-defined rewards, including the guilt-free day off (the rest mechanic priced at zero).

**New (row 4 — the three altitudes made real):**

- **19 Tasks → Projects** — the weeks altitude: active projects with next action, progress and open count; a quieter Someday group.
- **20 Tasks → Quests** — the game altitude: every card states its **ledger** (cost in vitals → payout in vitals/XP/skill), grouped Main · Challenge (pays extra, ranked) · Daily · Recovery.
- **21 Project Detail** — progress, task list, the skills it grows, its Journey milestone, and the **asymmetric ledger** ("drains Energy·Clarity, pays Inspiration·Joy·Experience — no money; the opposite ledger to the day job").

**New (the two Journey sub-views the re-cut tabs promised):**

- **22 Journey → Milestones** — the years altitude as a vertical path: done · you-are-here (focus ring) · next · locked, with an alternate-route hint. A milestone *is* a life project.
- **23 Journey → Chapters** — named life periods (the "vision of me" axis). Chapters aggregate from named weeks (Weekly Review, screen 17); enough same-toned weeks proposes a chapter break.

**New (onboarding / pairing — there is no conventional login):**

Auth is **device-pairing over Tailscale**, dictated by the verified gateway protocol (gateway-protocol.md S0/S2), not email/password. There is no account, no signup, and — per S2 — **no approval-wait**: a signed device is trusted immediately with read+write.

- **24 Welcome** — LifeOS mark, "Private. Runs on your Mac. No account.", one CTA: Connect to my Mac.
- **25 Pair** — `openclaw pair` on the Mac → scan QR (carries gateway URL + token), or paste the connection link; Tailscale-network hint.
- **26 Connecting → Connected** — the real steps: found gateway → **created a device key (Keychain)** → signed the challenge → connected; success panel; and the "Can't reach your Mac — is Tailscale on?" failure (nothing created).

**New (selectors — the sheet controls behind Task Detail & capture):**

- **S1 Time** — relative chips (Today/Tomorrow/…) + time-of-day + "pick exact date"; "No date" always valid.
- **S2 Project** — search + Active list (radio) + "New project".
- **S3 Area** — the 14 domains as a single-select chip grid + "No area".
- **S4 Priority** — None/Low/Medium/High, each with its *meaning* ("today, protect the time"), not just a flag.

**New (completion flow — the Rewards reframe):**

Screen **18 Rewards is deprecated** — a reward is not a store, it's resources received on completion (concept spec).

- **27 Task complete** — small overlay: gains + streak advanced.
- **28 Quest / challenge complete** — bigger overlay: the ledger paid out + the Journey node it moved + "first win after 4 tries".
- **29 Project complete** — the celebration moment ("Shipped.").
- **30 Progress review** — XP delta, skills grown, milestone reached/unlocked, streaks, resources banked, the chapter it belongs to. "No reward store — the reward is the resources, and seeing them move."

### IA diagrams

- **App IA — navigation map** (Figma `87:2`) — the full hierarchy: Launch → Paired? → {Onboarding chain | App shell}; shell → 5 tabs → their pushed detail screens; avatar → Me → the six overlays (Journey/Skills/Resources/Experience/Weekly Review/Rewards); (+) capture reachable from any tab.
- **App IA — surface types** (Figma `88:104`) — the five surface classes and the gesture that defines each: Persistent chrome (always) · Tabs (lateral, no back) · Push (‹ back) · Overlay (✕ full-screen, from the avatar) · Sheet (drag-dismiss, keeps draft; peek/half/full).

## Key design decisions

- **Decision:** Me becomes the top-left avatar; People takes the 5th tab. — **Why:** a tab pointing at "you" is redundant in an app entirely about you, and People is the model's biggest surface gap. — **Alternatives:** 6 tabs; People inside Areas; People as an overlay.
- **Decision:** Tasks carries all three altitudes under one tab. — **Why:** the concept spec already defines them as one loop at three zoom levels; splitting them into separate tabs would contradict the model. — **Alternatives:** separate Projects tab; Quests only inside the game overlay.
- **Decision:** (+) floats bottom-right above the tab bar. — **Why:** iOS-standard, thumb-reachable, stops the FAB and the tabs fighting for one band. — **Alternatives:** center FAB notching the bar; nav-bar button (too far for one-handed capture).
- **Decision:** Journey · Skills · Resources · Experience are overlays off the avatar, not tabs. — **Why:** they're reflection-frequency surfaces, not daily-cadence ones; giving them tabs would put the mirror above the actions. — **Alternatives:** a "Game" tab collecting all four.
- **Decision:** Every model object gets exactly one primary surface (the table above). — **Why:** an unsurfaced object silently decays into fiction; a doubly-surfaced one drifts out of sync.
- **Decision:** Tasks owns the full quest list; the Journey overlay shows only the quests attached to the current path, with a "all quests in Tasks →" cross-link. — **Why:** two complete quest lists is exactly the double-surfacing the rule above forbids; the Journey's job is *where you are*, not *what's on the list*. — **Alternatives:** quests only in Journey (buries the daily-cadence object two taps deep inside a reflection surface).
- **Decision:** The Journey overlay's tabs become **Map · Milestones · Chapters** (were Quests · Streaks · Rewards · Skills). — **Why:** those four made Journey a second hub, and Me is now the hub; each of them has its own home (Tasks, Weekly Review, screen 18, the Skills overlay).

## Constraints

- **Platform:** iOS, SwiftUI. One-handed use is the design target.
- **System:** no visual language committed yet — wireframes stay low-fi grayscale by explicit choice.
- **Technical:** surfaces read from `lifestate` + `memory`; anything shown must be inferable from real signals or a check-in, never hand-maintained.
- **Privacy:** the People restore/drain field never appears in exported, shared, or agent-quotable views.
- **Timeline:** none — concept/design phase, no build commitment.

## Success criteria

- Every row of the surface map resolves to a drawn frame.
- Capture is reachable in one thumb tap from all five tabs.
- A stranger reading the wireframes can name all three resource layers without the spec.
- Nothing in the UI can be farmed: no person score, no Joy meter, no streak-guilt.

## Out of scope

- Visual direction, type scale, color, motion (this is IA + fidelity-neutral structure).
- Onboarding, settings, agent configuration, notification design.
- Build order, SwiftUI implementation, and the parked Life Atlas vs. LifeOS foundation decision.
- Exact vital-inference formulas.

## Review-dump build (2026-07-24)

**Drawn (31–37):**
- **31 People · Rings** — radial closeness rings, you in the centre, periphery as dots. "Distance = closeness. No one is scored."
- **32 People · Faces** — the same people as an avatar grid, grouped by ring.
- **33 Person Detail · knowledge** — connected knowledge blocks: threads · memories · shared projects/habits.
- **34 Memory detail** — what opens on tapping a memory: body, linked people/areas, source thread, related, edit/forget.
- **35 Chats · agents grid** — Lifey as the highlighted hub + 12 specialists 3-wide.
- **36 Chats · rich thread** — in-thread controls in flow: scale → collapsed answer → entity picker (photo avatars) → free text → readout (with provenance) → ledger offer.
- **37 Area Detail · knowledge** — Fitness: feeds which vitals + **KNOWLEDGE → exercises** (the 1,324-item ExerciseDB), notes, grows-skills.

**Settings (38–41)** — reached from Me → Settings. No account (device-pairing auth), so "sign in" from inside the app = connection/device management.
- **38 Settings** — profile + grouped list (Connection · Agents & check-ins · Privacy & app · Unpair).
- **39 Connection & Devices** — gateway status (openclaw/protocol/Tailscale), this device (key fingerprint, scopes), paired-devices list with remove, pair-another (QR), **Unpair & sign out** ("keeps all data on the Mac"). This is the in-app sign-in surface; the cold-start pairing is screens 24–26.
- **40 Check-ins & vitals** — cadence · quiet hours · which vitals · the anti-nag toggles ("Stop asking after 3 skips", "Tell me when it backs off") — the guardrails from the concept spec, made settable.
- **41 Privacy & data** — "everything lives on your Mac", the **locked** person restore/drain field, what agents can see, export JSON, forget a memory, wipe & unpair.

**Agents — administration (42–45)** — the operator side of the 18-agent fleet, reached from Settings → Manage agents (or an agent in Chats). Grounded in the real roster (agents.md) and cron schedule (cron-jobs.md).
- **42 Agents admin** — fleet list: per agent status dot · domain · sessions/cron/last-activity; gateway link.
- **43 Agent · Activity** — one agent (Lifey): header (status · gpt-5.4 · thinking level · workspace), **Open chat** link + Config, tab bar Activity/Sessions/Cron, and the activity feed (chat replies, routing, cron runs — dreaming, snapshot, cost alert).
- **44 Agent · Sessions** — active sessions (sessionKey · running/idle · msg count · Abort) + recent isolated cron-run sessions.
- **45 Agent · Cron** — the agent's scheduled jobs (Memory Dreaming 03:00 … Cost Alert 20:00), each with schedule · next/last · type · enable toggle · Run now; + New cron job.

*(Note: the earlier Chats grid (35) used illustrative agent names; the real roster is 18 agents — Lifey/Scout/Buildy/Mindy/Dr. O'Body/Monty/Grove/Arty/… — corrected here and worth reconciling on screen 35.)*

**Journal / Diary (46–51) — native-integrated (Nick's call, 2026-07-24).** A diary those apps (Apple Journal / Day One references) can't build, because LifeOS has the substrate: **journals = the 14 Areas · mood→vitals · entries→Memories · prompts from agents.**
- **46 Journal · Today** — an agent prompt (Mindy asks…), a mood capture that feeds Stability/Joy, today's entries, "on this day" memory, and the mindful-minutes→Clarity note.
- **47 Journal · List** — month-grouped media cards (Apple-Journal layout) + the **List / Calendar / Media / Map** switcher.
- **48 Journal · Journals=Areas** — the Day-One journals list, but it *is* your areas (All entries · Health · Fitness · Career · … + Prompts).
- **49 Entry** — rich single entry: media, mood→vital (+Stability/+Joy), linked area/people, and "became a memory" (promoted by the dreaming cron).
- **50 New entry** — the editor: title + body, media toolbar (prompt · photo · camera · audio · location · ask-agent), and the "logging to your vitals" banner.
- **51 Calendar / Media / Map** — the other three views in one artboard.

**IA change (proposed, pending Nick's confirm before propagation):** Journal becomes a tab; **Areas folds into it** (browse-by-area = journals; area state stays on Home). Proposed tab bar **Home · Tasks · Chats · Journal · People**; **Me → top-right avatar**. Drawn on the Journal screens; NOT yet propagated to the other ~20 screens' tab bars.

**Learning / Courses (52–57) — grows Skills; own surface + in chat (Nick's call, 2026-07-24).** Reference was **Imprint** (visual micro-courses, lesson path, XP, ASK button). The key model tie: **learning is the verb for the Skills stock** — a course is a skill's path, and the node-map is the same visual grammar as Journey (Nick's "kinda reminds Journey" observation). Reached from the Skill Map (and Area knowledge, and an agent in chat). No paywall (runs on the Mac).
- **52 Learn · Browse** — categories = your areas/skills; **Made for you** (agent-generated by Mindy from your sources) + **From the library** (curated). *(sourcing = both)*
- **53 Course · Path** — the node map (done/current/locked), XP, "grows Clarity" header; finishing levels the skill.
- **54 Course · Intro** — agent-made badge, which skill it grows, the source it was built from, "no paywall — free by default".
- **55 Lesson player** — focused card + progress bar; the ASK button routes to **your agent** (Ask Mindy), not a generic AI.
- **56 Lesson in chat** — Mindy delivers the same micro-lesson inline with in-thread controls (Got it / quick check). "Same lesson, two homes."
- **57 Lesson complete → skill** — feeds the Skills stock: +XP, skill progress toward next level, learning streak, "see it on your Skill Map".

**Still pending Nick's references (not built, to avoid building wrong):**
- **Areas** — a **radial multifactorial wheel** (radar of the 14 areas) atop the Areas screen.
- **Skills** — a **huge zoomable game-map** (global, all skills at once) + a **single-skill detail** (level · area · connected knowledge). Keep the one-high-level-skill branch (screen 11).

## Open questions / risks

- **Home density** — Home now carries plan, check-in, tasks, calendar, quests, ask *and* the vitals strip. Likeliest cut: calendar → Tasks. (Owner: Nick, at mid-fi.)
- **Does People earn a daily-cadence tab?** It's the strongest available use of the slot, but if it goes untouched for weeks, Journey may deserve it instead. (Owner: Nick, after living with it.)
- ~~**Quests inside Tasks vs. inside Journey**~~ — resolved 2026-07-23, see Key Decisions.
- **Resources screen legibility** — 12 objects on one screen is the point where it can start reading as a spreadsheet, which is the original failure mode of Life Atlas. Mitigated by giving each layer a different mark (bars / tiles / outlined cards), but worth a fresh-eyes check.
- **Streaks has no screen** — it was one of the old Journey pills; Momentum now reads out on Home and in Weekly Review. Confirm that's enough before drawing one.
- **The FAB overlaps the last list row** on long screens (People, Quests). Standard iOS trade; revisit at mid-fi with a scroll-aware treatment.

## Handoff pointers

n/a — no engineering handoff at this stage. Wireframes live on the *Wirefarmes* page; the model diagram lives at `14:82`.

---

## Changelog

- 2026-07-23 — initial draft: tab restructure (Me → avatar, People → 5th tab), Tasks three-altitude sub-nav, (+) to bottom-right, full model→surface map, 6 new screens specced.
- 2026-07-23 (later) — row 4 added (19 Projects · 20 Quests · 21 Project Detail); Journey/Tasks quest duplication resolved and Journey's tabs re-cut to Map · Milestones · Chapters; three open questions updated. 21 frames now drawn.
- 2026-07-24 — row 5 started: 22 Journey → Milestones and 23 Journey → Chapters drawn, closing the two undrawn tabs the re-cut created. 23 frames now drawn.
- 2026-07-24 (later) — all screens grouped into feature **sections** (no loose frames left); added **onboarding/pairing** flow (24 Welcome · 25 Pair · 26 Connecting) and two **IA diagrams** (navigation map `87:2`, surface types `88:104`). 26 frames total.
- 2026-07-24 (later still) — added **selectors** (S1–S4: time/project/area/priority) and the **completion flow** (27 Task · 28 Quest · 29 Project · 30 Review); **retired screen 18 Rewards** per the concept-spec reward reframe. Logged the review backlog (chats/people/areas/skills).
- 2026-07-24 (batch 2) — drew 31–37: People rings + faces + Person-Detail-knowledge + Memory detail; Chats agents grid + rich thread; Area Detail knowledge (ExerciseDB). Areas radial + Skills game-map remain reference-pending.
- 2026-07-24 (batch 3) — **Settings** section (38 main · 39 Connection & Devices · 40 Check-ins & vitals · 41 Privacy & data). Clarified: cold-start sign-in = pairing screens 24–26; in-app sign-in = screen 39.
- 2026-07-24 (batch 4) — **Agents administration** (42 fleet · 43 Activity · 44 Sessions · 45 Cron), grounded in the real 18-agent roster + cron schedule.
- 2026-07-24 (batch 5) — **Journal / Diary** (46–51), native-integrated per Nick's decision. Journal proposed as a tab (Areas folds in; Me → top-right). Tab-bar propagation to other screens pending confirm.
- 2026-07-24 (batch 6) — **Learning / Courses** (52–57): own surface off Skills + in-chat delivery, both sourcing. Learning = the verb for the Skills stock; lesson→skill XP. Reorganized the whole board into 8 labeled IA tiers.
- 2026-07-24 (batch 7) — **rebuilt both IA diagrams** (`87:2` nav map, `88:104` surface types) to v2 (Journal tab, Areas folds in, Learn, Completion, Me→top-right, cross-cutting controls). Added the top-level mobile-app spec.
