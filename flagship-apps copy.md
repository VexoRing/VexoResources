# The Ring — Launch Flagship Apps

Three curated, co-built/funded third-party apps that ship at or near launch. Their job: be reasons to buy the ring (the Spotify-on-iPhone effect) and prove the platform is real on day one, so the marketplace is never empty. See the marketplace section of `CLAUDE.md` for how flagships fit the two-sided launch and `marketplacearchitecture.md` for the SDK and per-user isolation.

## The bar each one passes

1. **Felt desire** — a user seeks it out because it scratches a real itch, not because it is clever.
2. **Only-here novelty** — impossible or much worse on a phone, because it needs always-on capture of the wearer's own voice and/or biometrics on the same device.
3. **Wearer-only fit** — works on what *you* say (no diarization), which is exactly what the ring captures.
4. **Reason-to-buy** — someone would buy the ring partly for this.
5. **Privacy-native** — intimate enough that "data never leaves your device, developers never see it" is a feature, not a limitation.

These three hit three distinct desires: be reliable, understand yourself, be more impressive.

---

## 1. Kept — the promise keeper

**What it is.** It quietly catches the commitments you make out loud all day ("I'll send you that doc," "I'll call my mom this weekend," "let's grab coffee next week," "I'll get back to you on pricing") and tracks whether you actually followed through. Not a to-do app you type into. A net under everything you say.

**The want.** Everyone is quietly ashamed of the balls they drop and the "I'll get back to you"s that vanish. People want to be someone whose word is good. The pitch sells itself: never break a promise you forgot you made.

**Why only here.** A phone cannot hear you say it. The value is passive capture of spoken commitments in real life, which is exactly always-on wearer voice. Double-tap can confirm "log that one," but mostly it just listens.

**Pull not push.** Works ambiently and surfaces a short "you said you'd..." list when you want it. A safety net, not a nag.

**SDK scopes.** `captures:search`, `captures:read`, `events:subscribe` (on `capture.created`). On-device, no developer egress.

**Partner brief.** Build the commitment-extraction model (detect a spoken promise, who it is to, by when), a lightweight follow-through tracker, and a gentle daily/weekly review surface. Optional: tie a kept/dropped commitment back to the relevant person or project in the context layer.

---

## 2. Undercurrent — your body's read on your life

**What it is.** It fuses *what you talk about* with *how your body responds* (HRV, heart rate, skin temp) and reveals patterns you cannot see yourself: "Your HRV drops every time you talk about the co-founder situation." "You light up, physiologically, when you talk about the hardware, not the fundraising." "The days you mention your sister, your stress markers are lower."

**The want.** People are insatiable about understanding themselves and usually cannot tell what is actually draining or energizing them. This is a mirror they have never had: their own body's honest verdict on the people, topics, and decisions in their life.

**Why only here.** The most defensible app on the platform. It requires voice and biometrics fused on one always-on device worn continuously. No phone, watch, or journaling app can do it, because nothing else has your words and your physiology in the same place at the same time. This is the flagship that proves the sensor-fusion thesis.

**Pull not push.** Delivered as a weekly "here is what your body has been telling you" reveal. A discovery, not an alert stream.

**Headliner.** If one app makes someone say "wait, it can do that?", it is this one.

**SDK scopes.** `captures:search`, `context:projects`, `biometrics:history`, `biometrics:latest`, `events:subscribe`. On-device, no developer egress.

**Partner brief.** Build the topic/entity tagging over captures, the time-aligned correlation engine against biometric series, and the weekly insight reveal. The hard, valuable work is honest correlation (avoiding spurious patterns) and a calm, non-alarmist presentation.

---

## 3. Cadence — the speech coach for real life

**What it is.** It coaches how you actually speak, drawn from your real days rather than practice sessions: filler words ("um," "like," "you know"), pace, hedging ("I just think maybe..."), vocabulary, clarity, and how you sound when nervous versus confident. It shows trends and gives you one thing to work on at a time.

**The want.** How you talk is career and social currency, and almost everyone wants to sound sharper, calmer, more confident. Public-speaking anxiety, non-native speakers, salespeople, founders pitching. Today people pay coaches or use practice apps that do not reflect real life. This coaches the speech that actually happens.

**Why only here.** Practice-app coaching is fake because it is not how you really talk. The unlock is passive coaching on genuine everyday speech, which requires always-on wearer capture. A phone cannot sit in your real conversations.

**Pull not push.** You opt into "I want to speak better," and it gives gentle, periodic, private feedback. Nothing is broadcast; it is a coach in your corner.

**SDK scopes.** `captures:read`, `captures:search`, `events:subscribe`. On-device, no developer egress. (Benefits from access to speech-quality signals beyond the transcript, e.g. pace and disfluency markers; if those are not already derived on-device, add a `speech:prosody` scope.)

**Partner brief.** Build the disfluency/pace/hedging detectors, vocabulary and clarity scoring, trend tracking, and a "one focus at a time" coaching loop. Optional: pre-event warmups and post-event debriefs.

---

## Why this trio together

- Three distinct, powerful desires: **be reliable** (Kept), **understand yourself** (Undercurrent), **be more impressive** (Cadence). Different buyers each find a reason.
- Every one is **uniquely enabled by the hardware** and **works on wearer-only capture**, so they are not features bolted onto a generic recorder.
- All three are intimate, so the "data never leaves the device, developers never see it" architecture is a selling point. The privacy model and the flagships reinforce each other.
- None is "look at this novel thing." Each is "I want to be the person who keeps their word / knows themselves / speaks well." That is pull.

## Why these are third-party flagships, not first-party

Each is a deep vertical with its own expertise (behavioral nudging, psychophysiology, speech and linguistics) that benefits from a dedicated team obsessing over it, while the first-party app stays focused on the core capture → distribution loop. Funding or co-building these proves the platform without diluting first-party focus.

## Common platform notes

- All three run **on-device in the sandbox** with **no developer egress**, consistent with the rule in `CLAUDE.md` that data never leaves without explicit user consent.
- All three rely only on the **wearer's own voice** (plus the wearer's biometrics for Undercurrent), which is a strong signal they fit the hardware rather than fighting it.
- Each becomes available only after the user installs it and grants the listed scopes; scopes are granular and revocable.
