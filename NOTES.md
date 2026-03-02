# Focus by Khad — Project Notes
> Last updated: March 2, 2026
> This file captures all key decisions, creative choices, and technical context for the portfolio site.
> Read this at the start of any new session to get up to speed fast.

---

## 🌐 Site Overview
- **URL:** focusbykhad.com
- **Repo:** https://github.com/Khad94/focusbykhad.git
- **Hosting:** Netlify (auto-deploys on every `git push origin main`)
- **Domain registrar:** Porkbun
- **Stack:** Pure HTML / CSS / Vanilla JS — no frameworks, no build step
- **Languages:** EN / FR (JS i18n switcher, localStorage persistence)

---

## 📁 Project Structure
```
Portfolio Claude/
├── index.html          ← entire site (single file)
├── .gitignore          ← excludes originals, .DS_Store, serve.py, .claude/
├── NOTES.md            ← this file
├── ROADMAP.md          ← task tracking (optional)
└── images/
    ├── sports/
    │   └── baseball/
    │       └── web/    ← web-optimized baseball photos
    ├── street/
    │   ├── New York/
    │   │   └── web/    ← web-optimized NY street photos
    │   └── Barcelona/
    │       └── web/    ← web-optimized BCN street photos
    ├── portraits/      ← still Unsplash placeholders
    └── product/
        └── web/        ← web-optimized product photos
```

**Important:** Full-res originals are on a separate SSD (gitignored). Only web-optimized versions are in the repo.

---

## 🖼 Gallery — All Photos

### Sports / Baseball
| File | Title | Notes |
|------|-------|-------|
| KHS08813.jpg | **The Gates** | Exterior gates — opens the series (first in order) |
| KHS08814.jpg | **The House** | The stadium |
| KHS08994.jpg | **Lights On** | Night game lights |
| KHS08995.jpg | **Eye in the Sky** | Aerial/elevated view |
| KHS09012.jpg | **After the Storm** | Post-rain atmosphere |

> Football photos exist but not yet added. Need subfolder + sub-filter button.

### Street / New York
| File | Title | Notes |
|------|-------|-------|
| KHS00006.jpg | **The Crown** | Empire State spire above brick corner — portrait |
| KHS06766.jpg | **Downtown** | Dark subway platform, purple light — portrait |
| KHS06834.jpg | **The Exchange** | NYSE building, columns + flags — portrait |
| KHS07106.jpg | **The Concourse** | Grand Central main hall B&W from balcony — landscape |
| KHS07125.jpg | **The Square** | Times Square at night, dark crowd — landscape |
| KHS07432-3.jpg | **Rush** | Panning shot, white Chevy truck in midtown — landscape |
| KHS07827_-_BW.jpg | **The Grid** | B&W Manhattan skyline at night from above — landscape |
| KHS08534.jpg | **First Light** | Brooklyn Bridge + Lower Manhattan, golden hour — wide landscape |
| KHS08601-4.jpg | **Two Bridges** | Same vantage as First Light but full night, light trails — landscape |
| KHS09412.jpg | **Air Traffic** | Helicopter against blue sky — square |
| KHS09513.jpg | **Sweet** | Domino Sugar refinery Williamsburg at dusk — portrait |
| KHS09534.jpg | **Amber** | Brooklyn Bridge tower silhouetted orange sunset — near-portrait |
| KHS09548.jpg | **Orange Line** | Staten Island Ferry at dusk — landscape |
| KHS09634.jpg | **The Other Side** | Jersey City skyline at purple sunset — landscape |
| KHS08685.jpg | **The Avenue** | NYC street — added March 2026 |
| KHS09729.jpg | **The Bravest** | FDNY — added March 2026 |
| KHS09733.jpg | **Engine 26** | Fire station — added March 2026 |

> First Light and Two Bridges are same vantage point (Manhattan Bridge looking toward Brooklyn Bridge) but different times of day. Kept both intentionally.

### Street / Barcelona
| File | Title | Notes |
|------|-------|-------|
| KHS09863.jpg | **L'Escapada** | Piaggio scooter panning shot, summer 2023 — Catalan title |

> "L'Escapada" = Catalan for "the escape/getaway". Chosen over Spanish "La Escapada" intentionally.

### Product
| File | Title | Notes |
|------|-------|-------|
| Biere_KHS00006.jpg | **Noir** | Dark beer bottle |
| KHS06242_v2.jpg | **G-Shock** | G-Shock watch |
| Nike_Blazer_77_-_Normal_Size_(no_crop).jpg | **The 77** | Nike Blazer 77 sneaker |

### Portrait
> Still 4 Unsplash placeholders. Real photos not yet added.

---

## 🔧 Technical Setup

### Filter System
Two-level filter: category → subcategory
- `applyFilters(cat, sub)` handles all filtering logic
- Separate state: `activeSubSports` and `activeSubStreet`
- Separate NodeLists: `sportsSfBtns` and `streetSfBtns`
- Sub-filter bar uses CSS `max-height` + `opacity` transition with `.visible` class

### i18n (EN/FR)
- Single JS object `translations` with `en` and `fr` keys
- `applyLang(lang)` swaps text via:
  - `data-i18n` → `textContent`
  - `data-i18n-html` → `innerHTML`
  - `data-i18n-placeholder` → `placeholder`
  - `.g-cat` elements translated by reading parent's `data-category`
- Language saved in `localStorage`
- `EN · FR` toggle in nav

### Favicon
- File: `favicon.svg` (32×32, rounded rect)
- Dark background `#0a0a0a`, white "F" in Poppins Bold 700, gold dot `#c9a84c`
- Linked in `<head>` as `type="image/svg+xml"`

### Image Protection
- Right-click blocked globally via `contextmenu` → `preventDefault()`
- Android long-press blocked via same `contextmenu` event (Android fires it on long-press)
- iOS long-press blocked via `-webkit-touch-callout: none` on `.g-item` and `img`
- Drag-save blocked via `dragstart` → `preventDefault()` on `.g-item`
- `pointer-events: none` on `img` — image element doesn't receive touch/pointer events directly
- `user-select: none` + `-webkit-user-select: none` on `.g-item` and `img`

### Git / Deploy
- GitHub → auto-deploy on every push to `main`
- Web photos are force-added (`git add -f`) to override .gitignore
- .gitignore blocks `images/**/**/*.jpg` to prevent accidental push of full-res originals
- **Hosting:** migrating Netlify → Cloudflare Pages (unlimited bandwidth, free)
  - Pages project: `focusbykhad.pages.dev`
  - DNS on Cloudflare (nameservers: aaron + saanvi)
  - Custom domain `focusbykhad.com` added — verifying
  - ⚠️ Once verified: delete site from Netlify

---

## 🎨 Creative Decisions

### Removed
- **Merch section** — deactivated (code commented out), may return later
- **Hero eyebrow** ("Photography & Design") — removed entirely after Design/Merch was dropped

### FR Copy Choices
- "Travaux" → **"Photos"** (nav link, more direct)
- "Le Travail" → **"Mes Photos"** (section title)
- "Me Contacter" → **"Contact"** (simpler)
- "conteur visuel" removed — just **"photographe"** (cleaner, less corporate)
- "mémorisé" → **"immortalisé"** (stronger closing word in contact copy)
- Street category: **"Urbain"** (not "Rue" — more sophisticated)
- Stats: **"Histoires"** (not "Récits")

### Hero
- Title: `FOCUS. by Khad`
- Subtitle (EN): `Sports · Street · Portrait`
- Subtitle (FR): `Sport · Urbain · Portrait`
- Background: **Two Bridges** (`KHS08601-4.jpg`) — full night shot, Manhattan Bridge vantage looking toward Brooklyn Bridge + Lower Manhattan, light trails

### About Section
- Photo: still Unsplash placeholder → **to be replaced**
- EN bio: "I'm Khad — a photographer and visual storyteller..."
- FR bio: "Moi c'est Khad — photographe. Mon objectif s'installe dans l'énergie et l'émotion du sport..."

---

## ⏳ Pending / To-Do

- [ ] **Portrait photos** — replace 4 Unsplash placeholders with real shots
- [ ] **Football photos** — add subfolder, photos, Baseball/Football sub-filter buttons
- [ ] **About photo** — replace Unsplash placeholder with real photo of Khad
- [x] **Hero background** — set to Two Bridges (KHS08601-4.jpg) ✓
- [ ] **Social links** — Behance and LinkedIn still `#`
- [ ] **Hosting** — Cloudflare Pages set up, domain verifying → delete Netlify when confirmed ⚠️

---

## 💾 Conversation Backup
The raw Claude Code conversation file lives at:
```
/Users/khad/.claude/projects/-Users-khad-Documents-Portfolio-Claude/0c5db68b-5de6-459a-b35a-0522bb25b7f0.jsonl
```
It's ~22MB. Back it up to iCloud or your SSD if you want to preserve the full history.
To read it in a new session: `cat` the file or reference it via the path above.
