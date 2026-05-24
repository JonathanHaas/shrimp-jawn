# Prompt: Hamburger Menu + About Section

## What we asked for

> "can you add an about hamburger menu and link to a shrimp color overlay of this [photo]"
> "add copy about them being shrimp enthusiasts (spelling)"

## Result

- Fixed top-right hamburger button (frosted glass circle, animates to ✕ when open)
- Slide-out drawer from the right with darkened overlay behind it
- Uploaded photo embedded as base64 with a coral/peach CSS color overlay
- About copy with "shrimp enthusiasts" spelled out proudly
- Nav links inside the drawer

## How the color overlay works

```css
.about-photo-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    160deg,
    rgba(255, 107, 107, 0.45) 0%,
    rgba(255, 179, 186, 0.3) 40%,
    rgba(255, 211, 182, 0.4) 100%
  );
  mix-blend-mode: multiply;
}
```

`mix-blend-mode: multiply` makes the overlay interact with the photo naturally — darker areas stay dark, highlights pick up the coral tint. Much more editorial than a plain opacity tint.

## Embedding photos as base64

```python
from PIL import Image
import base64, io

img = Image.open('photo.jpg')
img = img.resize((700, int(700 * img.height / img.width)), Image.LANCZOS)
buf = io.BytesIO()
img.save(buf, format='JPEG', quality=88)
b64 = base64.b64encode(buf.getvalue()).decode()
# Use as: src="data:image/jpeg;base64,{b64}"
```

Keep JPEG quality at 82–88 for a good size/quality balance. Images over ~300KB will make the HTML file large.

## Drawer JS pattern

```js
function toggleDrawer() {
  const isOpen = drawer.classList.contains('open');
  drawer.classList.toggle('open', !isOpen);
  overlay.classList.toggle('open', !isOpen);
  burger.classList.toggle('open', !isOpen);
  document.body.style.overflow = isOpen ? '' : 'hidden'; // prevent scroll behind drawer
}
```

## Prompt tips

- "Frosted glass" → `background: rgba(255,255,255,0.15); backdrop-filter: blur(8px)`
- Always lock body scroll when a drawer/modal is open
- `mix-blend-mode: multiply` for photo color overlays, not plain rgba tints
