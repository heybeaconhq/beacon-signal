# Beacon Signal — Content → Video Workflow

Turn raw content (tweets, articles, research, notes) into a produced video with a custom AI avatar, motion graphics, and thesis-driven narrative using HeyGen Video Agent.

**Video Agent is an HTML interpreter.** It renders layouts, typography, and structured content natively. Every scene you write will be interpreted as a structured page layout. Write accordingly — describe spatial composition explicitly, describe B-roll as layered text motion graphics, stack multiple visual layers per scene.

## Trigger Phrases

- "Beacon Signal about [topic]"
- "Make a video about [content]"
- "Beacon Signal, Swiss Pulse" (locks a specific visual style)

## Workflow

### Step 1: Pull Data

Source depends on the topic:
- **Social media** — API or scraping, sort by engagement, grab top posts with user metadata
- **Web** — search + article extraction
- **Internal** — notes, research files, whatever fits the topic

### Step 2: Synthesize a Thesis

Not a list. A story. *"X is happening because Y — here's the proof."*

- Group into 3–5 themes
- Identify the most quotable content for on-screen display
- Every video needs a narrative arc, not bullet points

### Step 3: Pick a Visual Style

Choose from the [20-style library](styles.md). Match **mood first, content second** — ask: *"What should the viewer FEEL?"*

| If the content feels... | Use... |
|---|---|
| Data-driven, analytical | Swiss Pulse, Digital Grid |
| Personal, intimate | Soft Signal, Quiet Drama |
| Breaking, urgent | Red Wire |
| Fun, lighthearted | Play Mode, Carnival Surge |
| Dark, investigative | Shadow Cut, Contact Sheet |
| Hype, high-energy | Maximalist Type, Deconstructed |
| Tech-forward, futuristic | Data Drift |
| Elegant, premium | Velvet Standard, Geometric Bold |
| Cultural, global | Silk Route, Folk Frequency |

See [styles.md](styles.md) for all 20 styles with full visual specs and example scenes.

### Step 4: Design the Avatar

The avatar is NOT a fixed headshot. Design it for each video like a **movie character** — think costume designer + set designer.

**Rules:**
1. **Wardrobe is thematic** — match the cultural/emotional context of the content
2. **Set has brand props** — discussing Reddit? Show the Reddit logo in the scene
3. **Describe at costume-designer level** — fabric, color, accessories, posture
4. **Describe at set-designer level** — lighting, props, what's on the walls/desk
5. **Rich environment (60–100 words)** — 3+ content-specific props, dark/moody lighting preferred

| Content Type | Avatar Design | NOT This |
|---|---|---|
| Chinese New Year | Red qipao with gold embroidery, lantern-lit courtyard | "Reporter in a blazer" |
| Breaking tech news | Field reporter, windswept hair, earpiece, city skyline | "Anchor at a desk" |
| Sleep science | Oversized cream knit, cross-legged on bed, warm lamp, sleep tracker on wrist | "Analyst in a lab" |
| Reddit community | Messy desk, Reddit alien on monitors, orange upvote arrows on wall | "Researcher in a studio" |

### Step 5: Generate & Upload Avatar Look

Use any image generation model to create a photorealistic avatar photo, then upload to HeyGen.

See [avatars.md](avatars.md) for the full pipeline: prompt template, photorealism rules, HeyGen upload API calls.

### Step 6: Write the Video Agent Prompt

This is where the work happens. Structure:

1. **Format + tone** — e.g., "Bloomberg tech segment," "podcast breakdown"
2. **Avatar description** — at costume/set designer level (from Step 4)
3. **Visual style specs** — concrete rules from the chosen style (from Step 3)
4. **CRITICAL content block** — mark all real quotes, usernames, numbers: "MUST appear as readable on-screen text"
5. **Scene-by-scene storyboard** — rotate between the three scene types (see below)
6. **Close** — avatar wraps with punchy summary + end card
7. **Music + narration tone**

See [prompting.md](prompting.md) for the full prompt template, proven patterns, and anti-patterns.

### Step 7: Fire Video Agent

```
POST https://api.heygen.com/v1/video_agent/generate
{
  "prompt": "...",
  "config": {
    "avatar_id": "<look_id from Step 5>",
    "duration_sec": 75,
    "orientation": "landscape"
  }
}
```

Always pass `config.avatar_id` with the look from Step 5. Poll for completion, then retrieve the share link.

---

## Scene Types

Every prompt MUST rotate between these three types. Never do 3+ of the same type in a row. Every prompt needs at least 2 pure B-roll scenes.

### A-ROLL (Avatar Presenting)

Avatar talks to camera. Include:
- Spatial directive: "Avatar center-frame" or "Avatar left third"
- Gesture, expression, body language
- Set references: "Monitor behind shows [X]", "Ticker reads [Y]"

### B-ROLL (Full-Screen Motion Graphics — NO Avatar)

This is where the chosen style's DNA lives. Push it to maximum intensity. Minimum structure:

- **LAYER 1 (background):** Textured, branded, patterned — NOT a dark solid
- **LAYER 2 (primary content):** Bold headline, key number, or quote
- **LAYER 3 (supporting):** Labels, annotations, secondary data — must MOVE
- **LAYER 4 (accent/motion):** Animated bars, tickers, counting numbers, connectors
- **LAYER 5+ (style flourish):** Artist-specific motifs — overlapping text (Scher), pixel dissolves (Crouwel), deconstructed fragments (Brody)

**Every element must MOVE.** Use verbs: "slams in," "types on letter by letter," "counts up from 0," "cascades from top," "pulses," "glitches."

**Every B-roll scene MUST include a `VOICEOVER:` line.** Narration never stops.

Example:
```
SCENE 3 — FULL SCREEN B-ROLL (10 sec)
[NO AVATAR — motion graphic only]
VOICEOVER: "One hundred thirty-five thousand gateways exposed — 
  and fifteen thousand vulnerable to remote code execution."
LAYER 1: Dark #1a1a1a background with animated hex grid — grid lines 
  pulse outward from center like a radar ping, orange #FF4500 glow.
LAYER 2: "135K" SLAMS in from left edge, white Impact 120pt, fills 
  40% of frame. "GATEWAYS EXPOSED" types on letter-by-letter underneath 
  in orange, mechanical typewriter rhythm.
LAYER 3: Three data cards CASCADE from top, staggered 0.3s apart — 
  each counts UP from 0 to final value (135K, 15K, 900).
LAYER 4: Bottom ticker SLIDES in from right — continuous scroll with 
  source attribution.
LAYER 5: Hex grid fragments SHATTER on the "135K" slam impact — 
  particles drift and fade. Scan-line glitch at 0.5s and 0.8s.
```

### A-ROLL + OVERLAY (Avatar + Content Side by Side)

Always specify explicit spatial composition:
```
SPLIT FRAME — Avatar LEFT 35%, content RIGHT 65%. NO overlap.
```

Content side needs 3+ layers: primary (headline/quote), supporting (labels/stats), accent (animated elements). Alternate which side the avatar is on between overlay scenes.

---

## Quality Rules

- **Every scene has motion** — no static frames
- **Real content on screen** — exact quotes, usernames, follower counts, not paraphrases
- **Mark content CRITICAL** — so Video Agent renders it literally
- **Thesis-driven** — not "here are 5 tweets" but "here's what's happening and why"
- **Scene type rotation mandatory** — alternate A-roll → B-roll → overlay
- **Thematic wardrobe always** — avatar outfit matches content's emotional context
- **Brand logos in scenes** — if discussing a company, its logo appears in the scene
- **Explicit spatial composition on every scene** — no defaults
- **Text animation = primary visual language** — kinetic typography matching voiceover
- **Multi-layer motion graphics** — 4+ layers per B-roll, 3+ on overlay content side
- **Maximum style intensity on B-roll** — push the artist's DNA hard
- **Nothing is static** — every element enters, transforms, exits
- **Voiceover on every scene** — narration never stops, including B-roll
- **Natural scene lengths** — 10–15 seconds per scene. Forced ≤5s B-roll = black frames

---

## Reference Files

| File | Use During |
|------|-----------|
| [styles.md](styles.md) | Step 3 — choosing and applying a visual style |
| [prompting.md](prompting.md) | Step 6 — writing the Video Agent prompt |
| [avatars.md](avatars.md) | Step 5 — generating and uploading avatar looks |
