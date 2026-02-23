# Beacon Signal

Turn any content into a broadcast-quality video using [HeyGen Video Agent](https://docs.heygen.com/docs/video-agent).

> **The core insight:** Video Agent is an HTML interpreter. It renders layouts, typography, and structured content natively. Write prompts like storyboards for a motion graphics editor — not like text descriptions.

## Example Videos

- [Swiss Pulse — OpenClaw × OpenAI](https://app.heygen.com/share/95f7ee06388843ada664f0711ae2a0fc) (105s)
- [Digital Grid — HeyGen Twitter](https://app.heygen.com/share/ffb9b506798e409d9f0f32c1dad1b09b) (100s)
- [Digital Grid — OpenClaw](https://app.heygen.com/share/6f8f2f8d6bc64293839e9c0e9186b856) (82s)
- [Deconstructed — HeyGen Twitter](https://app.heygen.com/share/67579148ecb744c5bb69395a5d4d71d2) (89s)

## Install

Clone into your agent's skills directory:

```bash
git clone https://github.com/heybeaconhq/beacon-signal.git /path/to/skills/beacon-signal
```

Then tell your agent: *"Beacon Signal about [topic]"*

Your agent reads `SKILL.md` and follows the workflow. The reference files (`styles.md`, `prompting.md`, `avatars.md`) provide deeper detail for each step.

## Prerequisites

- [HeyGen API key](https://docs.heygen.com/reference/authentication) with Video Agent access
- An image generation model for avatar looks (Gemini Imagen, DALL-E, Flux, etc.)
- A photo avatar group in HeyGen (create via [API](https://docs.heygen.com/reference/create-photo-avatar-group) or dashboard)

## What's Inside

| File | For | What It Does |
|------|-----|-------------|
| `SKILL.md` | Your agent | Complete workflow — read this and go |
| `styles.md` | Your agent | 20 visual styles with full specs |
| `prompting.md` | Your agent | Prompt patterns, anti-patterns, template |
| `avatars.md` | Your agent | Avatar look generation + HeyGen upload |

## License

[MIT](LICENSE)
