# The Ring

A smart ring with always-on ambient capture and a personal context layer exposed over MCP.

## Language rules

- **NO EM DASHES.** Never use the long em dash character anywhere, in docs, code, UI copy, or generated text. Use periods, commas, colons, or parentheses to break clauses instead.
- Keep prose plain and direct. Prefer short sentences over dash-joined ones.

## One-liner

A ring that listens, turns what you say into distribution, and exposes your own context to your own AI agent over MCP.

## The one rule: data never leaves without consent

Data never leaves the app unless the user explicitly consents and grants permission. This is non-negotiable and applies everywhere.

- By default, everything (raw audio, transcripts, biometrics, motion, location, derived context) stays on-device. The cloud is never the default.
- Nothing crosses out of the app, to an AI agent, to a third-party app, or to any external destination, without an explicit user permission grant for that specific access.
- MCP is the consented door: access over MCP is allowed only after the user grants scoped, revocable permission, and only the data covered by that grant crosses. No grant, no data.
- Permissions are granular, per-destination, and revocable. Revoking a grant stops the access immediately.
- Developers and their apps never receive data except through a permission the user explicitly gave, and only the slice that permission covers.

## The differentiator: always-on listening

The core is always-on ambient listening, real-life hardware Siri. A phone app cannot do this: no app is allowed to constantly record in the background; only the OS-level assistant can, and it does not hand that capability to developers. A ring with its own mic can.

Existing smart rings have no microphone. The ones that market "voice assistance" route it through the phone app, not the ring itself. So this ring is the first to put always-on capture on the finger.

The ring captures the wearer's own narration, the ~1m mouth-to-ring near field. Capture is wearer-only: there is no speaker separation (diarization), so what gets captured is what *you* say, not the people around you. A double-tap marks intentional capture, so the wearer is the speaker by construction.

## Capture turns into distribution

Capture alone is just another notes graveyard. The point is distribution: what you say gets routed to where it creates value instead of sitting in an inbox.

A single narrated thought becomes:

- a tweet or thread, drafted in your voice
- a changelog entry or release note
- a feature spec or ticket dropped into your tracker
- a blog draft skeleton
- a TODO scoped to the right project
- a reply to a user you've been meaning to get back to

The pitch is not "record your ideas." It's "say it once, and it shows up everywhere it should be."

## The context layer over MCP

The ring fuses passive biometrics, motion, location, and intentional voice, unified on-device and exposed over MCP. That makes it a personal context platform.

Point your own AI agent at it and the agent has real context: your captured ideas, your health and activity signals, where you are, and what you actually spend time on. Instead of re-explaining your context every session, the agent already knows.

For someone running several apps solo, this is the unlock: the agent already knows your projects, your metrics, your backlog, and your voice.

## Hardware specs (v1)

The current ring hardware is deliberately minimal:

| Capability | Component |
|---|---|
| Voice capture | microphone |
| Stream to phone | over Bluetooth (BLE) |
| HR / HRV / SpO₂ | one optical PPG sensor |
| Skin temp | thermistor |
| Motion + intentional trigger | accelerometer (double-tap gesture) |
| Output to wearer | haptic buzz |

Notable decisions:
- **No indicator LED.** The ring signals state to the *wearer* via haptics only; there is no visual capture light for bystanders. Bystander honesty is handled in software/policy, not hardware.
- **Double-tap is the intentional trigger.** The accelerometer detects a double-tap to mark/confirm intentional capture (vs. passive ambient listening).
- **Location is not on-ring.** There is no GPS in the ring; location/place context is sourced from the paired phone, then fused into the context layer.
- **One PPG sensor** covers HR, HRV, and SpO₂; skin temp is a separate thermistor.

## The marketplace

The context layer is open. Developers build on the exposed context through MCP, so the ring is a platform others ship on, not just a single app. Shape: an open, local-first, sensor-fusion context platform with a developer marketplace on top.

This is a **day-one pillar, not a someday feature.** We attack both sides at the same time: a first-party product that is great on its own, and a marketplace where third-party apps become additional reasons to buy (the way Spotify and Instagram became reasons to own a phone). The marketplace launches with two tracks: a few curated flagship apps we co-build or fund so the store is never empty, plus an open self-serve marketplace any developer can publish to. We stay a platform without becoming a commodity by keeping the product proprietary (hardware, firmware, capture pipeline, first-party app) and exposing only the MCP interface: open platform, closed product. See `flagship-apps.md` for the launch flagship apps, `marketplacearchitecture.md` for the SDK and per-user data isolation, and `developer-experience.md` for the least-friction developer path.

## Where this sits against everything else

Always-on ambient capture on a wearable already exists, the Limitless Pendant does it, so this isn't the first attempt at the category. The angle is doing it on a ring, combined with health sensors and an open MCP marketplace. Nobody is combining those three.
