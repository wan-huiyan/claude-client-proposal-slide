# HTML Build Specifications

## Constraints to Pass to frontend-design

- **Format:** Self-contained HTML at 1280x720px (16:9 aspect ratio)
- **Purpose:** Client-facing proposal slide — premium, trustworthy, actionable
- **Tone:** Match to audience (executive = refined/minimal, operational = data-rich/structured)
- **The "recommended" action should use a warm accent (amber/gold)**
- **Must include `@media print` rules for PDF export**
- **Self-contained (all styles inline, Google Fonts via CDN)**

## Content Layout

- CSS Grid for the main layout
- Generous padding (44-56px edges)
- Clear section labels (uppercase, letter-spaced, colored)

## Data Visualization

- Horizontal bar charts for rate comparisons (simple CSS, no JS)
- Stat cards/pills for key numbers
- Progress bars for before/after comparisons

## Activation Section Styling

Use a different background shade, icon badges per stakeholder role, or a bordered
callout box for the "What This Means For Your Team" section.

## PDF Generation

### @media print rules (required in all HTML versions)

```css
@media print {
  .section, .card, .callout { break-inside: avoid; }
  p { break-inside: avoid; }
  h1, h2, h3 { break-after: avoid; }
  .activation-panel { break-inside: avoid; }
}
```

### Option A — puppeteer (if available)

```javascript
await page.pdf({
  path: outputPath,
  format: 'A4',
  printBackground: true,
  margin: { top: '15mm', bottom: '15mm', left: '12mm', right: '12mm' },
});
```

### Option B — Chrome headless (fallback, no npm install needed)

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu \
  --print-to-pdf="/absolute/path/to/output.pdf" \
  --no-pdf-header-footer \
  --print-to-pdf-no-header \
  "file:///absolute/path/to/input.html"
```

Key gotchas:
- Always use absolute paths for both --print-to-pdf and the HTML URL
- --no-pdf-header-footer is critical to avoid date/URL/page numbers
- CVDisplayLink errors on macOS are harmless — ignore them
- Prefer Option B when puppeteer is not pre-installed (npx puppeteer downloads ~300MB)
