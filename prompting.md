# Video Agent Prompting Guide

How to write effective Video Agent prompts. These patterns come from 40+ produced videos.

## The Core Insight

**Video Agent is an HTML interpreter.** It renders layouts, typography, and structured content natively. This means:

- Describe **spatial composition** explicitly ("Avatar left 35%, content right 65%")
- Describe B-roll as **layered text motion graphics**, not imagery
- Use **action verbs** ("slams in," "types on," "counts up") not layout specs ("upper-left, 48pt")

## What Works

### Natural Storyboards

Write each scene like a shot list for a motion graphics editor. Describe what happens, in order, with motion verbs.

```
✅ LAYER 2: "135K" SLAMS in from left, white Impact 120pt, fills 
   40% of frame. "GATEWAYS EXPOSED" types on underneath in orange.
```

### CRITICAL Content Blocks

Real quotes, usernames, and numbers marked CRITICAL consistently render on-screen:

```
✅ CRITICAL: The following MUST appear as readable on-screen text:
   - @techfounder92 (24.5K followers): "I signed up and it changed everything"
   - @devops_daily (180K followers): "This is the future of infrastructure"
```

### Thematic Wardrobe

Describe avatars at costume-designer level:

```
✅ Cream cable-knit sweater, cross-legged on a cozy couch, reading lamp 
   casting warm amber glow, sleep tracker visible on left wrist

❌ Professional woman in business casual attire in a studio
```

### Scene Type Rotation

Alternate between A-roll, B-roll, and overlay. Never 3+ avatar scenes in a row. Every prompt needs at least 2 pure B-roll scenes.

### Voiceover on Every Scene

Narration never stops. Every B-roll scene needs a `VOICEOVER:` line. Silent B-roll = broken video.

### Explicit Spatial Composition

Every scene needs layout direction:
- A-roll: "Avatar center-frame" or "Avatar left third"
- Overlay: "SPLIT FRAME — Avatar LEFT 35%, content RIGHT 65%"
- B-roll: describe arrangement of all layers

### Multi-Layer Motion Graphics

Every B-roll scene: 4+ layers. Every overlay content side: 3+ layers.

| Layer | Purpose | Example |
|-------|---------|---------|
| 1 — Background | Textured, patterned | Animated hex grid pulsing outward |
| 2 — Primary | Key headline or number | "135K" slams in from left |
| 3 — Supporting | Labels, secondary data | Data cards cascade from top |
| 4 — Accent | Animated bars, tickers | Bottom ticker slides in |
| 5+ — Style | Artist-specific motifs | Grid fragments shatter on impact |

## What Doesn't Work

### ❌ Layout Language

Describing screen coordinates causes empty/black B-roll:

```
❌ "UPPER-LEFT: headline in 48pt Helvetica"
❌ "Left 35 percent vermillion red. Right 60 percent footage"
❌ "CENTER-SCREEN: large number display at coordinates (400, 300)"
```

### ❌ Named Artists Without Specs

"Ikko Tanaka style" means nothing to Video Agent. Specify concrete rules:

```
❌ "Use an Ikko Tanaka style"
✅ "Flat color blocks, maximum 3 colors per frame, asymmetric composition, 
    60% negative space, typography as primary element"
```

### ❌ Forced Short B-Roll (≤5 seconds)

Too short for meaningful motion graphics. All tested videos with 5-second B-roll had empty/black screens. Let scenes breathe at 10–15 seconds.

### ❌ Style Examples Injected Into Prompts

Adding full example scenes from a style library confused Video Agent — the examples competed with the actual storyboard. Keep the style as concrete rules, not injected examples.

### ❌ Generic Avatar Descriptions

```
❌ "Professional reporter in a studio"
✅ "Field reporter in navy windbreaker, earpiece in right ear, hair slightly 
    windswept. Rooftop at dusk, city skyline behind, breaking news ticker 
    on a monitor to her left."
```

## Prompt Template

```
FORMAT: [Reference — "Bloomberg tech segment", "Vice documentary", "podcast breakdown"]
TONE: [Tone — "Authoritative but conversational", "Data-driven, slight urgency"]
DURATION: ~75 seconds

---

AVATAR DESCRIPTION:
[60-100 words. Costume-designer level: fabric, color, accessories, posture, expression.
Set-designer level: props, lighting, what's on the walls, specific environment details.
Match the content's emotional/cultural context.]

---

VISUAL STYLE: [Style Name] — [Artist]
- [Color palette — specific hex codes or named colors]
- [Composition rules — framing, spacing, alignment]
- [Typography — typeface, weight, sizing, treatment]
- [Transitions — how scenes connect]

---

CRITICAL CONTENT (MUST appear as readable on-screen text):
- [Quote 1 with full attribution — username, followers, exact text]
- [Stat 1 with source]
- [Quote 2 with full attribution]

---

SCENE 1 — A-ROLL (12 sec)
[Avatar position: center-frame / left third]
[What they say, gesture, expression]
[Set references: "monitor behind shows...", "ticker on wall reads..."]

SCENE 2 — FULL SCREEN B-ROLL (10 sec)
[NO AVATAR — motion graphic only]
VOICEOVER: "[Narration continues over graphics]"
LAYER 1: [Background — texture, pattern, color]
LAYER 2: [Primary content — headline, key number, motion verb]
LAYER 3: [Supporting — labels, data cards, annotation, motion verb]
LAYER 4: [Accent — tickers, connectors, animated elements]
LAYER 5: [Style flourish — artist-specific motif, motion verb]
[Transition to next scene]

SCENE 3 — A-ROLL + OVERLAY (12 sec)
SPLIT FRAME — Avatar LEFT/RIGHT 35%, content occupies 65%.
[Avatar: what they're saying, gesture, expression]
[Content side: quote card / data display / comparison]
[Content layers: primary + supporting + accent elements]

[... continue scenes, rotating types ...]

FINAL SCENE — A-ROLL (8 sec)
[Avatar wraps with punchy summary]
[End card with key takeaway]

---

MUSIC: [Direction — "Minimal electronic pulse, builds gradually"]
NARRATION: [Tone — "Measured, confident, slight urgency on data points"]
```

## Style Performance

Based on 40+ videos:

| Rank | Style | Strength |
|------|-------|----------|
| 1 | Deconstructed (Brody) | Most reliable across all topics |
| 2 | Swiss Pulse (Müller-Brockmann) | Best for data-heavy content |
| 3 | Digital Grid (Crouwel) | Strong for tech topics |
| 4 | Geometric Bold (Tanaka) | Elegant and versatile |
| 5 | Maximalist Type (Scher) | High energy, use sparingly |

## Duration Insights

| Approach | Avg Duration |
|----------|-------------|
| Natural storyboard + custom avatar | ~106s |
| Natural storyboard, no custom avatar | ~69s |
| Forced short scenes + custom avatar | ~71s |
| Layout language prompts | ~48s |

Natural storyboard + photorealistic custom avatar = longest, best videos.
