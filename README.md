# Fairlight 5.1 Interactive Routing Map

An interactive, single-file signal-flow map of a professional **5.1 film/TV mixing template** for **DaVinci Resolve Studio's Fairlight page** — with step-by-step build instructions, plain-English explanations for beginners, and a full glossary built in.

Verified against **DaVinci Resolve Studio 21.0.2** (FlexBus, July 2026).

> Open `map.html` in any browser. No install, no build step, no dependencies — everything is one self-contained file.

## What it does

- **Click any box** (track, bus, stem, VCA) to trace its complete signal path — everything that feeds it, everything it feeds, and the full downstream chain — plus exact Resolve 21 build steps (menus, clicks, formats) and *why it's built that way*.
- **Click any connection line** to learn what that route does and how to create it (Bus Outputs, Bus Sends, Bus Assign, VCA Assign…).
- **Hover any dotted-underlined term** for an instant definition (LUFS, dBTP, dialog-gated, M&E…).
- **Sidebar guides:** a "New to mixing? Start here" primer, a full A-to-Z glossary, Resolve 21/FlexBus version notes, a 21-bus build-order checklist with exact formats, and broadcast/streaming/web delivery targets.
- Drag to pan, scroll to zoom. Column headers, delivery-targets box and line-style key are drawn on the map itself, so it reads like the printed reference too.

## The template it documents

A documentary-style 5.1 mix structure for **broadcast, web and streaming** delivery:

```
11 SOURCE TRACKS → STEMS (DX / FX / MX + stereo mirrors) → PRINT MASTERS (5.1 + Stereo) → delivery
                     ↑                                        ↓
               8 reverb buses (aux)                    Webmix (compressed stereo)
```

Plus: 4 VCA control groups, 2 dedicated LFE buses, and an M&E (Music & Effects) stem built bus-to-bus so the foreign-dub deliverable can never drift out of sync with the mix. Delivery targets covered: ATSC A/85 (−24 LKFS), EBU R128 (−23 LUFS), Netflix-style dialog-gated (−27 LKFS), and web (~−14 LUFS).

## The site

Three interconnected pages, all self-contained static HTML (no build step, no dependencies):

| Page | What it is |
|------|-----------|
| `index.html` | **Landing page** — hero, live map preview, feature overview, the full kit |
| `map.html` | **The interactive map** — supports deep links (`?select=st_dx` opens with that element selected) |
| `guide.html` | **The build guide** — step-by-step instructions, interactive checklist with saved progress; every element deep-links to the map |
| `spec.html` | **The build spec** — the full engineering reference: 21-bus format table, build order A–L, delivery matrix |
| `glossary.html` | **The glossary** — every acronym and term, live-filterable, with deep links into the map |

## Companion documents

| File | What it is |
|------|-----------|
| `Fairlight 5.1 - Master Guide.md` | The full written guide (same content in document form) |
| `Fairlight 5.1 - Glossary.md` | Every acronym & term, explained for beginners |
| `Fairlight 5.1 Template - Build Spec.md` | The original build specification (Resolve 21 / FlexBus corrected) |
| `Fairlight 5.1 Template - Routing.canvas` | Obsidian Canvas version of the map |
| `Fairlight 5.1 Routing.pdf` | Static print reference |

## Hosting it with GitHub Pages

Everything is static, so GitHub Pages serves it directly:

1. Push this repo to GitHub.
2. Repo **Settings → Pages** → Source: *Deploy from a branch* → branch `main`, folder `/ (root)`.
3. The landing page is live at `https://<username>.github.io/<repo>/` — the map and guide are linked from there.

## Requirements

- Any modern browser to view the map.
- To build the template itself: **DaVinci Resolve 17+** (FlexBus). The free version covers buses, VCAs, 5.1 and loudness metering; **Resolve Studio** adds immersive formats, Dolby Digital encoding and the AI voice tools used in the delivery workflow.

## Notes

- Bus roles vs types: modern Resolve (FlexBus) has no Main/Sub/Aux bus types — the labels on the map are *roles* created by routing. The version-notes panel in the sidebar explains this.
- Loudness figures reflect common 2026 delivery specs; always verify against your recipient's current spec sheet.

## License

MIT — use it, fork it, adapt it for your own template. Attribution appreciated.
