# Story Sections & Light Mode Default — Design Spec

**Date:** 2026-04-14
**Status:** Approved

---

## Overview

Add two horizontal-sliding storytelling sections to the landing page that explain the problem Industrial IoT solves through a relatable factory scenario. Also switch the default theme to light mode.

**Target audience:** Non-technical factory owners and managers being demoed the product.

---

## 1. Default Light Mode

- Remove `dark` from `<html lang="en" class="dark scroll-smooth">` → `<html lang="en" class="scroll-smooth">`
- Add localStorage persistence to the theme toggle so the user's choice is remembered across visits

---

## 2. Section Order (updated)

1. Hero (existing)
2. **NEW — "Before" Story** (horizontal slideshow, red theme)
3. **NEW — "After" Story** (horizontal slideshow, green theme)
4. What is Industrial IoT? (existing)
5. The Problem (existing)
6. How It Works (existing)
7. ... remaining existing sections

The side navigation dots must be updated to include pointers to the two new sections.

---

## 3. "Before" Story Section

**Section heading:** "The Daily Reality Without Smart Monitoring"
**Subtitle:** "A story every factory manager knows too well"
**Accent color:** Red (`#ef4444`)

### Interaction

- Arrow-click slideshow (left/right arrow buttons on sides)
- One slide visible at a time, full viewport width
- Progress dots at the bottom showing current position
- No auto-advance — user controls the pace

### Slide Layout

- Side-by-side: illustration (image placeholder) on one side, text on the other
- **Alternating zigzag**: odd slides = image left / text right, even slides = text left / image right
- On mobile: stacks vertically (image on top, text below)

### Slides (7 total)

| # | Title | Text | Image Description |
|---|-------|------|-------------------|
| 1 | The Factory Floor | A busy factory with 20+ CNC machines. Operators at their stations. The hum of production. | Wide view of cartoon factory floor with many machines and workers |
| 2 | The Owner's Call | Owner picks up the phone and calls the manager: "How many machines are running right now? How many are switched off?" | Cartoon owner on phone with speech bubble asking about machine status |
| 3 | More Questions Pile Up | "Which batch is each machine working on? How many pieces are done? What about voltage and temperature?" The questions keep coming. | Multiple speech bubbles stacking up with different questions |
| 4 | The Manual Count | Manager puts down the phone, grabs a clipboard, and starts walking machine to machine. Checking each one. Asking operators. Writing on paper. | Cartoon manager with clipboard walking between machines, taking notes |
| 5 | Hours Pass... | The owner is still waiting. It's been 2 hours. Meanwhile, machines have changed status — some stopped, some started. The data is already stale. | Split scene: owner tapping watch impatiently on left, manager still walking around on right, clock showing 2+ hours |
| 6 | The Report Has Errors | Manager finally calls back with numbers. But 3 machines changed state while he was counting. The numbers don't add up. Owner is frustrated. | Manager presenting paper with numbers, red X marks on some, owner looking unhappy |
| 7 | Every. Single. Day. | This isn't a one-time problem. This is the daily reality. The manager dreads the owner's call. The owner can never trust the numbers. Decisions are based on guesswork. | Calendar with repeating cycle icons, stressed manager with head in hands |

---

## 4. "After" Story Section

**Section heading:** "Now Imagine This Instead..."
**Subtitle:** "Same factory, same questions — completely different experience"
**Accent color:** Green (`#10b981`)

### Interaction & Layout

Same as "Before" section: arrow-click slideshow, zigzag alternating layout, progress dots.

### Slides (6 total)

| # | Title | Text | Image Description |
|---|-------|------|-------------------|
| 1 | Same Question | Owner asks: "What's the factory status?" Same question as before. But this time, the answer is seconds away. | Cartoon owner asking casually, relaxed posture, same character as Before |
| 2 | Instant Answer | Manager pulls out his phone, opens the app. Within 5 seconds: "12 machines running, 3 idle, 2 in maintenance. Batch #47 is 78% complete." | Manager holding phone with visible dashboard screen, confident smile, speech bubble with precise numbers |
| 3 | Every Detail, One Tap | Tap any machine on the dashboard — see temperature, voltage, RPM, output count, batch info. All live data. No walking around needed. | Close-up of phone screen showing a machine detail card with stats |
| 4 | Owner Checks From Anywhere | The owner doesn't even need to call. He opens the same app from home, from his car, from the office. He sees everything the manager sees. Real-time, always accurate. | Owner sitting on couch/in car looking at phone, thought bubble showing factory dashboard |
| 5 | Alerts Come to You | Machine overheating? Unexpected shutdown? You get a notification instantly. Problems find you — you don't have to discover them. | Phone screen with notification popup "CNC-07 temperature critical!", alert bell icon |
| 6 | Confidence & Control | Every number is accurate. Every decision is data-driven. The owner trusts the reports. The manager is free to focus on real work, not counting machines. | Happy owner and manager standing together, dashboard screen in background showing green status |

---

## 5. Illustration Style

- **Style:** Friendly cartoon characters with sketch feel
- **Characters:** Consistent owner and manager characters across all 13 slides (same appearance, different expressions/poses)
- **Color palette:**
  - Before slides: warm tones with red accents for stress/frustration
  - After slides: cool tones with green/blue accents for confidence/ease
  - Characters use the brand blue (`#2a8bff`) and accent green (`#10b981`)
- **Background:** Simple, minimal — factory elements suggested rather than detailed
- **Expressions:** Key storytelling device — frustrated/stressed in Before, happy/confident in After
- **Format:** Each image should be roughly 16:9 or 3:2 aspect ratio to fit the side-by-side layout

---

## 6. AI Image Generation Prompts

All prompts use a consistent style prefix. Use these with Midjourney, DALL-E, Flux, or similar tools.

**Style prefix (prepend to every prompt):**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors,

### Before Slides

**Slide 1 — The Factory Floor:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, wide view of a busy factory floor with multiple CNC machines in rows, several cartoon workers standing at machines, industrial setting with warm lighting, overhead lamps, slight reddish warm tone, conveying a busy hectic atmosphere

**Slide 2 — The Owner's Call:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, a cartoon factory owner in a suit sitting at a desk talking on the phone with a serious expression, a large speech bubble showing questions like "How many machines running? How many OFF?", office setting with window showing factory in background

**Slide 3 — More Questions Pile Up:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, same cartoon factory owner on phone looking demanding, multiple speech bubbles stacking and overlapping with text like "Which batch?", "Output count?", "Temperature?", "Voltage?", bubbles getting larger and more overwhelming, reddish accent tones

**Slide 4 — The Manual Count:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, a cartoon factory manager wearing a hard hat carrying a clipboard and pen, walking between large CNC machines on a factory floor, looking down at clipboard writing notes, an operator nearby pointing at a machine, warm industrial tones

**Slide 5 — Hours Pass:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, split scene divided in the middle, left side shows cartoon owner impatiently tapping his watch looking annoyed, right side shows the manager still walking around the factory floor with clipboard looking tired, a large clock between them showing 2 hours have passed, warm reddish frustrated tones

**Slide 6 — The Report Has Errors:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, cartoon manager holding up a paper report with numbers on it, some numbers circled in red with X marks, cartoon owner standing opposite looking frustrated with arms crossed, red accent marks around incorrect numbers, tense atmosphere

**Slide 7 — Every Single Day:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, a cartoon calendar on the wall with every day marked with a repeating cycle icon, the cartoon manager sitting at desk with head in his hands looking exhausted, phone ringing with owner calling again, dark circles under eyes, stack of messy paper reports on desk, reddish tired tones

### After Slides

**Slide 1 — Same Question:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, same cartoon factory owner from before but now looking relaxed and casual, asking "What's the status?" with a small calm speech bubble, light blue and green tones, peaceful atmosphere, bright and airy feeling

**Slide 2 — Instant Answer:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, cartoon factory manager smiling confidently, holding up a smartphone showing a colorful dashboard with green status indicators, a speech bubble saying "12 running, 3 idle, Batch 78% complete", green accent tones, happy confident expression

**Slide 3 — Every Detail One Tap:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, close-up view of a cartoon hand holding a smartphone, the screen showing a machine detail card with icons for temperature, voltage, RPM, output count, all with green check marks, finger tapping the screen, blue and green accent colors, clean modern UI on screen

**Slide 4 — Owner Checks From Anywhere:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, cartoon factory owner sitting comfortably on a couch at home in casual clothes, smiling while looking at phone showing factory dashboard, a thought bubble above showing the factory with all machines running with green indicators, cozy home setting, green and blue peaceful tones

**Slide 5 — Alerts Come to You:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, a cartoon smartphone in the center with a large notification popup saying "Alert: CNC-07 Temperature Critical!" with a warning bell icon, small cartoon owner and manager on either side both looking at their phones with alert expressions but not panicked, orange alert accent with green background tones

**Slide 6 — Confidence & Control:**
> Friendly cartoon illustration, simple flat characters with expressive faces, clean sketch style, minimal background, soft pastel colors, cartoon factory owner and manager standing side by side smiling and giving thumbs up, behind them a large screen showing a factory dashboard with all green status indicators and charts trending upward, bright optimistic green and blue tones, celebratory atmosphere, clean and professional

---

## 7. Technical Implementation Notes

- Both story sections use the same reusable slideshow component
- Slideshow traps horizontal arrow key navigation when focused
- Smooth CSS transition between slides (slide-left / slide-right)
- Progress dots are clickable to jump to any slide
- Images are loaded lazily (only current + adjacent slides)
- On mobile (< 768px): side-by-side becomes stacked (image top, text bottom)
- Each section has `scroll-snap-align: start` like other sections
- Both sections need entries in the side navigation dots
