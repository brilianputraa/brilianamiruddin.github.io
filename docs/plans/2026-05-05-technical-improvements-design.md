# Technical Improvements Design

**Date:** 2026-05-05  
**Scope:** Performance, SEO, Analytics

## Overview

Improve site load time, search visibility, and user tracking through layered, low-risk optimizations.

## Section 1: Performance - Image Optimization

**Problem:** Site loads ~3.5MB of images on key pages:
- `me.jpg` (1.7MB) - profile photo, loads on every page
- `reference_layout.png` (1.8MB) - unused reference file
- Blog images range from 140KB-764KB each

**Fixes:**

1. **Profile photo compression**
   - Convert `me.jpg` to WebP at 80% quality
   - Target: ~200KB (8x reduction)
   - Keep original JPG as fallback

2. **Delete unused assets**
   - Remove `reference_layout.png`

3. **Lazy loading**
   - Add `loading="lazy"` to all `<img>` tags
   - Files: `_includes/sidebar.html`, `_layouts/post.html`

4. **Blog images**
   - Compress to max 400KB each
   - Use `<picture>` element with WebP source + JPG fallback

**Impact:** Homepage drops from ~2MB to ~300KB.

## Section 2: Performance - Fonts Optimization

**Problem:** 9 Google Font families loaded (~300KB), blocking render.

**Fixes:**

1. **Reduce to 4 families:**
   - `Open Sans` or `Roboto` - body text (pick one)
   - `Roboto Slab` - headings
   - `Inconsolata` - code
   - `Dancing Script` - site title
   
   Remove unused: Noto Sans SC, Noto Sans TC, Noto Serif SC, Noto Serif TC

2. **Add `display=swap`** to URL - renders text immediately

3. **Preload critical font** (optional)

**Impact:** Font load ~300KB → ~120KB, text visible faster.

## Section 3: Analytics - Google Analytics 4

**Problem:** GA tracking commented out.

**Fixes:**

1. Create GA4 property → get Measurement ID (`G-XXXXXXXXXX`)
2. Update `_config.yml`:
   ```yaml
   google_analytics: G-XXXXXXXXXX
   ```
3. Verify production deployment loads script

**Tracking goals:**
- Page views per post
- User locations
- Traffic sources
- Mobile vs desktop

## Section 4: SEO - Structured Data

**Problem:** Missing JSON-LD schemas.

**Fixes:**

1. **Person schema** in `_includes/head.html`:
   ```json
   {
     "@type": "Person",
     "name": "Brilian Putra Amiruddin",
     "email": "brilianamiruddin@pusan.ac.kr",
     "url": "https://brilianputraa.netlify.app/",
     "sameAs": ["github", "twitter", "scholar URLs"]
   }
   ```

2. **Article schema** in `_layouts/post.html`:
   ```json
   {
     "@type": "Article",
     "headline": "{{ page.title }}",
     "datePublished": "{{ page.date }}",
     "author": { "@type": "Person", "name": "{{ site.author }}" }
   }
   ```

## Implementation Summary

| # | Area | Task | Effort |
|---|------|------|--------|
| 1 | Performance | Compress `me.jpg` to WebP | 5 min |
| 2 | Performance | Delete `reference_layout.png` | 1 min |
| 3 | Performance | Add lazy loading | 10 min |
| 4 | Performance | Reduce fonts + display=swap | 5 min |
| 5 | Analytics | GA4 setup | 15 min |
| 6 | SEO | Person JSON-LD | 10 min |
| 7 | SEO | Article JSON-LD | 10 min |

**Files to modify:**
- `_config.yml`
- `_includes/head.html`
- `_layouts/post.html`
- `_includes/sidebar.html`
- `assets/images/me.jpg` → `me.webp`

**Total effort:** ~1 hour  
**Risk:** Low - all reversible