# Phase 1 - UI Review

**Audited:** 2026-05-04
**Baseline:** Abstract 6-pillar standards + Hamilton Jekyll theme
**Screenshots:** Not captured (Playwright browsers not installed)

---

## Pillar Scores

| Pillar | Score | Key Finding |
|--------|-------|-------------|
| 1. Copywriting | 3/4 | Good intro text, but photo alt text uses filenames |
| 2. Visuals | 3/4 | Clear hierarchy, map markers functional but small |
| 3. Color | 2/4 | Hardcoded colors diverge from theme skin system |
| 4. Typography | 4/4 | Follows theme typography correctly |
| 5. Spacing | 3/4 | Inline spacing adequate but inconsistent with theme units |
| 6. Experience Design | 2/4 | Missing loading states, error handling, and accessibility |

**Overall: 17/24**

---

## Top 3 Priority Fixes

1. **Hardcoded map marker colors** - Colors #28a745, #4a90d9, #ccc, #fff are not derived from theme variables. This breaks the skin system and causes visual inconsistency across light/dark modes. Replace with CSS custom properties mapped to theme colors.

2. **No loading state for external resources** - Leaflet CSS/JS and Lightbox2 are loaded from CDNs with no fallback or loading indicator. Users on slow connections see blank map area. Add loading states and consider local fallbacks.

3. **Non-descriptive photo alt text** - `alt="{{ photo.name }}"` uses filename as alt text. This fails accessibility requirements. Add a frontmatter field for alt text or derive from filename more intelligently.

---

## Detailed Findings

### Pillar 1: Copywriting (3/4)

**Strengths:**
- Hiking page has clear, descriptive intro: "A map of Korean mountains and national parks I've explored. Click on markers to see details."
- Map popup labels are clear: "Hiked", "Not visited", "To explore"
- Empty state message for photos is helpful: "Add photos to `/assets/photos/` to populate this gallery."

**Issues:**
- **BLOCKER:** Photography page alt text uses `{{ photo.name }}` which returns the filename (e.g., "IMG_2023" or "DSC0001"). This provides no meaningful information to screen readers.
  - File: `photography.md:16`
  - Fix: Add an `alt_text` field to photo frontmatter, or use a more descriptive pattern

- Photography intro is minimal: "A collection of my photographs." Could be expanded to explain the type of photography or subjects.

### Pillar 2: Visuals (3/4)

**Strengths:**
- Hiking page has clear visual hierarchy: title > description > map > list
- Map is the primary focal point at 400px height, full width
- Color-coded markers provide visual differentiation (green=hiked, blue=explore, gray=not visited)

**Issues:**
- **WARNING:** Map markers are only 12px diameter. On high-DPI or large screens, these may be difficult to see and click. Consider responsive sizing.
  - File: `hiking.md:59-60`
  - Impact: Mobile users may struggle with touch targets

- **WARNING:** Photo grid at 3 columns with 0.5em gap is tight. Consider increasing gap to 1em for better visual breathing room.
  - File: `photography.md:22`

- **WARNING:** Empty photo grid shows only text message with no visual placeholder or illustration. This could appear broken rather than intentionally empty.

### Pillar 3: Color (2/4)

**BLOCKER:** Hiking page uses hardcoded colors that bypass the Hamilton theme's skin system.

```javascript
// hiking.md:57-59
var c = m.ex ? '#ccc' : (m.h ? '#28a745' : '#4a90d9');
// ...
html: '<div style="background:'+c+';width:12px;height:12px;border-radius:50%;border:2px solid #fff;"></div>',
```

**Theme colors (daylight skin):**
- Text: `#111`
- Link: `#003be4`
- Border: `#828282` (base), lightened/darkened variants

**Hardcoded colors in hiking.md:**
| Color | Usage | Theme Equivalent |
|-------|-------|------------------|
| `#28a745` | Hiked markers | Not in theme palette |
| `#4a90d9` | To explore markers | Close to `$link-base-color: #003be4` but different |
| `#ccc` | Not visited markers | Not in theme palette |
| `#fff` | Marker border | Uses `$background-color: #fff` but hardcoded |

**Impact:** These colors will not adapt to the theme's skin system (sunrise/daylight/sunset/midnight). On dark-mode skins (midnight), the white borders and light gray markers will look jarring.

**Recommended fix:**
```javascript
// Use CSS custom properties that inherit from theme
var c = m.ex ? 'var(--text-color-light)' : (m.h ? 'var(--subscribe-color)' : 'var(--link-base-color)');
```

Or define CSS variables in custom-styles.scss for map-specific colors that can be overridden per-skin.

### Pillar 4: Typography (4/4)

**Strengths:**
- Both pages use the theme's typography system (Roboto Slab for content, Roboto for headings)
- No inline font-size or font-family declarations that would break the theme
- The page layout correctly uses `post-content` class which applies `font-family: $reading-font-family`

**No issues found.** Typography follows Hamilton theme conventions correctly.

### Pillar 5: Spacing (3/4)

**Strengths:**
- Uses theme's page layout with proper padding from `.post-content`
- Photo grid uses responsive design with mobile breakpoint

**Issues:**
- **WARNING:** Inline spacing values don't match theme's `$spacing-unit: 2rem` pattern.
  - `hiking.md:15`: `margin: 1em 0;` (theme uses 2rem multiples)
  - `photography.md:22`: `gap: 0.5em; margin: 1em 0;` (theme uses 2rem multiples)

- This is acceptable for component-specific styles but creates inconsistency if the theme's spacing rhythm is strict.

- **WARNING:** Map height is fixed at 400px. Consider using viewport-relative units for better responsiveness:
  - Current: `height: 400px;`
  - Better: `height: min(400px, 50vh);` or similar

### Pillar 6: Experience Design (2/4)

**BLOCKER:** No loading states for external resources.

Both pages load external CSS/JS from CDNs:
- `hiking.md`: Leaflet CSS + JS from unpkg.com
- `photography.md`: Lightbox2 CSS + JS from cdnjs.cloudflare.com

**Issues:**
1. **No loading indicator:** Users on slow connections see blank space before map/gallery renders.
2. **No error handling:** If CDN fails or is blocked, there's no fallback UI.
3. **No noscript fallback:** Users with JavaScript disabled see nothing.

**Accessibility issues:**
1. **Map is not accessible:** The `#hiking-map` div has no ARIA label, role, or text alternative. Screen readers cannot access the geographic information. Consider adding a text list or data table as alternative.
2. **Photo alt text is filename-based:** Already covered in Copywriting pillar.

**Positive findings:**
- Photo images use `loading="lazy"` for performance
- Map has attribution for OpenStreetMap
- Photo gallery has responsive grid (3 col desktop, 2 col mobile)
- Map marker popups provide contextual information

---

## Registry Safety

**No shadcn or third-party component registries detected.** This is a Jekyll static site using CDN-hosted libraries (Leaflet, Lightbox2). No NPM component registry audit required.

---

## Files Audited

| File | Purpose |
|------|---------|
| `hiking.md` | Hiking page source with Leaflet map integration |
| `photography.md` | Photography gallery page with Lightbox2 |
| `_sass/hamilton/variables.scss` | Theme spacing and font variables |
| `_sass/hamilton/base.scss` | Theme base styles |
| `_sass/hamilton/layout.scss` | Theme layout styles |
| `_sass/hamilton/skin.scss` | Theme color skin system |
| `_sass/hamilton/skins/daylight.scss` | Daylight skin color values |
| `_sass/hamilton/custom-styles.scss` | Custom style placeholder (empty) |
| `_layouts/page.html` | Page layout template |
| `_includes/header.html` | Header/navigation component |
| `_data/navigation.yml` | Navigation structure |
| `_config.yml` | Jekyll configuration |
| `_hikes/geumjeongsan.md` | Sample hike data file |

---

## Recommendations Summary

| Priority | Issue | Effort | Impact |
|----------|-------|--------|--------|
| HIGH | Replace hardcoded colors with theme variables | Medium | High |
| HIGH | Add meaningful alt text for photos | Low | High |
| MEDIUM | Add loading states for map and gallery | Medium | Medium |
| MEDIUM | Make map accessible to screen readers | Medium | High |
| LOW | Increase map marker size for touch targets | Low | Low |
| LOW | Increase photo grid gap | Low | Low |