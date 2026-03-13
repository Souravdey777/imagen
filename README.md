# ✨ ImaGen: Card Studio

A sleek, browser-based card generator for creating stunning social media quote cards with live preview and one-click export. Built with vanilla HTML, CSS, and Canvas API — zero dependencies, zero build step.

![Card Studio Preview](https://img.shields.io/badge/Status-Live-1C86FF?style=flat-square) ![License](https://img.shields.io/badge/License-MIT-green?style=flat-square) ![Zero Dependencies](https://img.shields.io/badge/Dependencies-0-333?style=flat-square)


---

## 🎯 What It Does

Card Studio lets you design professional quote cards for LinkedIn, Twitter/X, and Instagram — directly in your browser. Type your text, tweak the typography, and export in seconds.

**Perfect for:** content creators, dev advocates, personal branding, and anyone who posts text-based visuals on social media.

---

## ⚡ Features

- **Live Canvas Preview** — see every change rendered in real-time on a 720×720 canvas
- **Gradient Text** — wrap any text in `**double stars**` and it renders with a blue-to-teal gradient
- **Text Alignment** — left, center, or right alignment with icon toggle buttons
- **Font Size Control** — adjustable from 14px to 64px
- **Author Footer** — editable name + website with circular avatar
- **Multi-line Support** — each line becomes a new row; empty lines create visual spacing
- **One-Click Export** — download as JPG (default), PNG, or SVG via a split button with format dropdown
- **Responsive Layout** — editor panel + live preview side-by-side on desktop, stacked on mobile

---

## 🖼️ Card Anatomy

```
┌──────────────────────────────────┐
│  ┌────────────────────────────┐  │
│  │                            │  │
│  │   Great **code reviews**   │  │  ← Editable text with
│  │   do more than find bugs.  │  │    gradient syntax
│  │                            │  │
│  │   They build better devs.  │  │
│  │                            │  │
│  │  ───────────────────────── │  │  ← Gradient divider
│  │  (avatar) Name             │  │
│  │           website.com      │  │  ← Author footer
│  └────────────────────────────┘  │
│         Blue → Teal gradient BG  │
└──────────────────────────────────┘
```

---

## 🚀 Getting Started

No install, no build, no dependencies.

```bash
# Clone the repo
git clone https://github.com/yourusername/imagen-card-studio.git

# Open it
open index.html
```

Or just drag `index.html` into your browser. That's it.

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Rendering | HTML5 Canvas API |
| Styling | Vanilla CSS with custom properties |
| Typography | Google Fonts (Poppins) |
| Export | `canvas.toDataURL()` for JPG/PNG, SVG string builder for vector export |
| Avatar | Base64-embedded PNG (no external requests) |

**Zero runtime dependencies.** The entire app is a single self-contained HTML file.

---

## 📐 Architecture

```
index.html (single file)
├── CSS
│   ├── Design tokens (CSS variables)
│   ├── Layout (header, panel, preview grid)
│   ├── Components (inputs, buttons, dropdown, toast)
│   └── Animations (ambient orbs, entrance transitions)
├── HTML
│   ├── Editor panel (textarea, controls, export)
│   └── Live preview (canvas)
└── JavaScript
    ├── State management (reactive object)
    ├── Canvas renderer (draw function)
    ├── Text parser (**gradient** syntax)
    ├── Alignment engine
    ├── Export (JPG/PNG via offscreen canvas, SVG builder)
    └── UI interactions (dropdown, alignment, toast)
```

Key design decisions:
- **Single `draw()` function** renders to any canvas context — preview and export share the exact same code path
- **Config objects** (`CARD`, `FOOTER`, `COLORS`) hold all layout constants — change dimensions in one place
- **No framework overhead** — vanilla DOM manipulation for a sub-100KB total page weight

---

## ✏️ Gradient Text Syntax

Wrap any word or phrase in double asterisks to apply the signature blue-to-teal gradient:

```
Build solutions, not just **code**.
```

Renders as: "Build solutions, not just" in white + "code." in gradient.

Multiple gradient segments per line are supported:

```
**Great engineers** write **great tests**.
```

---

## 📤 Export Formats

| Format | Use Case | How |
|--------|----------|-----|
| **JPG** | Social media posts, quick sharing | Rasterized from canvas at 720×720 |
| **PNG** | Higher quality, transparency support | Rasterized from canvas at 720×720 |
| **SVG** | Scalable, editable in design tools | Generated markup with proper gradients and `text-anchor` |

All exports are client-side — nothing is uploaded to any server.

---

## 🎨 Customization

### Changing the avatar

Replace the base64 data URL in the `AVATAR` constant with your own. To generate one:

```bash
# Resize to 84x84 and convert to base64
python3 -c "
from PIL import Image
import base64, io
img = Image.open('your-photo.png').resize((84,84), Image.LANCZOS)
buf = io.BytesIO()
img.save(buf, format='PNG')
print(f'data:image/png;base64,{base64.b64encode(buf.getvalue()).decode()}')
"
```

### Changing the card colors

Edit the `COLORS` object in the script:

```javascript
const C = {
  w: '#FFFFFF',      // Text color
  url: '#bbbbbb',    // URL color
  blue: '#1C86FF',   // Primary gradient stop
  teal: '#5ADDCF',   // Secondary gradient stop
  card: '#000000'    // Card background
};
```

### Changing the card dimensions

Edit the `CARD` and `FOOTER` config objects:

```javascript
const CARD = { x: 60, y: 60, w: 600, h: 600, r: 16, pad: 59 };
const FOOTER = { divY: 555, cx: 140, cy: 600, r: 21, tx: 172, ny: 594, uy: 614 };
```

---

## 🌐 Browser Support

Works in all modern browsers that support Canvas API and CSS custom properties:

- Chrome 80+
- Firefox 78+
- Safari 14+
- Edge 80+

---

## 📄 License

MIT — use it, fork it, make it yours.

---

## 👤 Author

**Sourav Dey**
Senior Frontend Engineer · Building in public around AI + Engineering

[Souravdey.space](https://Souravdey.space)

---

<p align="center">
  <sub>Built with ✨ and vanilla JavaScript</sub>
</p>
