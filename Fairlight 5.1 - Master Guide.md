# Fairlight 5.1 — Master Guide

*The complete written version of the interactive routing map (`map.html`), for reading, printing and Obsidian linking. Written for someone new to audio mixing.*

*Updated 2026-07-04 · verified against **DaVinci Resolve Studio 21.0.2** (FlexBus). Acronyms are explained in [[Fairlight 5.1 - Glossary]].*

---

## 1. New to mixing? Start here

This whole template is a **river system**. Your audio clips sit on **tracks** (the lanes of the timeline). Each track flows into a **stem** — a submix that gathers one category together: all the talking in one place (DX), all the sound effects in another (FX), all the music in a third (MX). The stems then flow into the **Print Master** — the finished mix you actually listen to and export.

Why bother with the middle layer?

- **Control:** one fader turns all dialogue up or down at once.
- **Deliverables:** broadcasters want the mix *and* the separated stems as files, so the programme can be re-edited or dubbed later.
- **The M&E:** a version of the mix with no dialogue, needed so foreign broadcasters can dub in their own language. It's built automatically from the FX and MX stems.

Riding alongside the river: **VCAs** (remote-control volume knobs that move several faders at once — no audio flows through them), **reverb buses** (shared echo machines many tracks can borrow), and **LFE buses** (collectors for deep bass that feed the subwoofer).

Signal flow in one line:

```
SOURCE TRACKS → STEMS (submixes) → PRINT MASTERS (final mixes) → monitoring / delivery
                  ↑                     ↓
            reverbs (aux)          Webmix (compressed stereo)
```

---

## 2. Resolve 21 version notes (read once)

**Bussing changed in v17 — "Main / Sub / Aux" are roles, not bus types.** Modern Resolve uses **FlexBus**: every bus is created the same way (`Fairlight ▸ Bus Format ▸ Add Bus` — set name, format, colour) and its role comes from routing:

- **"Sub" (stems):** a bus that track *Bus Outputs* feed into.
- **"Aux" (reverbs):** a bus reached only via *Bus Sends*; its own output returns to a stem.
- **"Main" (print masters):** the last bus in the chain, monitored and delivered.

FlexBus limits: a track can output to up to **10 buses** and send to **10 more**; buses can feed other buses up to **6 layers deep**. Legacy fixed bussing still exists (Project Settings ▸ Fairlight ▸ "Use fixed bus mapping", new empty projects only, one-way conversion back) — don't use it for new work.

**VCAs:** up to 16 groups via `Fairlight ▸ VCA Assign`; masters appear to the right of the buses in the Mixer.

**Free vs Studio:** buses, VCAs, 5.1, FairlightFX and loudness metering all work in the free version. Studio adds immersive formats (5.1.2–9.1.6 / Atmos — Preferences ▸ Video and Audio I/O ▸ Immersive Audio), Dolby Digital encoding, and the AI voice tools.

**New since the original spec:** v20 — AI Audio Assistant (auto first-pass mix; fine for temp mixes, not a replacement for this routing), AI Dialogue Separator & Matcher, Voice Isolation, Cut-page mixer with loudness metering. v21 — audio **track folders** (collapse the 11 source tracks into Dial/FX/Amb/Mus groups), 6-band Clip EQ, **Chain FX** presets, EQ Match / Level Matcher, new Fairlight Audio Core. 21.0.1/21.0.2 are maintenance releases.

**Export:** 48 kHz / 24-bit; 5.1 SMPTE channel order **L R C LFE Ls Rs**.

---

## 3. The elements, one by one

### 3.1 Source tracks (11)

**In plain English:** a track is a lane in the timeline where you drop audio clips. Everything placed on the lane flows wherever the lane's output points — into its family's stem.

| # | Track | Width | Colour | Outputs to | Pan | Reverb sends (at −∞) | LFE send | VCA |
|---|-------|-------|--------|-----------|-----|----------------------|----------|-----|
| 1 | Narration / VO | Mono | Blue | DX Stem + Stereo DX Stem | Hard Centre | **none — keep dry** | — | Dialogue |
| 2 | DX (Dialogue) | Mono | Blue | DX Stem + Stereo DX Stem | Hard Centre | DX Verb Mono/Stereo/5.0 | — | Dialogue |
| 3 | Futz | Mono | Blue | DX Stem + Stereo DX Stem | Hard Centre | none (futz FX on clips) | — | Dialogue |
| 4 | PFX | Mono | Blue | DX Stem + Stereo DX Stem | Centre | DX Verb Stereo | — | Dialogue |
| 5 | FX A | Mono | Orange | FX Stem + Stereo FX Stem | L/R/Ls/Rs, Centre clear | FX Verb Mono/5.0 | FX LFE Bus | FX |
| 6 | FX B | Mono | Orange | FX Stem + Stereo FX Stem | L/R/Ls/Rs | add per project | FX LFE Bus | FX |
| 7 | FX C | Stereo | Orange | FX Stem + Stereo FX Stem | fronts, spread | FX Verb Stereo | FX LFE Bus | FX |
| 8 | Ambience A | Mono | Green | FX Stem + Stereo FX Stem | wide into Ls/Rs | — | — | Ambience |
| 9 | Ambience B | Stereo | Green | FX Stem + Stereo FX Stem | wide into Ls/Rs | — | — | Ambience |
| 10 | Music (Stereo) | Stereo | Purple | MX Stem + Stereo MX Stem | L/R fronts | MX Verb Stereo | Music LFE Bus | Music |
| 11 | Music (5.1) | 5.1 | Purple | MX Stem + Stereo MX Stem | discrete pass-through | MX Verb 5.0 | Music LFE Bus | Music |

**How to build any track (Resolve 21):**

1. **Create:** right-click a track header ▸ Add Track ▸ pick the width (Mono/Stereo/5.1). Double-click the name to rename; right-click ▸ Change Track Color.
2. **Outputs:** Mixer ▸ the strip's **Bus Outputs ▸ +** ▸ pick the 5.1 stem, then **+** again ▸ the stereo stem. Bulk: select several tracks, hold Alt/Option, click +.
3. **Pan:** double-click the pan pot to open the surround panner; place per the table.
4. **Sends:** Mixer ▸ **Bus Sends ▸ +** ▸ pick the reverb/LFE bus. Leave at −∞ in the template.
5. **VCA:** `Fairlight ▸ VCA Assign` ▸ add the track to its group.

Track-specific notes:

- **Narration/VO** carries an information piece — its own fader, a de-esser + light compression, and no reverb. Streaming loudness is dialog-gated, so this track largely decides whether you pass the −27 LKFS check.
- **Dialogue lives hard Centre** — it stays anchored to the screen for every seat and folds down predictably.
- **Futz** = deliberately degraded voice. Do the degradation with clip FX (band-pass ~300 Hz–3 kHz + distortion); v21's 6-band Clip EQ makes this easy per clip.
- **PFX** stays with dialogue because it shares the recording acoustics; the dub replaces it from library FX.
- **Ambience folds into the FX stem** — standard for backgrounds and M&E. Need a separate BG deliverable? Add a BG Stem later; the structure supports it.
- **Music (5.1)** passes channel-for-channel; its LFE send exists for reinforcing stereo-sourced cues.

### 3.2 VCAs (4) — Dialogue, FX, Ambience, Music

**In plain English:** a remote-control volume knob. Pull it down and every member track turns down together, keeping their relative balance. No sound travels through it.

**Build:** `Fairlight ▸ VCA Assign` ▸ create and name each group ▸ tick member tracks (see table above). Masters appear right of the buses in the Mixer. Members keep their own routing regardless.

**Why:** one-fader control of a whole section *without* collapsing it to a bus — per-track automation, panning and stem routing stay untouched. This is your top-level balance layer.

### 3.3 Reverb buses (8, "aux" role)

**In plain English:** a shared echo machine. Tracks tip a little of their sound in (a "send"); it comes out wet and echoey and is added back into the submix (the "return"). One reverb serves many tracks, each at its own amount.

| Bus | Format | Returns into | Preset guide |
|-----|--------|--------------|--------------|
| DX Verb Mono | Mono | DX Stem | small room / plate |
| DX Verb Stereo | Stereo | DX Stem | room / plate |
| DX Verb 5.0 | 5.0 | DX Stem | hall / large space |
| FX Verb Mono | Mono | FX Stem | small room |
| FX Verb Stereo | Stereo | FX Stem | room / chamber |
| FX Verb 5.0 | 5.0 | FX Stem | hall / exterior |
| MX Verb Stereo | Stereo | MX Stem | plate / hall |
| MX Verb 5.0 | 5.0 | MX Stem | scoring stage / hall |

**Build each:** `Fairlight ▸ Bus Format ▸ Add Bus` ▸ name + format ▸ Mixer ▸ Effects slot ▸ **+ ▸ FairlightFX ▸ Reverb** (100% wet — the dry path already goes to the stem) ▸ **Bus Outputs ▸ +** ▸ its stem. Feed it **only via Bus Sends** — never a track's main output.

**Why:** returning the verb into the matching stem keeps wet signal inside the correct deliverable — dialogue tails can never pollute the M&E. 5.0 (not 5.1) keeps reverb out of the subwoofer.

### 3.4 LFE buses (2)

**In plain English:** a collector for deep bass. Tracks tip low rumble in here, a filter keeps only the sub-bass, and the result feeds the subwoofer (.1) channel — so *you* decide what shakes the room, not the playback system's bass management.

**Build:** `Bus Format ▸ Add Bus` ▸ Mono ▸ insert a **low-pass filter ~120 Hz** ▸ **Bus Outputs ▸ +** ▸ the 5.1 stem, then open the bus's output surround panner and steer **100% to the LFE channel** (zero to the mains). Fed by Bus Sends from FX A/B/C (FX LFE Bus) and the Music tracks (Music LFE Bus).

### 3.5 Stems (8, "sub" role)

**In plain English:** a stem is a submix — all of one category gathered in one place with one master fader. Stems are also exported as separate files so the mix can be taken apart and re-versioned later.

| Stem | Format | Fed by | Outputs to |
|------|--------|--------|-----------|
| DX Stem | 5.1 | VO/DX/Futz/PFX + DX verbs | 5.1 Print Master |
| FX Stem | 5.1 | FX + Ambience + FX verbs + FX LFE | 5.1 Print Master **and** M&E Stem |
| MX Stem | 5.1 | Music + MX verbs + Music LFE | 5.1 Print Master **and** M&E Stem |
| M&E Stem | 5.1 | FX Stem + MX Stem | **nothing — deliverable only** |
| Stereo DX Stem | Stereo | dialogue tracks (2nd output) | Stereo Print Master |
| Stereo FX Stem | Stereo | FX + Ambience (2nd output) | Stereo Print Master **and** Stereo M&E |
| Stereo MX Stem | Stereo | music tracks (2nd output) | Stereo Print Master **and** Stereo M&E |
| Stereo M&E Stem | Stereo | Stereo FX + Stereo MX | **nothing — deliverable only** |

**Build each:** `Bus Format ▸ Add Bus` ▸ name/format/colour ▸ `Fairlight ▸ Bus Assign` (or Mixer Bus Outputs +) ▸ route per the table. A bus can feed several buses at once, up to 6 layers deep.

**Why M&E is fed from stems, not tracks:** it guarantees M&E always equals FX + Music + Ambience with zero per-track bookkeeping. Change an FX level and both the mix and the M&E follow automatically. Leave the M&E buses' outputs **unassigned**.

### 3.6 Print Masters (2) and Webmix

**In plain English:** the finished mix — every stem summed. This is what you listen to while mixing, what the loudness meters judge, and what gets exported. The Webmix is a louder, squashed copy of the stereo mix for the internet.

**5.1 Print Master** (5.1): fed by DX/FX/MX stems.
- **Monitor it:** monitoring panel (top-left of the Fairlight page) ▸ set the Control Room source to this bus. Speakers: Preferences ▸ Video and Audio I/O.
- **Loudness:** the monitoring-panel meters measure the monitored bus — pick your standard in the meter options (blue = in spec, yellow = tolerance, red = over). Switch to **dialog-gated** for the streaming check. Right-click any clip ▸ Analyze Audio Level for an offline read.
- **Deliver:** 6-channel WAV 48 kHz/24-bit (L R C LFE Ls Rs), or Dolby Digital (Studio).

**Stereo Print Master** (Stereo): fed by the three stereo stems; its output also feeds the Webmix.
- Set the downmix flavour your broadcaster requires: **Lt/Rt** (matrix, most broadcasters) or **Lo/Ro** — check the delivery spec.
- Meter it separately from the 5.1 — both must pass their own target.

**Webmix Stereo:** insert **Compressor** (~3:1) then **Limiter** (ceiling −1.0 dBTP) — save both as one **Chain FX** preset (v21). Target ≈ **−14 LUFS**. Deliver as AAC/MP3 for online review and social.

---

## 4. The routes, explained

Every line on the map is one of these eight connection types:

**Track output → bus.** The track's post-fader, post-pan signal is mixed into the bus — the primary path from a lane into its stem. *Create:* Mixer ▸ Bus Outputs ▸ + (Alt/Option-click for many tracks at once) or `Fairlight ▸ Bus Assign`.

**Bus Send → reverb (aux send).** A copy of the sound is siphoned to the echo machine; the original keeps flowing unaffected. *Create:* Mixer ▸ Bus Sends ▸ + ▸ the verb bus; right-click the send for pre/post-fader (post is typical). Template default: −∞.

**Reverb return → stem.** The echo joins the group mix, so the echo of dialogue always lives with the dialogue. *Create:* the verb bus's own Bus Outputs ▸ + ▸ the stem.

**LFE send → LFE bus.** Some of the track's deep bass is siphoned to the bass collector. *Create:* Bus Sends ▸ + ▸ the LFE bus; filtering happens once, on the bus.

**LFE bus → stem's LFE channel.** The collected, filtered bass is poured into the subwoofer channel. *Create:* Bus Outputs ▸ + ▸ the stem, then pan the bus's output 100% to LFE.

**VCA assignment (control only).** No sound — a volume remote-control link. *Create:* `Fairlight ▸ VCA Assign` or the Mixer Group dropdown.

**Stem → M&E.** The effects/music group is also copied into the "no dialogue" version, automatically. *Create:* Bus Assign ▸ the stem's Out ▸ also tick M&E.

**Bus → master chain.** The group mix is poured into the final mix (stems → print masters; Stereo PM → Webmix). *Create:* Bus Assign or Bus Outputs ▸ +.

---

## 5. Build order — quick checklist

1. **Project:** new project; Project Settings ▸ Fairlight ▸ 48 kHz; leave "Use fixed bus mapping" **off**.
2. **Buses first** (`Fairlight ▸ Bus Format`, **×21**), setting the **Format** on each — this is where mono/stereo/5.1 is decided: 3 masters (5.1 PM = **5.1**; Stereo PM + Webmix = **Stereo**), 4 stems = **5.1**, 4 stereo stems = **Stereo**, 2 LFE buses = **Mono**, 8 reverb buses = **Mono/Stereo/5.0** per §3.3. Exact names matter — they appear in every routing menu.
3. **Bus-to-bus routing** (`Fairlight ▸ Bus Assign`): stems → masters; FX/MX → M&E too; LFE buses → stems (panned to LFE); verbs → stems; Stereo PM → Webmix; M&E outputs unassigned.
4. **Tracks:** the 11 lanes, correct widths, renamed, colour-coded (v21: group into track folders).
5. **Track outputs:** each track → its 5.1 stem **and** stereo stem.
6. **Panning:** dialogue Centre; FX across the field; ambience into surrounds; music L/R or discrete.
7. **LFE sends:** FX + Music tracks → LFE buses; low-pass ~120 Hz on each bus.
8. **Reverbs:** FairlightFX Reverb on each verb bus; sends pre-routed at −∞.
9. **VCAs:** 4 groups via VCA Assign.
10. **Monitoring + meters:** monitor the 5.1 PM; loudness meters set to your standard; dialog-gated for streaming checks.
11. **Webmix:** Compressor + Limiter (Chain FX preset), ≈ −14 LUFS / −1 dBTP.
12. **Save:** `File ▸ Export Project` (.drp) — this is the reusable template.

---

## 6. Delivery targets & export

| Deliverable | Integrated loudness | True peak | Measurement |
|---|---|---|---|
| US broadcast (ATSC A/85 · CALM) | −24 LKFS | −2 dBTP | program |
| EU broadcast (EBU R128) | −23 LUFS | −1 dBTP | program |
| Premium streaming (Netflix-style) | −27 LKFS | −2 dBTP | **dialog-gated** |
| Web / social (Webmix) | −14 to −16 LUFS | −1 dBTP | program |

No single master satisfies all four — mix once, then produce normalized versions. Verify numbers against each recipient's current spec sheet.

**Export from the Deliver page** — each bus renders as its own file. 48 kHz / 24-bit, SMPTE order L R C LFE Ls Rs:

- **5.1 Print Master** → 6-ch WAV (or Dolby Digital, Studio) — the surround master.
- **Stems (DX/FX/MX/M&E)** → 6-ch WAVs — archival, QC, re-versioning. **M&E is usually mandatory.**
- **Stereo Print Master** → stereo WAV (Lt/Rt or Lo/Ro per spec).
- **Stereo stems + Stereo M&E** → stereo WAVs.
- **Webmix** → AAC/MP3 for online preview.

**Atmos:** skip unless a platform requests it — 5.1 + stereo is a complete package for an information piece.

---

*Related: [[Fairlight 5.1 - Glossary]] · [[Fairlight 5.1 Template - Build Spec]] · `map.html` · `Fairlight 5.1 Template - Routing.canvas` · `Fairlight 5.1 Routing.pdf`*
