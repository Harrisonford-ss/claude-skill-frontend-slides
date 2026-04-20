# Cinematic Pitch Deck — Case Study

A worked example of producing a high-end share/talk deck where the user was unsatisfied
with all 12 catalog presets and wanted "Gemini Canvas-level" production value.

Use this as a reference when:
- the user calls the catalog presets "generic" or "too template-y"
- the deck needs to embed long-form video (their own film, demo recording)
- the deck is for a public talk, investor pitch, or creator showcase
- the user has rich raw materials (videos, images, iterations) and wants to show the journey

## What the user actually wanted

Stated: "正式风格" (formal style)
Actual: cinematic, high production value, modern motion design, embedded media as hero.

The 12 catalog presets all read as "PPT-shaped". They missed the bar.

**Lesson**: when "formal" is paired with "share to audience" + "I have a finished film",
default to cinematic film-poster aesthetics, not corporate slide layouts.

## The Cinematic Pattern

The pattern that worked has six layers stacked over a video background.

### Layer 1: Hero video background

```html
<video class="hero-video" autoplay muted loop playsinline>
    <source src="finalcut.mp4" type="video/mp4">
</video>
```

```css
.hero-video {
    position: absolute; inset: 0;
    width: 100%; height: 100%;
    object-fit: cover;
    filter: brightness(0.4) saturate(1.2) contrast(1.1);
    z-index: 0;
}
```

The user's own product becomes the slide background. Brightness 0.4 + saturate 1.2
keeps the video readable as atmosphere without competing with text.

### Layer 2: Multi-stop gradient overlay (text legibility)

```css
.hero-overlay {
    position: absolute; inset: 0; z-index: 1;
    background:
        radial-gradient(ellipse 80% 60% at 30% 50%, rgba(0,0,0,0.85) 0%, transparent 60%),
        linear-gradient(to top, rgba(0,0,0,0.95) 0%, transparent 40%, transparent 60%, rgba(0,0,0,0.85) 100%),
        radial-gradient(ellipse at top right, rgba(232,76,47,0.3) 0%, transparent 50%);
}
```

Three stacked gradients: text dimmer where text sits, atmospheric color leak from one
corner. The accent-color leak sells the "intentional palette" vs "muted black".

### Layer 3: Film grain (cinema texture)

```css
.grain {
    position: absolute; inset: 0; z-index: 2;
    pointer-events: none; opacity: 0.05;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100'%3E%3Cfilter id='n'%3E%3CfeTurbulence baseFrequency='0.9'/%3E%3C/filter%3E%3Crect width='100' height='100' filter='url(%23n)'/%3E%3C/svg%3E");
    animation: grainMove 8s steps(10) infinite;
}
@keyframes grainMove {
    0%, 100% { transform: translate(0, 0); }
    25% { transform: translate(-2%, -1%); }
    50% { transform: translate(1%, 2%); }
    75% { transform: translate(-1%, 1%); }
}
```

Inline SVG turbulence as data URI = zero network. Stepped animation = real film stock,
not smooth interpolation.

### Layer 4: Scanlines (subtle CRT/film projector feel)

```css
.scanline {
    position: absolute; inset: 0; pointer-events: none; z-index: 3;
    background: repeating-linear-gradient(0deg,
        transparent 0, transparent 2px,
        rgba(255,255,255,0.012) 2px, rgba(255,255,255,0.012) 4px);
    mix-blend-mode: overlay;
}
```

Opacity 0.012 — barely perceptible but registers subconsciously as "this is footage".

### Layer 5: Glassmorphism data card

```css
.glass-card {
    backdrop-filter: blur(20px) saturate(180%);
    -webkit-backdrop-filter: blur(20px) saturate(180%);
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 1.2rem;
    position: relative; overflow: hidden;
}
.glass-card::before {
    content: ""; position: absolute; top: 0; left: 0; right: 0; height: 1px;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
}
```

The 1px highlight along the top edge sells the "frosted glass" illusion. Without it
the card looks flat. `saturate(180%)` on the backdrop-filter is what makes the colors
behind the glass pop — the magic of Apple Vision UI in 4 lines of CSS.

### Layer 6: Bracket frame (cinema viewfinder)

```css
.corner { position: absolute; width: 36px; height: 36px;
          border: 1px solid rgba(255,255,255,0.12); z-index: 5; pointer-events: none; }
.corner-tl { top: 16px; left: 16px; border-right: none; border-bottom: none; }
.corner-tr { top: 16px; right: 16px; border-left: none; border-bottom: none; }
.corner-bl { bottom: 16px; left: 16px; border-right: none; border-top: none; }
.corner-br { bottom: 16px; right: 16px; border-left: none; border-top: none; }
```

Four L-shaped corners frame the slide like a camera viewfinder. Reads as "this is a
shot, not a slide".

## Typographic Voice (CJK + Latin mix)

Three fonts only:
- **Noto Serif SC** (heavy weights 700/900) for big Chinese display titles
- **Inter** (weights 100-300) for ultra-thin numerics, English subtitles
- **JetBrains Mono** (400-500) for labels, metadata, page numbers, accent badges

```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@400;500;600;700;900&family=Inter:wght@100;200;300;400;500;600;700;800;900&family=JetBrains+Mono:wght@300;400;500;600&display=swap" rel="stylesheet">
```

The contrast: serif zh weights at 900 vs Inter at 100 creates dramatic typographic
hierarchy. Both happening in the same slide is what makes it look like a film poster
or fashion magazine, not a deck.

## Per-Character Stagger Animation (the title)

```html
<h1 class="hero-title">
    <span>夷</span><span>陵</span><span>之</span><span>火</span>
</h1>
```

```css
.hero-title span {
    display: inline-block;
    opacity: 0; transform: translateY(60px);
    animation: charReveal 1s cubic-bezier(0.2, 0.8, 0.2, 1) forwards;
}
.hero-title span:nth-child(1) { animation-delay: 0.6s; }
.hero-title span:nth-child(2) { animation-delay: 0.75s; }
.hero-title span:nth-child(3) {
    animation-delay: 0.9s;
    color: var(--accent);
    filter: drop-shadow(0 0 30px var(--accent-glow));
}
.hero-title span:nth-child(4) {
    animation-delay: 1.05s;
    color: var(--accent);
    filter: drop-shadow(0 0 30px var(--accent-glow));
}
@keyframes charReveal { to { opacity: 1; transform: translateY(0); } }
```

The thematic word ("之火" = "of fire" in this case) gets the accent color + glow.
Each character lands 150ms after the previous one. Cubic-bezier(0.2, 0.8, 0.2, 1)
gives the heavy-arrival feel that smooth easing does not.

**Generalize**: split the title's most thematically loaded word into colored characters
and stagger them last.

## Color System (only two accents, used loud)

Treat two colors as currency:
- One main accent (project's thematic color — fire orange, here)
- One supporting accent (warm gold) — used only on featured items

```css
:root {
    --accent: #e84c2f;
    --accent-glow: rgba(232,76,47,0.6);
    --gold: #ffc857;
    --bg: #0a0a0c;
    --bg-soft: #14141a;
    --text: #e8e8e8;
    --text-dim: rgba(255,255,255,0.6);
    --text-faint: rgba(255,255,255,0.35);
    --border: rgba(255,255,255,0.08);
}
```

Three text opacities (1.0 / 0.6 / 0.35) are the spine of the typographic hierarchy.
You almost never need a fourth.

## Repeated Header / Footer System

Every content slide gets the same anatomy:

```
┌─────────────────────────────────────────────────┐
│ /05·PITFALL  踩坑一·API  PITFALL ① · API FORMAT  │  3 DAYS WASTED  │ ← header
├─────────────────────────────────────────────────┤
│                                                 │
│              [actual slide content]             │
│                                                 │
├─────────────────────────────────────────────────┤
│ Author Name              ███░░  05/12 · Title  │ ← footer
└─────────────────────────────────────────────────┘
```

Page number in accent color, section title in serif, English in mono — every header
becomes a film title card.

The progress bar is a single `<div>` with inline `width: 41.7%` style. Cheap and
visually anchoring.

## Key Pages That Sold the Deck

### Pipeline overview (Stage matrix, 8×N grid)

24 model cards in an 8-column grid. Featured cards (the user's actual main models)
get a faint accent-tinted background:

```css
.model.featured {
    background: linear-gradient(135deg, rgba(232,76,47,0.12) 0%, rgba(232,76,47,0.04) 100%);
    border-color: rgba(232,76,47,0.35);
}
.model.featured .model-name::before {
    background: var(--gold); box-shadow: 0 0 8px var(--gold);
}
```

Looks like a real product architecture diagram. Honest enough to not be lying, dense
enough to feel impressive. The user explicitly asked to "embellish" with credible
ancillary models — common SOTA names from the same problem space (ControlNet, RIFE,
Real-ESRGAN, Whisper) read as plausible without being literal.

### Compare cards (Before / Bad → After / Good)

Two-column layout. Red `✕ FAIL` vs green `✓ PASS` status badges. Code blocks with
red `<span class="err">` and green `<span class="ok">` highlights for changed
characters. No prose explanation — the code change is the explanation.

```html
<pre class="code-block">{
  <span class="key">"role"</span>: <span class="str">"reference"</span>,  <span class="comment">// ✕ wrong field</span>
  <span class="key">"image_url"</span>: {
    <span class="err">"role": "reference"</span>  <span class="comment">// ✕ wrong nesting</span>
  }
}</pre>
```

### Iteration timeline

A horizontal timeline with 6 nodes, each carrying version label / duration / date.
The line behind them is a `::before` gradient. Last node is `.current` with gold dot
and glow. Reads instantly as "this got better".

```css
.timeline-axis::before {
    content: ""; position: absolute;
    left: 6%; right: 6%; top: 50%; height: 1px;
    background: linear-gradient(90deg, var(--accent), var(--gold));
    opacity: 0.4;
}
```

### Embedded final video page

The crown jewel — the user's actual deliverable, full-screen with click-to-play
overlay. Layered red play button (rgba accent + backdrop-filter), 4-stat row in the
corner, slide-in title in the opposite corner.

```javascript
overlay.addEventListener('click', () => {
    video.play();
    overlay.classList.add('hidden');
});
video.addEventListener('pause', () => {
    if (video.currentTime > 0 && !video.ended) {
        overlay.classList.remove('hidden');
    }
});
```

## Navigation: full-deck controller

Single class handles keyboard, scroll-snap detection, click navigation, touch swipe:

```javascript
class PresentationController {
    constructor() {
        this.slides = document.querySelectorAll('.slide');
        // ... build dots, attach keyboard, observe slides
    }
}
```

Use `scroll-snap-type: y mandatory` on `<html>` and `scroll-snap-align: start` on
each slide so wheel scroll feels like keynote even without JS.

## What the user pushed back on (and how to anticipate)

1. **"那三个都太基础"** — the catalog Paper&Ink / Dark Botanical / Vintage Editorial
   previews all looked like PPT templates. They asked for "Gemini Canvas-level" quality.
   → Always offer a fourth, custom Cinematic preview when the deck has video assets.

2. **"侍臣的脸串成张飞"** — when iterating slide content, the user can spot character
   identity errors instantly.
   → Verify any AI-generated visuals before slotting them.

3. **"你为什么把视频也删了"** — destructive cleanup of old assets when "保留" was
   in the plan.
   → Never delete files even when refactoring. Move-to-archive instead.

4. **"我没让你做场景8"** — pre-emptively starting the next task.
   → Stop after each scene/slide and wait for explicit "continue".

5. **"署名改一下"** — author name corrections.
   → Confirm author name and title from user before generating; do not invent.

6. **"用 8081 我没开"** — preview server on a port the user can't reach.
   → Always reuse the existing public-facing port. Drop preview HTMLs into the
   directory already being served.

7. **"打个包给我"** — wants downloadable artifact.
   → Always offer a tarball with: HTML + actual referenced media + README.txt.
   Don't include the entire output directory; only what the HTML actually loads.
   `grep -oE '"(media-pattern)"' deck.html | sort -u` to enumerate dependencies.

## Reusable prompts to ask up front

When the user wants a "share / talk / pitch" deck:

1. "What's your hero asset?" (the finished thing — film, demo, screenshot)
2. "Who's the audience?" (sets formality and inside-baseball level)
3. "What's the throughline?" (origin → struggle → fix → result, or pure showcase)
4. "What's your accent color?" (project palette, used loud)
5. "Author name / title to credit?"
6. "Public port for preview?" (avoid using a port the user hasn't opened)

## Anti-patterns to avoid

- starting the deck on a content slide instead of an atmospheric hero
- using your accent color on every element (loses meaning)
- embedding video without a `poster=` or click-to-play overlay (autoplay invasive)
- generic stock photos when the user has their own visuals
- "professional" purple gradients that read as SaaS template
- writing five lines of body copy where a number + label would do
- showing every iteration uncritically; pick the 3 most instructive
