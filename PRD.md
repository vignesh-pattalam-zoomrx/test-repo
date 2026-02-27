# PRD: Vignesh's Birthday Party Page

## 1. Overview

A single, self-contained static HTML page celebrating Vignesh's birthday. The page serves as a fun, shareable birthday party invitation that guests can open directly in any modern browser. All code (HTML, CSS, JavaScript) must live in **one file**: `index.html`.

---

## 2. Goals

| # | Goal |
|---|------|
| 1 | Create a visually festive, colorful birthday page for Vignesh |
| 2 | Display party details (date, time, venue) with easy-to-swap placeholders |
| 3 | Include fun interactive elements: countdown timer, confetti, and a birthday cake animation |
| 4 | Keep it dead simple — single HTML file, no build tools, no dependencies, no external CDNs |

---

## 3. Non-Goals

- No backend or server-side logic.
- No RSVP form or data collection.
- No external hosting setup (GitHub Pages, Netlify, etc.) — the file is opened locally.
- No frameworks, libraries, or package managers.

---

## 4. Technical Constraints

| Constraint | Detail |
|------------|--------|
| **Single file** | Everything in one `index.html` — inline `<style>` and `<script>` tags only |
| **Zero dependencies** | No CDN links, no npm, no external fonts or images. All assets must be CSS/SVG/JS-generated |
| **Browser support** | Must work in the latest versions of Chrome, Firefox, Safari, and Edge |
| **Responsive** | Must look good on both desktop (1920×1080) and mobile (375×812) viewports |
| **Performance** | Page must load instantly with no network requests. Total file size should stay under 50KB |

---

## 5. Page Structure & Sections

The page scrolls vertically. Sections appear in the following order from top to bottom:

### 5.1 Hero Section

- **Large heading**: "Happy Birthday, Vignesh!" in a bold, playful font (use a system font stack — no external fonts).
- **Subtitle**: "September 7" displayed below the heading.
- **Confetti animation**: On page load, trigger a CSS/JS confetti animation that rains colorful confetti particles down the screen for ~5 seconds. The confetti should use at least 5 bright colors (e.g., red, yellow, blue, green, pink).
- **Background**: A vibrant gradient background (e.g., warm tones — orange to pink, or yellow to coral).

### 5.2 Birthday Cake Animation Section

- **Animated birthday cake** built entirely with CSS (no images, no SVGs loaded from files — inline SVG or pure CSS shapes are fine).
- The cake must include:
  - **3 layers/tiers** in different colors (e.g., pink, purple, yellow).
  - **Candles on top** (at least 3 candles) with a flickering flame animation (CSS keyframes).
  - The flames should have a subtle glow effect.
- **Interaction**: When the user clicks/taps on the cake, the flames go out (disappear with a short fade-out animation) and a "Happy Birthday!" message appears above the cake with a pop-in animation. Clicking again should relight the candles (flames fade back in).

### 5.3 Countdown Timer Section

- **Heading**: "Countdown to the Party"
- **Countdown display**: Shows days, hours, minutes, and seconds remaining until the party date/time.
- **Target date/time**: Use a placeholder value that is clearly marked and easy to change. Set the default to `2026-09-07T18:00:00` (September 7, 2026 at 6:00 PM local time).
- **Behavior when countdown reaches zero**: Replace the countdown with a celebratory message: "The party is ON! Let's go!"
- **Visual style**: Each time unit (days, hours, minutes, seconds) should be displayed in its own rounded card/box with the number on top and the label below. Cards should have a colorful background.

### 5.4 Party Details Section

- **Heading**: "Party Details"
- Display the following fields in a clean card/list layout. Each field uses a **placeholder value** wrapped in square brackets so it's trivially easy to find-and-replace:

| Field | Placeholder Value |
|-------|-------------------|
| Date | `[Saturday, September 7, 2026]` |
| Time | `[6:00 PM onwards]` |
| Venue | `[Venue Name, Full Address]` |
| Dress Code | `[Casual / Festive Attire]` |
| BYOB | `[Yes / No]` |
| Special Notes | `[Any additional info for guests]` |

- Use icons or emoji prefixes for each field to make it scannable (e.g., a calendar emoji for date, a clock for time, a pin for venue).

### 5.5 Footer

- A simple footer with the text: "Made with love for Vignesh's birthday"
- Small, centered, muted color.

---

## 6. Design Specifications

### 6.1 Color Palette

| Role | Color | Hex |
|------|-------|-----|
| Primary background gradient start | Warm yellow | `#FFD700` |
| Primary background gradient end | Coral pink | `#FF6B6B` |
| Card background | White with slight transparency | `rgba(255, 255, 255, 0.9)` |
| Primary text | Dark charcoal | `#2D2D2D` |
| Heading text | Deep magenta | `#C2185B` |
| Accent 1 | Bright blue | `#2196F3` |
| Accent 2 | Vivid green | `#4CAF50` |
| Accent 3 | Sunny orange | `#FF9800` |

### 6.2 Typography

- **Font stack**: `'Segoe UI', 'Helvetica Neue', Arial, sans-serif`
- **Hero heading**: 3rem (desktop), 2rem (mobile), bold (700 weight)
- **Section headings**: 2rem (desktop), 1.5rem (mobile), semi-bold (600 weight)
- **Body text**: 1rem, regular (400 weight)
- **Countdown numbers**: 2.5rem, bold

### 6.3 Spacing & Layout

- Max content width: `800px`, centered with auto margins.
- Section vertical padding: `60px` (desktop), `40px` (mobile).
- Card border-radius: `16px`.
- Card box-shadow: `0 4px 15px rgba(0, 0, 0, 0.1)`.

---

## 7. Animations Detail

### 7.1 Confetti

- Generate **80–120 confetti pieces** using JavaScript on page load.
- Each piece is an absolutely-positioned small `<div>` (8–12px wide, randomized shape: square or rectangle).
- Randomize: color (from 5+ bright colors), horizontal start position, fall speed (3–6 seconds), rotation, and slight horizontal drift.
- Use CSS `@keyframes` for the fall + rotation animation.
- Confetti pieces should be removed from the DOM after their animation completes to avoid memory buildup.
- Confetti should appear to fall from the top of the viewport.

### 7.2 Cake Candle Flames

- Each flame is a small CSS shape (teardrop/oval using `border-radius`) colored in orange/yellow gradient.
- Flicker animation: subtle `scale` and `opacity` oscillation on a `0.3s` loop with slight randomized delay per flame so they don't flicker in sync.
- Glow effect: `box-shadow` with a warm orange/yellow spread.

### 7.3 Cake Click Interaction

- **Blow out**: Flames fade out over `0.5s` with `opacity: 0` and slight `scale(0)` transition. After fade-out, show a "Happy Birthday!" text above the cake that pops in (scale from 0.5 to 1 + fade in, `0.4s` ease-out).
- **Relight**: "Happy Birthday!" text fades out, flames fade back in over `0.5s`.
- Use a boolean state variable in JavaScript to toggle between lit/unlit states.

---

## 8. File Structure

```
test-repo/
├── index.html          <-- The single deliverable file
├── PRD.md              <-- This document
├── mysecondfile.txt    <-- Pre-existing file (do not modify)
```

No other files should be created.

---

## 9. Placeholder Reference

All placeholders that the user needs to customize before sharing:

| Placeholder | Location | What to Replace With |
|-------------|----------|---------------------|
| `2026-09-07T18:00:00` | Countdown timer JS | Actual party date and time in ISO format |
| `[Saturday, September 7, 2026]` | Party Details section | Actual party date |
| `[6:00 PM onwards]` | Party Details section | Actual party time |
| `[Venue Name, Full Address]` | Party Details section | Actual venue |
| `[Casual / Festive Attire]` | Party Details section | Actual dress code |
| `[Yes / No]` | Party Details section | BYOB policy |
| `[Any additional info for guests]` | Party Details section | Special notes or remove row |

---

## 10. Acceptance Criteria

The implementation is complete when ALL of the following are true:

- [ ] Single `index.html` file with zero external dependencies.
- [ ] Opens correctly in Chrome, Firefox, Safari, and Edge (latest versions).
- [ ] Hero section displays "Happy Birthday, Vignesh!" with confetti animation on load.
- [ ] Confetti uses 5+ colors, falls from top, and cleans up from DOM after animation.
- [ ] Birthday cake is rendered purely with CSS/inline SVG (no external images).
- [ ] Cake has 3 tiers, 3+ candles with flickering flame animations.
- [ ] Clicking the cake toggles candle flames on/off with smooth transitions.
- [ ] "Happy Birthday!" message appears when candles are blown out, hides when relit.
- [ ] Countdown timer counts down to the placeholder date, updating every second.
- [ ] Countdown shows days, hours, minutes, seconds in separate styled cards.
- [ ] When countdown reaches zero, it displays the celebration message.
- [ ] Party details section shows all 6 fields with their placeholder values.
- [ ] Page is responsive — looks good on both desktop and mobile viewports.
- [ ] Total file size is under 50KB.
- [ ] Footer text is present.
