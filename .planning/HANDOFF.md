---
name: trail-map-implementation
description: Handoff notes for adding Korea Trail GPX data to hiking map
type: project
---

# Trail Map Implementation - Handoff Notes

## Status: In Progress

### Completed
1. **Netlify deployment fix** - Added `csv` gem for Ruby 3.4 compatibility, created `netlify.toml` with Node.js 18
2. **Updated hiking.md** - Added Hallyeohaesang, Byeonsanbando, and 9 more national parks to hiked list
3. **Added Trailing section** - Haeparanggil courses 1-4, Namparanggil courses 2,4,5 completed
4. **API key obtained** - Durunubi API key saved in `.env` file (already in .gitignore)
5. **GPX files downloaded** - All 7 completed trail courses downloaded to `/tmp/`

### Remaining
1. Parse GPX files to extract lat/lng coordinates
2. Add trail polylines to hiking.md Leaflet map
3. Style trails (green for completed, not overshadowing mountain markers)
4. Reorganize project folder structure

---

## Key Files and Locations

### API Key
```
File: .env
Key: DURUNUBI_API_KEY=f2fb09a106dae44c90cc0c1865c7eb9b845e2fffd59d50bd1ed6a585cc8fa3d9
```

### GPX Files (downloaded to /tmp/)
| Trail | Course | File |
|-------|--------|------|
| Haeparanggil | 1 | `/tmp/hae1.gpx` |
| Haeparanggil | 2 | `/tmp/hae2.gpx` |
| Haeparanggil | 3 | `/tmp/hae3.gpx` |
| Haeparanggil | 4 | `/tmp/hae4.gpx` |
| Namparanggil | 2 | `/tmp/nam2.gpx` |
| Namparanggil | 4 | `/tmp/nam4.gpx` |
| Namparanggil | 5 | `/tmp/nam5.gpx` |

### API Endpoints
```
Course List: https://apis.data.go.kr/B551011/Durunubi/courseList
Params: serviceKey, MobileOS=ETC, MobileApp=hiking-blog, _type=json
Route List: https://apis.data.go.kr/B551011/Durunubi/routeList
```

---

## Implementation Guidance

### How to parse GPX and add to map

GPX format is XML with `<trkpt lat="..." lon="...">` elements. Parse with:

```python
import xml.etree.ElementTree as ET

def parse_gpx(filepath):
    tree = ET.parse(filepath)
    root = tree.getroot()
    points = []
    for trkpt in root.findall('.//trkpt'):
        lat = float(trkpt.get('lat'))
        lon = float(trkpt.get('lon'))
        points.append([lat, lon])
    return points
```

### Add to Leaflet map in hiking.md

After the mountain markers code block, add:

```javascript
// Trail polylines - completed courses (green)
var trailStyle = {
  color: '#28a745',
  weight: 3,
  opacity: 0.7,
  dashArray: '5, 5'  // dashed line so markers remain visible
};

// Haeparanggil courses 1-4
var hae1Coords = [...]; // parsed from /tmp/hae1.gpx
L.polyline(hae1Coords, trailStyle).addTo(map).bindPopup('해파랑길 1코스');

// Repeat for other courses...
```

### Trail styling to not overshadow mountains
- Use `opacity: 0.6-0.7` (semi-transparent)
- Use `dashArray: '5, 5'` (dashed line)
- Z-index: trails should render below markers (Leaflet default)
- Color: green (#28a745) matches hiked marker color

---

## Folder Reorganization

Current structure is messy. Proposed organization:

```
/
├── _posts/          # Blog posts (keep)
├── _projects/       # Project collection (keep)
├── _hikes/          # Hike collection (keep)
├── _data/           # Data files (keep)
├── _layouts/        # Layouts (keep)
├── _includes/       # Includes (keep)
├── _sass/           # Sass partials (keep)
├── assets/
│   ├── images/      # All images
│   ├── css/         # Compiled CSS
│   └── js/          # JavaScript (if any)
├── pages/           # Static pages (hiking.md, projects.md, etc.)
├── _config.yml
├── Gemfile
├── netlify.toml
└── .env             # API keys (already gitignored)
```

Files to move:
- `hiking.md`, `projects.md`, `about.md`, `publications.md`, `traveling.md`, `faq.md`, `docs.md`, `categories.md`, `tags.md`, `years.md` → `pages/`
- `me.jpg`, `favicon.PNG`, `reference_layout.png` → `assets/images/`

---

## Commits Made (on patch-1 branch)

1. Fix Netlify deployment for Ruby 3.4 compatibility
2. Add Hallyeohaesang and Byeonsanbando to hiked national parks
3. Add Trailing in Korea section with completed coastal trail courses
4. Remove external link from trailing section
5. Update hiked national parks list (added 9 more)
6. .gitignore updated to include `.env`

---

## Next Session Prompt

```
Resume work on trail map implementation. GPX files are in /tmp/ (hae1-4.gpx, nam2/4/5.gpx). 
Parse them and add polylines to hiking.md map. Use dashed green lines at 0.7 opacity.
Then reorganize folder structure per HANDOFF.md.
```