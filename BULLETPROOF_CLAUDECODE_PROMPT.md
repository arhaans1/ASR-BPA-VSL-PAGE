# CLAUDE CODE PROMPT — BulletProof Ads System Scrollytelling Page
# Paste this entire file as your prompt to Claude Code (Opus 4.6)
# ═══════════════════════════════════════════════════════════════

Build me a GROUNDBREAKING scrollytelling landing page as a single `index.html` file.
This must be genuinely unforgettable — not a standard marketing page with fade-ins.
Think: SBS "The Boat" meets a premium editorial brand meets a cinematic graphic novel.

This is for ASR Media Pro — a Meta advertising agency.
The page must make the viewer FEEL the pain of broken Meta ads through an immersive
narrative experience, then introduce the BulletProof Ads System as the salvation.

---

## THE CORE MECHANIC — TRUE SCROLLYTELLING

The page is divided into SCENES. Each scene is PINNED to the viewport.
Scrolling does NOT move the page up — it ADVANCES the story within each pinned scene.
The user's scroll wheel is a story timeline scrubber.

Use GSAP + ScrollTrigger (from CDN: https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js
and https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js)

Each scene has a `scrub: true` ScrollTrigger that animates elements as scroll progresses.
Between scenes, a brief transition (colour wash, character movement) bridges the gap.
The total scroll height should be approximately 600-700vh to give scenes enough room.

---

## THE CHARACTER — RAJAN

Rajan is the protagonist. He is a high-ticket coach in his 30s.
He must be drawn as an inline SVG character — not a photo, not a stock illustration.
Think: clean graphic novel line art. Minimal but expressive. Like a character from
"The Boat" or a high-end editorial illustration.

Rajan has THREE visual states that you must create as SVG variants:

**STATE 1 — STRESSED (Scenes 1-2)**
- Sitting at a desk, hunched forward
- Face: furrowed brow, visible tension lines on forehead
- One hand holding head, elbow on desk
- Screen glow illuminating his face from below (blue-white)
- The desk has a laptop/monitor showing a glowing screen
- Body language: defeated, confused, exhausted

**STATE 2 — REALISATION (Scene 3 — the pivot)**
- Same character, but sitting upright now
- Head tilted slightly, eyes wide — the "aha" expression
- One hand raised slightly, finger pointing up
- The screen glow shifts from blue-white to warm amber
- Body language: curious, engaged, something just clicked

**STATE 3 — CONFIDENT (Scenes 4-5)**
- Standing now, arms slightly open
- Face: calm, confident half-smile
- Light source from above (golden)
- Background has the faint 4-layer architecture blueprint behind him
- Body language: transformed, in control

SVG construction rules:
- Use simple closed paths for body shapes — no photorealistic detail
- Thick outlines (stroke-width 2-3px) in dark charcoal (#1a1a2e)
- Flat fills, minimal shading — 2-3 colours per body region maximum
- Face expressions done through simple path curves for eyebrows and mouth
- Character should be approximately 300px tall when rendered
- The character SVG must be inline in the HTML so it can be animated with GSAP
- Individual body parts (head, torso, arms, face elements) must have unique IDs
  so GSAP can tween them independently (e.g. #rajan-head, #rajan-brow-left,
  #rajan-mouth, #rajan-arm-right, #rajan-screen-glow)

---

## DESIGN SYSTEM

**Aesthetic:** Graphic novel meets premium editorial darkness.
High contrast. Cinematic. Like a Nolan film poster crossed with a Bloomberg Businessweek spread.
NOT a typical SaaS dark theme. NOT purple gradients. NOT generic.

**The unforgettable element:** The entire page feels like turning pages of a graphic novel
where YOU control the pacing with your scroll. The panels have visible comic-book style
borders that draw themselves. Text appears like caption boxes in a graphic novel.

**Typography:**
- Display: 'Bebas Neue' (Google Fonts) — for scene numbers, impact headlines
- Headlines: 'Syne' weight 800 (Google Fonts) — for main narrative text
- Body: 'DM Mono' weight 400 (Google Fonts) — for body copy, giving a technical/precise feel
- Caption boxes: 'DM Mono' italic — styled like actual graphic novel caption boxes

**Colour palette:**
```
--ink:        #0d0d0f    (near black — primary background)
--paper:      #f0ede6    (warm paper white — used for caption boxes)
--charcoal:   #1a1a2e    (character outlines, dark elements)
--accent:     #e8400c    (burnt orange-red — the "alarm" colour for pain scenes)
--gold:       #d4a017    (warm gold — the "solution" colour for resolution scenes)
--blue-dim:   #1e3a5f    (deep blue — screen glow, data elements)
--muted:      rgba(240,237,230,0.4)
--panel-bg:   rgba(240,237,230,0.04)  (subtle panel backgrounds)
--border:     rgba(240,237,230,0.08)
```

**The comic panel aesthetic:**
- Scene borders: 2px solid rgba(240,237,230,0.15) — draws itself via SVG stroke animation
- Caption boxes: rectangular divs with --paper background, dark ink text, slight drop shadow
  styled exactly like graphic novel caption boxes (top-left positioned, sharp corners)
- Scene transitions: brief full-screen colour flash (accent red for pain → gold for solution)
- Scanline texture: very subtle horizontal line texture overlay on dark scenes

---

## THE SCENES — DETAILED SPEC

### SCENE 0 — THE COVER (viewport height: 100vh, scroll budget: 80vh)

This is the "book cover" of the experience.

**Background:** Pure --ink. Subtle noise grain texture via CSS.

**Elements that animate on scroll progress (0% → 100% of scene's scroll budget):**

At 0% scroll:
- Page is empty except for a thin horizontal line across the centre
- Line colour: --accent

At 10% scroll:
- The horizontal line expands outward from centre to full width
- Then splits into a frame (top, bottom, left, right lines forming a rectangle)
- Frame is the outer border of the "comic panel"

At 25% scroll:
- Inside the frame, Rajan (STATE 1) fades in, positioned left-centre
- He appears in a "materialise" effect: starts as outline only, fill colours fade in

At 40% scroll:
- The headline types itself in, character by character (typewriter effect):
  Right side of frame: "THIS IS THE STORY OF RAJAN."
  Font: Bebas Neue, massive (clamp 60px-120px)
  Colour: --paper

At 60% scroll:
- Sub-headline fades in below: "He built a high-ticket coaching business."
- Then: "He did everything right with his Meta ads."
- Then: "And it broke anyway."
- Each line appears with 0.3s gap

At 80% scroll:
- A small caption box appears bottom-left:
  [CHAPTER 01 — THE COLLAPSE]
  styled exactly like a graphic novel chapter title box
  background: --accent, text: white

At 100% scroll:
- Scene transition: accent red wash sweeps across screen (left to right)
- Then reveals Scene 1

---

### SCENE 1 — THE GOOD DAYS (viewport: 100vh, scroll budget: 100vh)

**Background:** Dark --ink. Rajan STATE 1 at desk but relaxed version — not stressed yet.
Screen glows a healthy blue-green.

**Floating dashboard panel** (positioned like a comic book inset panel):
Dark glass card, top-right of scene. Contains:
```
CAMPAIGN STATUS: ACTIVE
━━━━━━━━━━━━━━━━━━━━━
Cost Per Lead    ₹298    ↓ GOOD
ROAS             4.8x    ↑ STRONG  
Show Rate        61%     ↑ SOLID
Qualified Leads  24      ↑ THIS WEEK
━━━━━━━━━━━━━━━━━━━━━
STATUS: [██████████] SCALING
```
Each metric counts up via GSAP when scene enters.

**Caption box top-left:**
"Monday morning. Everything is working."
"The leads are coming in. The sales team is happy."
"Rajan thinks he's finally cracked it."

**Narrative text right side (appears line by line):**
"₹298 a lead."
"4.8x return."
"This is the moment every high-ticket business dreams about."

**At 50% scroll through scene:**
Rajan's expression on screen subtly brightens (GSAP tween his mouth curve from neutral to slight smile)
Dashboard numbers all pulse gold once

**At 80% scroll through scene:**
Caption box changes (dissolve transition):
"He decides to scale."
"Because the numbers make sense."
"Because the margin is there."
"Because why wouldn't you?"

**At 100% scroll:**
Scene transition: the dashboard panel cracks — a single diagonal line appears across it
Sound note: (no actual sound needed, but the visual crack should feel audible)
Then smash-cut to Scene 2

---

### SCENE 2 — THE COLLAPSE (viewport: 100vh, scroll budget: 120vh)

This is the most VISCERAL scene. Maximum impact.

**Background:** Same desk, but now the screen light has gone red-orange (--accent glow).
Rajan morphs to STATE 1 STRESSED — GSAP tweens his posture: shoulders hunch,
head drops into hand, eyebrows furrow.

**The dashboard panel from Scene 1 returns — but BROKEN:**
Same position, same layout, but now:
```
CAMPAIGN STATUS: ⚠ CRITICAL
━━━━━━━━━━━━━━━━━━━━━━━━━━━
Cost Per Lead    ₹612    ↑↑ +106%
ROAS             1.9x    ↓↓ TANKING
Show Rate        22%     ↓↓ COLLAPSED
Qualified Leads  3       ↓↓ THIS WEEK
━━━━━━━━━━━━━━━━━━━━━━━━━━━
STATUS: [██░░░░░░░░] BREAKING DOWN
```
Numbers animate FROM the good values TO these bad values as the scene progresses.
The card has a red border glow pulsing.

**Caption boxes appear sequentially as user scrolls:**

Caption 1 (top-left, --accent background):
"Thursday."
"Nothing changed. Same creative. Same audience. Same budget."
"And yet."

Caption 2 (middle-right, dark background):
"CPL: doubled overnight."
"Show rate: collapsed."
"Sales team: asking questions he can't answer."

Caption 3 (bottom-centre, --accent background):
"He duplicates the ad set."
"Launches a new creative."
"His agency says: 'Give it time.'"

**WhatsApp message panel** (styled as an actual phone notification, floats in from right):
```
┌─────────────────────────────┐
│ 📱 Sales Team               │
│ ─────────────────────────── │
│ Bhai leads kahan hain?      │
│ Pipeline bilkul empty       │
│ ho gayi...                  │
│                    2:47 PM ✓✓│
└─────────────────────────────┘
```
Appears with a slide-in from right + subtle bounce

**At 60% scroll:**
Large text slams in — Bebas Neue, full width, --accent colour:
"YOUR FUNNEL DIDN'T BREAK."
Then below it:
"YOU RAN OUT OF READY BUYERS."

**At 85% scroll:**
Rajan's screen shows a flat line (EKG style) — the campaign flatlined.
A second flat line. A third.

**At 100% scroll:**
Caption box: [CHAPTER 02 — THE REAL REASON]
Scene transition: screen goes to static/noise for 0.3s, then clears to Scene 3

---

### SCENE 3 — THE DIAGNOSIS (viewport: 100vh, scroll budget: 100vh)

**Background:** Shifts slightly — less harsh, more clinical. Blue-dim tones.
Rajan transitions to STATE 2 REALISATION.

**This scene is split into two visual halves:**
Left half: Rajan looking at something
Right half: A "thought bubble" / diagram space showing the explanation

**The Awareness Pyramid builds itself as user scrolls:**
An SVG pyramid divided into 5 horizontal levels, drawn with stroke animation:

```
         ▲
        ╱ ╲         ← MOST AWARE (2-3%) — "READY TO BUY"
       ╱────╲       ← PRODUCT AWARE (5-8%) — "RESEARCHING"  
      ╱──────╲      ← SOLUTION AWARE (15%) — "EXPLORING OPTIONS"
     ╱────────╲     ← PROBLEM AWARE (30%) — "KNOWS THE PAIN"
    ╱──────────╲    ← UNAWARE (50%+) — "DOESN'T KNOW YET"
   ▼────────────▼
```

As each level draws in (bottom to top, as scroll progresses):
- A label appears next to it
- At the TOP level: a small circle/cursor highlights it with text:
  "YOUR ADS ONLY WORK HERE"
- Then an arrow points to all OTHER levels with:
  "META STARTS SHOWING YOUR ADS HERE WHEN YOU SCALE"
  "AND THESE PEOPLE ARE NOT READY."

**Caption boxes:**

Caption 1: "Meta's algorithm is brilliant. But it can't read minds."
Caption 2: "When you only optimise for 'Lead' — it finds people who LOOK like leads."
Caption 3: "Not people who ARE leads."
Caption 4: "The top 2% of your market was always finite."
Caption 5: "You burned through them. Now you're paying to reach the other 98%."
Caption 6: "And nobody told you this was happening."

**At 70% scroll:**
New panel appears — "THE REAL PROBLEM ISN'T CREATIVE. IT'S DATA."

Two columns appear:
```
WHAT META KNOWS          WHAT META NEEDS TO KNOW
─────────────────        ──────────────────────────
"This person clicked"    "This person qualified"
"This person booked"     "This person SHOWED UP"  
"This person registered" "This person BOUGHT"
"This person visited"    "This person STAYED"
```
Left column fills in all at once (--muted colour)
Right column fills in one by one (--gold colour) with a checkmark

**At 100% scroll:**
Caption box: [CHAPTER 03 — THE ARCHITECTURE]
Rajan's expression fully transitions to STATE 2 — the realisation
Scene transition: a golden light washes in from the right

---

### SCENE 4 — THE SYSTEM REVEAL (viewport: 100vh, scroll budget: 140vh)

**Background:** The colour palette shifts decisively. Darker ink, but now with warm gold
light source from the right side. Rajan has transitioned to STATE 3 CONFIDENT.
He stands to the left, facing right, looking at a large architectural diagram.

**The 4-Layer Blueprint reveals itself — this is the centrepiece of the page.**

The blueprint is an SVG architectural diagram — NOT a simple list or grid.
It looks like an actual engineering blueprint / system diagram:

```
BULLETPROOF ADS SYSTEM — ARCHITECTURE v1.0
══════════════════════════════════════════════════════

 COLD MARKET                                    SALE
 ──────────                                  ────────
     │                                           ▲
     ▼                                           │
 ┌─────────────────┐                             │
 │  LAYER 01       │   25% watch 25%+ video      │
 │  SIGNAL         │──────────────────────►      │
 │  FILTRATION     │   Exclude: bounced/ignored  │
 │  [65% budget]   │                             │
 └─────────────────┘                             │
          │                                      │
          ▼ Engaged audience only                │
 ┌─────────────────┐                             │
 │  LAYER 02       │   Belief shifts fire        │
 │  BELIEF         │──────────────────────►      │
 │  ARCHITECTURE   │   20-30 educational videos  │
 │  [25% budget]   │                             │
 └─────────────────┘                             │
          │                                      │
          ▼ Warm, conditioned audience            │
 ┌─────────────────┐                             │
 │  LAYER 03       │   Clean pixel signal ───────►
 │  CONVERSION     │──────────────────────►  QUALIFIED
 │  TRIGGER        │   Book call / webinar    BOOKED
 │  [10% budget]   │                             │
 └─────────────────┘                             │
          │                                      │
          ▼ Post-booking                         │
 ┌─────────────────┐                             │
 │  LAYER 04       │   Show-up rate 70%+ ────────►
 │  SHOW-UP        │──────────────────────►   SHOWED
 │  CERTAINTY      │   Authority + social proof   UP ──► SOLD
 │  [10% budget]   │                             
 └─────────────────┘                             
          │
          ▼ NEGATIVE SIGNALS EXCLUDED
 ┌─────────────────────────────────────────────┐
 │  PIXEL CONDITIONING ENGINE                  │
 │  ✗ No-shows excluded  ✗ Ghosts excluded     │
 │  ✗ Unqualified DQ'd   ✓ Buyers amplified    │
 └─────────────────────────────────────────────┘
```

Each box DRAWS ITSELF as the user scrolls — SVG stroke-dashoffset animation.
Connecting arrows draw themselves AFTER their source box completes.
Labels type in after boxes draw.

**Colour coding of layers:**
- Layer 01: blue-dim (#1e3a5f)
- Layer 02: mix of blue and gold
- Layer 03: gold (#d4a017)
- Layer 04: bright gold
- Pixel Conditioning: accent red border, then resolves to gold

**As each layer reveals, a caption box appears on the right:**

Layer 01 caption:
"Stop paying for curiosity."
"Layer 01 filters for genuine interest."
"Only engaged, intent-signalling prospects move forward."

Layer 02 caption:
"The objections killing your conversions are invisible."
"Layer 02 dismantles them systematically."
"20-30 belief-shift videos. 5 psychological angles."
"By the time they see your offer — they're already half-sold."

Layer 03 caption:
"Now you ask for the conversion."
"To an audience that is warm, educated, and ready."
"Not to strangers. Never to strangers again."

Layer 04 caption:
"Most funnels bleed revenue right here."
"The gap between 'booked' and 'showed up.'"
"Layer 04 floods every channel with reasons to attend."
"Show rates climb from 34% to 71%+."

Pixel Conditioning caption:
"This is the unlock nobody talks about."
"You're not just tracking who converts."
"You're teaching Meta who to AVOID."
"The algorithm gets smarter every single week."

**At 100% scroll of scene:**
The entire blueprint glows briefly — all borders light up gold simultaneously
Rajan's STATE 3 form is fully visible, looking at the completed blueprint
Caption box: [CHAPTER 04 — THE PROOF]

---

### SCENE 5 — THE PROOF (viewport: 100vh, scroll budget: 80vh)

**Background:** Slightly lighter than previous scenes. Feels like daylight breaking.
Rajan STATE 3 stands to the side, smaller, observing. The scene is dominated by data.

**3 large "result cards" appear one by one — each styled like a magazine data callout:**

Card 1 (appears at 20% scroll):
```
┌────────────────────────────────────┐
│                 12x                │
│        ━━━━━━━━━━━━━━━━━━━━        │
│  ROAS sustained over 90 days       │
│  without changing a single         │
│  creative. Structure did the work. │
└────────────────────────────────────┘
```
The "12x" counts up from 0 via GSAP.

Card 2 (appears at 50% scroll):
```
┌────────────────────────────────────┐
│                71%                 │
│        ━━━━━━━━━━━━━━━━━━━━        │
│  Show-up rate. Up from 34%.        │
│  In under 6 weeks.                 │
│  Layer 04 alone paid for itself.   │
└────────────────────────────────────┘
```

Card 3 (appears at 70% scroll):
```
┌────────────────────────────────────┐
│              ₹1,200                │
│        ━━━━━━━━━━━━━━━━━━━━        │
│  Cost per qualified sales call.    │
│  High-ticket coaching niche.       │
│  Not leads. Qualified calls.       │
└────────────────────────────────────┘
```

**Testimonial block** (appears at 85% scroll, centred):
Large quote marks (decorative, --gold, Bebas Neue, 200px) behind text:
"We'd tried three agencies before."
"This was the first time scaling didn't break everything."
Attribution: — Client, High-Ticket Coaching Programme

---

### SCENE 6 — THE INVITATION (viewport: 100vh, NO scroll budget — static final scene)

This scene is the landing after the scrollytelling journey. The "exhale" moment.
Clean. Simple. The ask.

**Background:** Pure --ink. Back to the beginning. Full circle.
But now a warm golden gradient bleeds in from the right edge — barely perceptible.

**Rajan STATE 3** appears small in the bottom-left corner — a final nod to the character.
He's just standing there. Done explaining.

**Centre of screen:**

Eyebrow (small caps, --gold, letter-spaced):
NO FLUFF. NO THEORY. NO HYPE.

Headline (Syne 800, large):
"12 minutes."
"The entire system."
"Watch it now."

Sub (DM Mono, muted):
"This video explains every layer of the BulletProof Ads System in full."
"At the end, if it makes sense for your business,"
"there's an option to work with us directly."

**Video placeholder** (16:9, centered, max-width 680px):
Dark card with:
- Radial gradient glow from centre (gold this time, not red)
- Large play button: gold circle, white triangle
- Pulse animation on play button
- Label: "The BulletProof Ads System — Full Reveal | 12 min"
- Duration badge: "12:04" top right
- Note in code: // REPLACE THIS WITH YOUR VSL EMBED (Wistia/Vimeo/YouTube iframe)

**CTA section below video:**

Primary CTA button:
- Full-width on mobile, centered on desktop
- Background: --accent
- Text: Syne 700, white: "Show Me If This Works For My Business →"
- On hover: slight scale up (1.02), brighter glow
- Box shadow: 0 0 40px rgba(232,64,12,0.4)

Sub-text below button:
"Free 30-min diagnostic. We map your funnel, find the leaks, show you the fix."
"No pitch unless there's a genuine fit."

**Three small trust indicators in a row:**
✓ High-ticket only   ✓ Meta specialists   ✓ 4-layer system

---

## NAVIGATION + CHROME

**Fixed top nav:**
- Logo left: "ASR MEDIA PRO" — Bebas Neue, letter-spaced, small
  with a thin accent-coloured underscore that animates in on load
- Right: Scene indicator — shows current chapter:
  "CH.01 / THE COLLAPSE" — updates as scenes progress
  This is a KEY design detail — it reinforces the graphic novel chapter feel
- Far right: Small "WATCH THE SYSTEM →" button, accent bordered

**Progress bar:**
- NOT a standard horizontal bar
- Instead: a vertical line on the RIGHT edge of the viewport
- Fills from top to bottom as user scrolls through the total page
- Colour: gradient from --accent (top) to --gold (bottom)
- Width: 2px
- This is subtle but premium — only power users will notice it

**Custom cursor:**
- Replace default cursor with a small crosshair cursor
- Inner dot: --accent colour
- On hover over interactive elements: cursor expands to a circle
- Implemented via a div that follows mouse position with requestAnimationFrame

**Chapter transition overlays:**
Between each scene, a full-viewport overlay briefly appears:
- A rectangle that slides in from left, fills screen, then slides out right
- Colour alternates: accent (pain scenes) / gold (solution scenes)
- Duration: 400ms in, 400ms out
- The chapter label ("CHAPTER 02") appears centred during the overlay

---

## TECHNICAL ARCHITECTURE

**Libraries (CDN only, no npm):**
```html
<!-- GSAP Core -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
<!-- ScrollTrigger Plugin -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Syne:wght@700;800&family=DM+Mono:ital,wght@0,400;1,400&display=swap" rel="stylesheet">
```

**GSAP ScrollTrigger setup pattern for each scene:**
```javascript
// Scene is pinned — scrolling advances the timeline, not the page
ScrollTrigger.create({
  trigger: "#scene-01",
  start: "top top",
  end: "+=800",        // scroll budget in pixels
  pin: true,
  scrub: 0.5,          // smooth scrubbing (0.5s lag = cinematic feel)
  anticipatePin: 1,
  onEnter: () => showChapterOverlay("CHAPTER 01", "THE COLLAPSE"),
});

// Scene timeline
const scene01 = gsap.timeline({
  scrollTrigger: {
    trigger: "#scene-01",
    start: "top top",
    end: "+=800",
    scrub: 0.5,
  }
});

// Then add tweens to the timeline:
scene01
  .from("#rajan-body", { opacity: 0, duration: 1 })
  .from("#dashboard-card", { x: 100, opacity: 0, duration: 0.8 })
  .to("#rajan-brow-left", { attr: { d: "stressed brow path" }, duration: 0.5 }, "+=0.3")
  // etc.
```

**SVG Character Animation pattern:**
```javascript
// Rajan's individual parts get tweened via GSAP attr tweens
gsap.to("#rajan-mouth", {
  attr: { d: "M85,95 Q100,88 115,95" },  // sad mouth path
  duration: 0.4,
  ease: "power2.inOut"
});
gsap.to("#rajan-brow-left", {
  rotation: -15,
  transformOrigin: "right center",
  duration: 0.4
});
// Screen glow colour shifts
gsap.to("#rajan-screen-glow", {
  fill: "#e8400c",
  duration: 0.6
});
```

**SVG stroke animation for blueprint:**
```javascript
// Get total path length and animate
const paths = document.querySelectorAll('.blueprint-path');
paths.forEach(path => {
  const length = path.getTotalLength();
  gsap.set(path, { strokeDasharray: length, strokeDashoffset: length });
});
// Then in scene timeline:
scene04.to('.blueprint-box-01 path', {
  strokeDashoffset: 0,
  duration: 1,
  stagger: 0.1,
  ease: "power2.inOut"
});
```

**Typewriter effect:**
```javascript
function typeWriter(element, text, duration) {
  gsap.to({}, {
    duration: duration,
    onUpdate: function() {
      const progress = this.progress();
      element.textContent = text.slice(0, Math.floor(progress * text.length));
    }
  });
}
// Called within scene timeline at specific position
```

**Chapter transition overlay:**
```javascript
function showChapterOverlay(number, title) {
  const overlay = document.getElementById('chapter-overlay');
  const tl = gsap.timeline();
  tl.set(overlay, { display: 'flex', x: '-100%' })
    .to(overlay, { x: '0%', duration: 0.35, ease: 'power3.in' })
    .to(overlay, { x: '100%', duration: 0.35, ease: 'power3.in', delay: 0.3 })
    .set(overlay, { display: 'none' });
}
```

**Scene structure HTML pattern:**
```html
<div id="scene-01" class="scene">
  <!-- Fixed background layer -->
  <div class="scene-bg"></div>
  <!-- Character layer -->
  <div class="scene-character">
    <!-- Inline SVG Rajan -->
  </div>
  <!-- Content layer — elements animated by GSAP -->
  <div class="scene-content">
    <div class="caption-box" id="s01-caption-01">...</div>
    <div class="dashboard-card" id="s01-dashboard">...</div>
    <!-- etc -->
  </div>
</div>
```

**CSS base for scenes:**
```css
.scene {
  width: 100vw;
  height: 100vh;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Caption box — graphic novel style */
.caption-box {
  background: var(--paper);
  color: var(--charcoal);
  font-family: 'DM Mono', monospace;
  font-size: 14px;
  line-height: 1.6;
  padding: 12px 16px;
  border-left: 3px solid var(--charcoal);
  max-width: 280px;
  position: absolute;
  /* Each caption box is absolutely positioned within its scene */
  box-shadow: 4px 4px 0 rgba(0,0,0,0.4);
  opacity: 0;  /* starts hidden, GSAP animates in */
}

/* Blueprint box style */
.blueprint-box {
  border: 1px solid rgba(212,160,23,0.4);
  background: rgba(212,160,23,0.03);
  padding: 16px 20px;
  position: absolute;
  font-family: 'DM Mono', monospace;
  font-size: 12px;
  color: var(--gold);
}
```

---

## MOBILE HANDLING

On screens < 768px:
- ScrollTrigger pinning still works but reduce scroll budgets by 40%
- Rajan character scales to 60% of desktop size
- Caption boxes stack vertically, reduce max-width to 90vw
- Blueprint diagram simplifies to a vertical flow (layers stack top to bottom)
- Two-column layouts become single column
- Font sizes: use clamp() throughout

---

## COMPLETE COPY — ALL SCENES

### Scene 0 (Cover):
Typewriter text: "THIS IS THE STORY OF RAJAN."
Sub-lines: "He built a high-ticket coaching business." / "He did everything right with his Meta ads." / "And it broke anyway."
Chapter label: [CHAPTER 01 — THE COLLAPSE]

### Scene 1 (Good Days):
Caption 1: "Monday morning. Everything is working. / The leads are coming in. The sales team is happy. / Rajan thinks he's finally cracked it."
Narrative: "₹298 a lead." / "4.8x return." / "This is the moment every high-ticket business dreams about."
Caption 2: "He decides to scale. / Because the numbers make sense. / Because the margin is there. / Because why wouldn't you?"

### Scene 2 (Collapse):
Caption 1: "Thursday. / Nothing changed. Same creative. Same audience. Same budget. / And yet."
Caption 2: "CPL: doubled overnight. / Show rate: collapsed. / Sales team: asking questions he can't answer."
Caption 3: "He duplicates the ad set. / Launches a new creative. / His agency says: 'Give it time.'"
Impact text: "YOUR FUNNEL DIDN'T BREAK." / "YOU RAN OUT OF READY BUYERS."
WhatsApp: "Bhai leads kahan hain? Pipeline bilkul empty ho gayi..."

### Scene 3 (Diagnosis):
Caption 1: "Meta's algorithm is brilliant. But it can't read minds."
Caption 2: "When you optimise for 'Lead' — it finds people who LOOK like leads."
Caption 3: "Not people who ARE leads."
Caption 4: "The top 2% of your market was always finite."
Caption 5: "You burned through them. Now you're paying to reach the other 98%."
Caption 6: "And nobody told you this was happening."
Panel label: "THE REAL PROBLEM ISN'T CREATIVE. IT'S DATA."

### Scene 4 (System Reveal):
Layer 01 caption: "Stop paying for curiosity. / Layer 01 filters for genuine interest. / Only intent-signalling prospects move forward."
Layer 02 caption: "The objections killing your conversions are invisible. / Layer 02 dismantles them. Systematically. / 20-30 belief-shift videos. 5 psychological angles. / By the time they see your offer — they're already half-sold."
Layer 03 caption: "Now you ask for the conversion. / To an audience that is warm, educated, and ready. / Not to strangers. Never to strangers again."
Layer 04 caption: "Most funnels bleed revenue right here. / The gap between 'booked' and 'showed up.' / Layer 04 floods every channel with reasons to attend. / Show rates: 34% → 71%+."
Pixel caption: "This is the unlock nobody talks about. / You're not just tracking who converts. / You're teaching Meta who to AVOID. / The algorithm gets smarter every single week."

### Scene 5 (Proof):
Card 1: "12x / ROAS sustained over 90 days / without changing a single creative. / Structure did the work."
Card 2: "71% / Show-up rate. Up from 34%. / In under 6 weeks. / Layer 04 alone paid for itself."
Card 3: "₹1,200 / Cost per qualified sales call. / High-ticket coaching niche. / Not leads. Qualified calls."
Testimonial: "We'd tried three agencies before. This was the first time scaling didn't break everything."

### Scene 6 (Invitation):
Eyebrow: "NO FLUFF. NO THEORY. NO HYPE."
Headline: "12 minutes. The entire system. Watch it now."
Sub: "This video explains every layer of the BulletProof Ads System in full. At the end, if it makes sense for your business, there's an option to work with us directly."
CTA: "Show Me If This Works For My Business →"
Sub-CTA: "Free 30-min diagnostic. We map your funnel, find the leaks, show you the fix. No pitch unless there's a genuine fit."

---

## FINAL INSTRUCTION TO CLAUDE CODE

Build this as a single `index.html` file.
Every line of CSS inline in `<style>`.
Every line of JS inline in `<script>`.
GSAP and Google Fonts loaded from CDN only.

The Rajan SVG character MUST be fully drawn — do not use a placeholder rectangle.
Draw him with actual SVG paths: head, body, arms, desk, screen, face expression elements.
Each element must have an ID for GSAP animation.

The blueprint diagram MUST be drawn as SVG with animatable stroke paths.
The awareness pyramid MUST be drawn as SVG.
The WhatsApp notification MUST be styled as an actual phone notification UI.
The dashboard cards MUST have monospace font, proper table-like layout with dividers.

Do not simplify. Do not use placeholders. Do not say "add your content here."
Build the complete, final, production-ready experience as described.

This page will be seen by high-ticket business owners spending ₹5L-50L/month on ads.
It must be the most impressive marketing page they have ever seen.
It must make them feel: "Someone finally understands my exact problem."
It must make them think: "This agency is operating at a completely different level."

Output only the complete index.html. Nothing else.
