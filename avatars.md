# Avatar Generation Pipeline

Generate a photorealistic avatar look for each video, then upload to HeyGen as a new look in your photo avatar group.

## Overview

1. **Generate** — use any image generation model with a reference photo for face consistency
2. **Upload** — push the image to HeyGen's asset store
3. **Add to group** — attach as a new look in your avatar group
4. **Wait** — poll until the look is validated and ready

## Step 1: Generate the Look

Use an image generation model (Gemini Imagen, DALL-E, Flux, etc.) with a reference photo of the avatar's face for identity consistency. The reference carries the identity — **do not describe the person's physical appearance** in the prompt. Only describe what's NEW: wardrobe, environment, lighting, pose.

### Prompt Template

```
[Facing camera / natural 3/4 angle], [expression — genuine, not posed].
[Thematic wardrobe — fabric, color, fit, accessories. Match the content's vibe].
[Creative environment — specific props, brand logos, set details that evoke the topic].
Shot on Canon 5D Mark IV, 85mm f/1.8.
Natural skin with visible pores and texture, no retouching.
Slight film grain, slightly desaturated warm tones.
[Natural lighting — direction, color temperature], slight shadows under chin.
[Messy real details — wrinkled fabric, half-empty mug, cluttered desk, etc.]
Muted color palette, slightly desaturated.
This should look like a real candid photo, NOT an AI render.
```

### Photorealism Rules

These are baked into the template, listed here for reference:

1. **Camera hardware** — "Shot on Canon 5D Mark IV, 85mm f/1.8"
2. **Natural skin** — "visible pores and texture, no retouching"
3. **Film characteristics** — "Slight film grain, slightly desaturated warm tones"
4. **Natural lighting** — direction + color temp + "slight shadows under chin"
5. **Candid, not posed** — "genuine relaxed smile, not posed"
6. **Grounded wardrobe** — everyday clothes, not theatrical costumes
7. **Messy real environments** — clutter, wrinkled fabric, lived-in spaces
8. **Muted palette** — slightly desaturated, warm, NOT oversaturated
9. **Anti-AI-render closing** — always end with the line
10. **Reference image** — always pass a face reference for identity consistency
11. **Face toward camera** — front-facing or natural 3/4 angle
12. **Simple compositions** — one person, one environment, one light source

### Creative Direction

Be **ambitiously creative** with environment and outfit. The wardrobe, set, and props should viscerally evoke the content's theme — not just reference it. Think music video director, not corporate photographer.

- Sleep science → cozy knit on a king bed with amber lamp, books on nightstand, morning light through sheer curtains
- Breaking tech story → glass newsroom with company logos on monitors behind
- Reddit community → messy desk with Reddit alien logo glowing on dual monitors, orange upvote arrows on wall

## Step 2: Upload to HeyGen

```bash
# Upload the generated image
curl -X POST "https://upload.heygen.com/v1/asset" \
  -H "x-api-key: <your-api-key>" \
  -H "Content-Type: image/png" \
  --data-binary @generated_avatar.png
```

Returns an `image_key`.

## Step 3: Add to Avatar Group

```bash
# Add as a new look in your avatar group
curl -X POST "https://api.heygen.com/v2/photo_avatar/<your-avatar-group-id>/look" \
  -H "x-api-key: <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{"name": "descriptive-look-name", "image_keys": ["<image_key>"]}'
```

Returns a `look_id`. This is your `avatar_id` for the Video Agent call.

## Step 4: Wait for Validation

```bash
# Poll until status is "completed"
curl "https://api.heygen.com/v2/photo_avatar/<look_id>" \
  -H "x-api-key: <your-api-key>"
```

Training is automatic — no extra API call needed. Once `status: completed`, the look is ready to use.

## Important

- **Always add looks to an existing group.** Don't create a new avatar group per video.
- **Don't describe the person's face/body** in the generation prompt. The reference image carries the identity.
- **Pass `config.avatar_id`** in the Video Agent API call with the look_id from Step 3.
