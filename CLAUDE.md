# Mark Beaumont Website

Personal/speaker website for Mark Beaumont — adventurer, Guinness World Record holder, BBC broadcaster, author, and impact investor.

**Team:** Deborah (Manager), Yoyo (Research & Marketing), Ed (Partnership Manager)

---

## Project structure

```
MB web/
├── index.html          # Main site — single self-contained file
├── podcast.html        # Standalone podcast page
├── index-map.html      # Map prototype
├── card-map-v1–v5.html # Iterative map card prototypes
├── images/             # All photography
├── files/              # Static assets (one PNG)
├── podcast/            # Podcast section assets
├── backups/            # Manual backups (good.html, index 2.html, etc.)
└── web inspo/          # Reference/inspiration folder
```

**No build tools.** Pure HTML/CSS/JS — everything inline, no npm, no bundler, no framework. Google Fonts is the only external dependency. Edit files directly and open in a browser.

---

## Design system

CSS variables defined in `:root`:

| Variable | Value | Use |
|---|---|---|
| `--ink` | `#0D0D0D` | Near-black, body text |
| `--paper` | `#F0EDE6` | Warm off-white background |
| `--blue` | `#2B2BFF` | Primary accent, CTAs |
| `--yellow` | `#F5E642` | Secondary accent |
| `--white` | `#FFFFFF` | Clean white sections |
| `--mid` | `#888` | Subdued text |
| `--light` | `#E0DDD6` | Borders, dividers |
| `--r` | `20px` | Border radius |

**Font:** `Plus Jakarta Sans` — weights 300, 400, 500, 600, 700, 800. Always use this font, never substitute.

Typography pattern: headings at weight 800, `letter-spacing: -.04em`, `line-height: .9`. Kickers/labels at weight 700, `letter-spacing: .2em`, `text-transform: uppercase`, 9–11px. Body at weight 400, `line-height: 1.65–1.8`.

Sizing uses `clamp()` throughout for fluid responsive type and spacing. Mobile breakpoints at 480px, 600px, 768px, 900px.

---

## Page sections (index.html)

### Intro overlay
Full-screen blue overlay with MB logo SVG (clip path with 4 photos flying in from corners). Fades out on load. Respects `prefers-reduced-motion`.

### Card stack (`#cards-scroll`)
Five full-screen sticky cards, scroll-driven. Container is `height: 500vh`. JS uses cubic-bezier ease + `translateY` to animate cards off-screen as user scrolls.

| ID | Class | Theme | Content |
|---|---|---|---|
| `c0` | `.c0` | Blue (`--blue`) | Hero — "Mark Beaumont", MB logo watermark |
| `c1` | `.c1` | Dark split | "Two Lives" — Sport/Business 50/50 split with photos |
| `c2` | `.c2` | Yellow (`--yellow`) | "Fastest Around the World" — animated SVG world map + bicycle animation |
| `c3` | `.c3` | Dark photo overlay | "Backing Business" — finance/investor card |
| `c4` | `.c4` | Blue photo overlay | "Giving Back" — community/charity card |

### `#about` — white
2-col grid: left = bio text, stat pills, GWR achievement cards; right = portrait photo.

Stats: 100+ Countries, 18,000 Miles, 200+ Keynotes, £2M+ Raised.

### `#speaking` — dark (`--ink`)
Horizontally scrollable topic cards (drag-to-scroll on desktop). Speaker reel block below.

### `#testimonials` — paper
6 sticky notes in a 3-col grid. Click to bring forward (z-index). Each note has a colour theme (blue, yellow, dark — alternating).

### `#podcast` — white
Left: episode list + platform links (Spotify, Apple, etc.). Right: photo collage (hidden on mobile).

### `#how` — dark
Zigzag "How It Works" steps. Steps activate (opacity 1) as user scrolls past 84% of viewport height.

### `#contact` — white
Booking form (left) + team sidebar with fees card (right, hidden on mobile).

Speaking fees: UK £4,500–£6k · International £8k–£10k.

Team sidebar: Deborah (Manager), Yoyo (Research & Marketing), Ed (Partnership Manager).

### `#resources` — paper
Event resource download grid: Speaker Reel, Headshots, Bios & Rate Card.

### Footer + social sidebar
Footer: "Mark Beaumont" brand left, "Back to top" right.

Fixed social sidebar (right on desktop, bottom bar on mobile): LinkedIn, Instagram, YouTube, Facebook.

Custom cursor: 8px blue dot with `mix-blend-mode: multiply`. Hidden on touch devices.

---

## JS behaviours

All JS is inline at the bottom of each HTML file — no external scripts.

- **Card stack scroll** — RAF-throttled scroll listener, cubic-bezier easing, translateY per card
- **Bicycle animation (c2)** — triggers once when c2 is in view (scrolled 1.3–3× vh past wrap top)
- **Topics drag-scroll** — mousedown/mousemove/mouseup on `.topics-track`
- **How-it-works activation** — IntersectionObserver-style via scroll + getBoundingClientRect
- **Sticky notes z-index** — click any note to bring it forward
- **Podcast photo carousel** — `setInterval` at 4000ms, opacity fade between slides
- **Intro overlay** — plays on first load, classes `intro-exit` trigger CSS animations

---

## Image assets

All in `images/`. Naming is inconsistent — don't rename without checking all references.

- `JPEG image 2.jpeg`, `JPEG image 3.jpeg`, `JPEG image 4.jpeg`, `JPEG image 8.jpeg`
- `JPEG image 10.jpeg`, `JPEG image 14.jpeg`, `JPEG image 19.jpeg`, `JPEG image 20.jpeg`
- `JPEG image 21.jpeg`, `JPEG image 22.jpeg`, `JPEG image 26.jpeg`, `JPEG image copy.jpeg`
- `Slide 1.jpg` → `Slide 7.jpg` (also `Slide 8.jpg`)
- `Slide 5 (thumbail in podcast section).JPG` — note capitalised `.JPG`
- `1768933307293.png` — in `files/`, used as favicon/asset

Intro overlay uses: JPEG image 2, 20, 14, 3 (preloaded in `<head>`).

---

## Mark Beaumont — key facts (for copy accuracy)

- **Fastest cycle around the world:** 78 days · 14 hours · 40 minutes · 18,000 miles (2017)
- **World's Highest Marathon:** Atacama Desert, 2026
- BBC broadcaster, bestselling author, multiple Guinness World Record holder
- 100+ countries cycled through, 200+ keynotes delivered, £2M+ raised for charity
- **Investor/business:** 14 years Corporate Ambassador at LDC (UK's leading mid-market PE firm); 6 years Partner at Eos (healthcare & environmental sustainability); Operating Partner at Envoy Group
- **Charities:** My Name'5 Doddie Foundation (MND research — £1.6m raised in 2026), Action Medical Research (Ambassador 10+ years, donates 100% of keynote fees), The Archie Foundation

Social handles: LinkedIn `/in/mark-beaumont-47906728`, Instagram `@mrmarkbeaumont`, YouTube `@MrMarkBeaumont`, Facebook `MarkBeaumontAdventures`.

---

## Working conventions

- All CSS goes inside the `<style>` block in the `<head>` of each file
- All JS goes in `<script>` at the end of `<body>`
- Keep everything in one file per page — don't split into separate CSS/JS files
- Test by opening the HTML file directly in a browser (no server needed for most features)
- Before making significant changes to `index.html`, manually copy it to `backups/` first
- The card-map-v*.html files are prototypes/experiments — don't delete them, they're reference
