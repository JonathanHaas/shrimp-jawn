# Lessons Learned + Future Prompts

## What worked well

### Be specific about revert targets
❌ "revert 3 changes ago" — hard to track without version history  
✅ "revert to the version before the floating bubbles change" — describes the state, not the count

### Keep it one file
Everything embedded as base64 (images, fonts via Google Fonts CDN) makes the site trivially deployable. No asset pipeline, no build step, no broken paths.

### CSS animations > JS for simple motion
The bobbing character bubbles and speech bubble cycling use pure CSS keyframes — zero JS overhead, no errors on load timing. Only use JS (`requestAnimationFrame`) when you need physics or interactivity.

### Always test mobile speech bubble width
Long strings with `white-space: nowrap` overflow on small screens. Use:
```css
white-space: normal;
max-width: 120px;
text-align: center;
```

---

## What to watch out for

### Global CSS replacements can hit unintended selectors
When we replaced `white-space: nowrap` across all speech bubbles, it also hit the `.marquee-wrap` — breaking the scrolling ticker. Always scope CSS changes to a specific selector.

### JS that runs before DOM is ready
Character bubble JS that queries `.harry-bubble` before the element exists throws:
> `TypeError: Cannot read properties of null (reading 'style')`

Fix: wrap in `window.addEventListener('DOMContentLoaded', ...)` or place the `<script>` tag after the elements in the HTML.

### base64 image size
| Quality | ~Size |
|---------|-------|
| JPEG q=85, 400×400 | ~25–45KB base64 |
| JPEG q=88, 700px wide portrait | ~250KB base64 |
| PNG screenshot (no resize) | 500KB+ — always resize first |

Keep total HTML file under 500KB for fast load.

---

## Suggested future prompts

### Add a new character bubble
> "Add a [character name] bubble in the [position] corner with these quotes: [quote 1], [quote 2]"

### Swap a character photo
> "Replace the [name] bubble image with this photo [upload]"

### Add a new section
> "Add a [section name] section between [section A] and [section B] with [description of content]"

### Change the color palette
> "Update the site palette — swap coral (#FF6B6B) for [new color] throughout"

### Add Instagram feed
Options:
1. **Behold.so embed** — paste the embed snippet: "Add this Instagram embed snippet to a new section below the marquee: [snippet]"
2. **Static screenshots** — "Add an Instagram feed section using these screenshots [upload] with captions [list]"

### Add music / sound
> "When the counter hits a billion milestone, play a short shrimp sound effect"

### Add a modal lightbox
> "When you click a recipe card, show a modal with the full recipe steps"

### Make it a PWA
> "Add a web app manifest and service worker so Shrimp Jawn can be installed on mobile"

---

## Project file structure (suggested for GitHub)

```
shrimp-jawn/
├── index.html          ← the whole site
├── README.md
└── docs/
    ├── PROMPT_01_initial_site.md
    ├── PROMPT_02_counter.md
    ├── PROMPT_03_hamburger_about.md
    ├── PROMPT_04_character_bubbles.md
    └── LESSONS_LEARNED.md
```
