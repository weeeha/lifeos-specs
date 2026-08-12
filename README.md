# LifeOS — design specifications

Two working design specs from **LifeOS**, an independent personal life-management system I have been designing and building for my own use since April 2026.

Published here as a public, dated record of the work, and because they are the two documents I would most want another designer to read.

| Document | Date | What it is |
|---|---|---|
| [IA and surface map](2026-07-23-lifeos-ia-and-surfaces-spec.md) | 2026-07-23 | Collapsing a 12-object economy model and 5 entity types into a navigable iOS app: five tabs, one avatar, one capture button, three overlays. Includes the full model-to-surface map and 57 specced screens. |
| [Visual language](2026-07-26-lifeos-visual-language-spec.md) | 2026-07-26 | "The Field Notebook." How to make an app warm enough to open on a bad day and honest enough that a bad day looks bad, resolved structurally rather than by good intentions. Measured WCAG AA contrast, light and dark. |

## The system these describe

LifeOS models a life as a small economy rather than a pile of features: **5 vitals** (Energy, Clarity, Willpower, Stability, Inspiration), **3 stocks** (Experience, Skills, Money), **4 readouts** (Joy, Confidence, Momentum, Social Support), and **5 entity types** (Areas, People, Tasks/Projects/Quests, Skills, Journey nodes). State is inferred from real signals rather than typed in by hand.

## Three ideas in here worth stealing

**A model object with no surface is a model object that will quietly stop being true.** The IA spec's surface map exists to enforce this: every object in the model gets exactly one primary home, and a row with no surface is a row that is already fiction.

**Colour is not a judgment channel.** A low reading is *short*, not *red*. Length, position and elapsed time carry the truth; colour carries nothing about it, and one reserved accent marks only the next small action. So the single coloured thing on any screen is the way up, never the alarm.

**Never score a person.** No "relationship health 62%". Ring, last contact, and your own words. Every other guardrail in the system protects the user from gaming their own metrics; this one protects the people around them.

## Status

Working documents, not polished artefacts. They carry their own changelogs, open questions and unresolved risks, which is the point of publishing them as they are.

Related: the earlier web MVP that preceded this, **Life Atlas**, is live at [life-atlas-visualiser.vercel.app](https://life-atlas-visualiser.vercel.app). Its fatal flaw was manual data entry, a vision board that yellows. Making state signal-inferred is the thing LifeOS exists to fix.

---

Nick Vyhouski · [vyhouski.com](https://vyhouski.com) · [github.com/weeeha](https://github.com/weeeha)

These documents are published for reading and reference. LifeOS, its architecture, and all derivatives remain the property of the author.
