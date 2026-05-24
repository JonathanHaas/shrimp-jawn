# Prompt: Initial Site Generation

## What we asked for

> "can you build a single page shrimp centric website that is whimsical"

## Result

A fully self-contained single-page HTML site with:
- Pastel gradient hero with animated bobbing 🦐 emoji and floating bubble particles
- Animated wave SVG at the bottom of the hero
- Scrolling dark marquee ticker with shrimp facts
- Facts grid with hover animations (tilt + coral border)
- Shrimp species cards
- Dark ocean poetry section
- Seafoam recipe cards
- Coral counter section
- FAQ accordion
- Footer
- Shrimp emoji cursor
- Floating shrimp that drift across the screen periodically

## Key design decisions

- **Fonts:** Fraunces (serif, display) + Nunito (rounded sans)
- **Palette:** `--coral: #FF6B6B`, `--peach: #FFD3B6`, `--seafoam: #A8E6CF`, `--deep: #1A3A4A`, `--sand: #FFF5E6`, `--sky: #E8F4FD`
- **Tone:** Whimsical, warm, playful — not ironic
- **Stack:** Zero dependencies, one HTML file

## Prompt tips for similar sites

- Specify "whimsical" or "playful" for loose, bouncy animations
- Ask for `Fraunces` serif for display headings — it gives editorial warmth
- Request `cubic-bezier(0.34, 1.56, 0.64, 1)` transitions for that satisfying overshoot bounce
- "One file, no frameworks" keeps it deployable anywhere instantly
