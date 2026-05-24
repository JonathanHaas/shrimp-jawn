# Prompt: Character Bubbles

## What we asked for

> "CAN YOU ADD A BUBBLE WITH THIS [Harry Styles photo]"
> "can you add bubba gump as a bubble?"
> "can you replace the bubble image with this [Bubba movie still]"
> "add this too [Pee-wee Herman / then replaced with Pepe the King Prawn]"
> "one more edit - bubba gump should just be referred as bubba"

## Result

Three fixed-position floating character bubbles:
- **Harry Styles** — bottom-left, coral glow ring
- **Bubba** — bottom-right, same coral glow
- **Pepe the King Prawn** — above Bubba on the right

Each has:
- A circular photo (90×90px, border-radius: 50%)
- Alternating speech bubbles that fade in/out on a CSS animation cycle
- A name label beneath
- A gentle bob animation with slight rotation

## Speech bubble cycling pattern

Two or three spans stacked absolutely, with offset keyframe animations:

```css
.s1 { animation: pop1 6s ease-in-out infinite; }
.s2 { position: absolute; top: 0; opacity: 0; animation: pop2 6s ease-in-out infinite; }

@keyframes pop1 { 0%, 100% { opacity: 1; } 45%, 55% { opacity: 0; } }
@keyframes pop2 { 0%, 40%, 100% { opacity: 0; } 50%, 90% { opacity: 1; } }
```

For three quotes, divide the 100% timeline into thirds and offset accordingly.

## Bob animation per character

Give each character a slightly different duration and rotation to feel independent:

```css
/* Harry */
animation: harryFloat 4s ease-in-out infinite;
@keyframes harryFloat {
  0%, 100% { transform: translateY(0) rotate(-2deg); }
  50%       { transform: translateY(-12px) rotate(2deg); }
}

/* Bubba */
animation: bubbaFloat 4.5s ease-in-out infinite;

/* Pepe */
animation: peeweeFloat 3.5s ease-in-out infinite;
```

## Stacking bubbles vertically

```css
.bubba-bubble  { bottom: 2rem; right: 2rem; }
.peewee-bubble { bottom: 8rem; right: 2rem; } /* 6rem above Bubba */
```

## Speech bubble triangle pointer

```css
.char-speech::before {
  content: '';
  position: absolute;
  top: -7px; left: 50%;
  transform: translateX(-50%);
  border: 5px solid transparent;
  border-bottom-color: white;
  border-top: none;
}
```

## Prompt tips

- When replacing a placeholder illustration with a real photo, ask to "replace the bubble image" — keep all other CSS intact
- `void el.offsetWidth` pattern not needed here since animations run on CSS only
- Keep speech text short (under 5 words) for mobile — set `max-width: 120px; white-space: normal; text-align: center`
- Phase-offset animation delays (`animation-delay: 0.8s` per bubble) prevent synchronized bobbing
