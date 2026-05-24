# Prompt: Shrimp Ate Counter

## What we asked for

> "can you add a fast counter of shrimps ate?"
> "can you increase it by 1000s with random numbers?"
> "can you make the shrimp counter smaller and make it in the billions"

## Result

An auto-running counter that:
- Starts at a random value between 500B–1T
- Jumps forward in random increments on a set interval
- Displays formatted as `X.XXX billion` / `X.XXX trillion`
- Has three speed modes with a label showing the last jump amount
- Pulses the number on each tick with a CSS scale animation

## Speed modes

| Mode | Jump range | Interval |
|------|-----------|----------|
| 🐢 Chill | +10M–80M | 200ms |
| 🚀 Chaotic | +200M–999M | 100ms |
| 🌊 UNHINGED | +1B–9.9B | 50ms |

## Core JS pattern

```js
let count = Math.floor(Math.random() * 500e9) + 500e9;

function formatBillions(n) {
  if (n >= 1e12) return (n / 1e12).toFixed(3) + ' trillion';
  if (n >= 1e9)  return (n / 1e9).toFixed(3) + ' billion';
  return n.toLocaleString();
}

function randBetween(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

function jump() {
  const bump = randBetween(speed.min, speed.max);
  count += bump;
  el.textContent = formatBillions(count);
  el.classList.remove('tick');
  void el.offsetWidth; // force reflow to re-trigger animation
  el.classList.add('tick');
}

ticker = setInterval(jump, speed.ms);
```

## Prompt tips

- "Start in the billions" — set the seed value high so it feels global-scale immediately
- `void el.offsetWidth` is the trick to re-trigger a CSS animation on the same element
- Keep the font size smaller for large numbers so they don't overflow on mobile
