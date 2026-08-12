# LifeOS iOS — Visual Language — Design Spec

> **Provenance.** Authored by Nick Vyhouski as part of **LifeOS**, an independent
> personal life-management system he has designed and built for his own use since
> **April 2026**. This document is published unmodified in substance from the original
> dated working spec held in a private version-controlled repository
> (`weeeha/LifeOS`, initial commit 2026-04-25). Only private links, internal
> cross-references, and file paths have been removed. Published 2026-08-11.
>
> LifeOS and all derivatives of it remain the property of the author.

---


**Date:** 2026-07-26
**Owner:** Nick
**Status:** Approved (direction + ground + type). Marks, game surfaces, and motion are open.
**Related:** IA & surface map · mobile app spec · Life Game concept · M3 walking skeleton

## Problem

Every prior spec deferred visual language on purpose — the wireframes are low-fi grayscale "by explicit choice," and M3 ships raw SwiftUI defaults. That was correct while the IA was moving. It isn't anymore: 57 screens are specced, the tab structure is settled, and the app is about to be built for daily use.

The deferral now costs something specific. LifeOS has an unusual pair of requirements that most apps never have to reconcile: it must be **warm enough to open on a bad day**, and **honest enough that a bad day looks bad**. Those pull in opposite directions, and the direction they get resolved in is decided by pixels, not prose. Without a committed language, the resolution happens accidentally — one encouraging color at a time — and lands on the dopamine pattern the concept spec explicitly forbids.

## Users & JTBD

- **Primary user:** Nick. Single-player, personal. iOS, one-handed, in-the-moment, frequently at night.
- **Job to be done:** *"Show me an honest picture of where my life is — and don't make me dread looking."*
- **The load-bearing moment:** a bad week. Vitals near the floor, quests stalled. Everything below is designed against that screen, not against the good-day screen.

## Approach

**The Field Notebook.** The app's surface is a personal record that happens to be alive: a warm paper ground, ink-weight marks, scarce color. Warmth is carried by *material* — the way a well-made notebook feels warm without being colorful — rather than by encouragement, celebration, or saturation.

The direction is defined by three rules, which matter more than the specific hues. Each exists to make the honesty structural rather than a promise to behave well:

**1. Warmth and honesty are carried by different elements.** The paper is warm; the ink is not. The app can be kind in its ground and its voice while the reading stays a plain mark. If warmth ever needs to increase, it increases in the paper — the data does not move.

**2. Color is not a judgment channel.** A low vital is *short*, not *red*. Nothing changes color because a reading is bad. Length, position, and elapsed time carry the truth; color carries nothing about it.

**3. There is exactly one accent, reserved for the handhold.** The sanguine mark appears only on the next small action. The single colored thing on any screen is therefore *the way up* — never the alarm. Scarcity is the mechanism: an accent that also marked errors, overdue items, and streaks would mean nothing within a week.

Dark mode is not inverted paper — it is the same page with the lamp off. Warm dark board, chalk-light ink, identical hue family, luminance flipped. Never the blue-black most apps default to, because blue-black is a different material and the app would feel like it changed identity at night.

### Alternatives considered

**Register** (how the app feels on a bad day):
- *Instrument* — clean, quiet, no editorializing. Rejected: does very little of the "motivate" half of the stated job.
- *Companion — plain reading, then a way up* — **chosen.**
- *Modulating* — presentation shifts with mood. Rejected: an app with moods is an app whose data you eventually read *through* the mood.

**Platform stance:**
- *Native, dressed* — system everything plus color and a few custom pieces. Viable, less distinct.
- *Custom skin* — own type, own controls. Rejected: roughly a 3–4× multiplier per screen for a solo builder, and re-implements accessibility, Dynamic Type, and dark mode by hand.
- *Native shell, custom heart* — **chosen.** Utility surfaces stay genuinely native; hand-built pixels concentrate in the game surfaces behind the avatar.

**Ground:**
- *The Field Notebook* — **chosen.**
- *Living Light* — iOS materials with an ambient layer carrying state. Rejected: cheapest to build and the least distinct, and ambient state-coloring reintroduces the rejected "app has moods" pattern as atmosphere.
- *The Creature* — the avatar is the interface; vitals read off a rendered being's posture. Rejected: the reading and the emotional editorial become the same pixels, which is precisely the failure mode being designed against. Also the most expensive.

## The system

### Palette

| Role | Light — *the page* | Dark — *lamp off* |
|---|---|---|
| Ground | `#F4EFE6` paper | `#1A1613` board |
| Raised surface | `#EFE8DA` | `#221D19` |
| Ink (primary text, marks) | `#241F19` | `#E8E0D2` chalk |
| Faded ink (secondary) | `#6B6157` | `#A0968A` |
| Rule (dividers, tracks) | `#DDD4C4` | `#3A332C` |
| Sanguine (accent — handhold only) | `#B4472E` | `#D97757` |

Measured contrast against the respective ground: ink **14.3:1** light / **13.7:1** dark; faded ink **5.3:1** / **6.2:1**; sanguine **4.7:1** / **5.8:1**. All clear WCAG AA for normal text. Note the light sanguine at 4.7:1 has little headroom — it must not be lightened further.

### Type

Both faces ship with iOS, so the serif costs nothing and Dynamic Type comes free.

**The rule: serif is language, sans is anything measured or tappable.**

- **New York** — the app's sentences, journal body, chapter and milestone names. What the app observes and what you write.
- **SF Pro** — numerals, row labels, section labels, navigation, controls, actions. Neutral on purpose.

This is the same enforcement trick as the color rule: the emotional register lives entirely in the serif and every number lives in a neutral face, so warmth cannot leak into a reading — the two are set in different typefaces.

Two consequences worth stating explicitly:
- **The handhold is sans, not serif.** It is an offer, not an observation, so it is typeset as a control and always reads as something that can be ignored. The app's voice never issues instructions.
- **Numerals use tabular figures.** They align down a list and do not jitter on update.

## Key design decisions

- **Decision:** Companion register, not instrument. — **Why:** "mirror + motivate" is the stated job and an instrument does only the first half. — **Alternatives:** instrument; a split between sober utility and warm game surfaces.
- **Decision:** A bad reading is stated plainly, then paired with one next small action. — **Why:** honesty is non-negotiable, but a reading with no handhold does no motivating. — **Constraint this creates:** the handhold may never change the reading, only sit beside it.
- **Decision:** Native shell, custom heart. — **Why:** ~57 screens, one builder; custom controls in SwiftUI are where solo projects die. Hand-built pixels are spent only where they earn it (Journey map, Skills tree). — **Alternatives:** fully native; fully custom.
- **Decision:** Warmth in the ground, honesty in the ink — enforced by using different elements and different typefaces for each. — **Why:** rules that depend on restraint erode as screens are added; rules enforced by structure do not.
- **Decision:** One accent, reserved for the handhold. — **Why:** makes the only colored thing on screen the way forward. — **Cost, accepted:** no color remains for errors, offline, or overdue states; those must be expressed in type, position, or copy.
- **Decision:** Journal entries are set in the same serif as the app's own sentences, separated by attribution and position rather than by typeface. — **Why:** one shared notebook. — **Status:** taken as a default, not strongly held; revisit after real entries exist.

## Constraints

- **Platform:** iOS 17+, SwiftUI. One-handed target. Frequent night use.
- **System:** native components (Lists, sheets, system nav) on utility surfaces; custom rendering only behind the avatar.
- **Technical:** offline is a normal state, not an error — the gateway lives on a Mac that sleeps.
- **Team:** one person plus an agent. Cost per screen is a first-class design constraint.

## Success criteria

- A bad week is legible as a bad week at a glance, with no color having been used to say so.
- The app is comfortable to open at 11pm without the ground changing character.
- A new screen can be built by following the rules above without a new color or typeface being invented.
- Nothing in the interface flatters, celebrates, or rounds a reading up.

## Out of scope

- ~~Marks~~ — vitals resolved 2026-07-31 (see Open questions). Stocks and readouts are
  still undrawn, and should follow the vital mark's shape rather than invent their own.
- The custom heart — Journey map and Skills tree rendering (both still awaiting reference images).
- Motion and transitions.
- Avatar form (literal / archetype / spirit-creature) — still open from the concept spec.
- Iconography beyond SF Symbols.
- Application to the existing wireframe set; the ~20 stale tab bars are a separate cleanup.

## Open questions / risks

- ~~**Marks are undecided**~~ — **resolved 2026-07-31.** A vital reads as **level + elapsed
  time**: a seven-day trace whose ink thins toward the past, a filled dot for today, and a
  sans elapsed stamp (`2d`, `today`) at the right. Three candidates were built and compared
  on device; the ruled line and the five-spoke dial were deleted, the ruled line's elapsed
  stamp kept. See `LifeOSDesign/Components/VitalMark.swift` for the treatment and the two
  rejections. The dial's failure is worth remembering: one radius carrying both level and
  recency made figure *size* track recency, so a week of 10% vitals fed today drew large —
  a reading that looked precise and wasn't. Color is not the only channel that can
  editorialize; any single channel asked to carry two variables will.
- **No color left for system states.** Offline, stale, failed-send, and overdue all need a non-color expression. The M3 app already has connection banners that will violate this on contact. — *Owner: next session, before M4.*
- **Paper can go twee.** The line between "warm material" and "skeuomorphic 2011" is not written down anywhere in this spec, and will be found by drawing, not by rule.
- **Serif at small sizes on-device is unverified.** New York's readability in dense list contexts has not been checked on a real screen.
- **Avatar form is still open** and the concept spec says it "affects the whole visual tone." This spec is deliberately compatible with all three answers, but that cannot last.
- **Nothing here has been rendered in SwiftUI.** The palette and type pairing have been checked in a browser mockup only.

## Handoff pointers

- No Figma frames yet — the direction was agreed in conversation and validated against two browser mockups (palette in both modes; type specimen).
- Accessibility: contrast measured and recorded above. Dynamic Type is inherited from both system faces; tabular figures required for all numerals.
- Implementation note: the palette should land as a single semantic color set (ground / raised / ink / faded / rule / accent) with light and dark values, so no screen ever names a hex.

---

## Changelog
- 2026-07-26 — initial spec. Direction, ground, and type approved in session; marks, game surfaces, and motion deferred.
- 2026-07-31 — **marks resolved for vitals**: the decay trace + elapsed stamp, chosen by
  rendering three candidates on device in both schemes and looking (brainstorm → three
  options → build → compare). Shipped as `VitalMark`; the two rejected treatments were
  deleted rather than kept, following `StateNote`'s precedent. Two things the render
  taught that prose had not: a 30pt trace cannot separate 0.09 from 0.22 (44pt is a
  floor, not a preference), and a single geometric channel carrying two variables
  editorializes exactly the way color would. Stocks and readouts remain undrawn.
