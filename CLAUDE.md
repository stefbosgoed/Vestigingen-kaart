# CLAUDE.md - AI Assistant Guide for Vestigingen-kaart

## Project Overview

**Vestigingen-kaart** (Dutch for "Locations Map") is an interactive web application that displays store locations for **Sani4All** and **Kitchen4All** retail chains across the Netherlands. The map also shows potential expansion locations on a shortlist.

- **Primary Language**: Dutch (UI/content), English (code)
- **Target Audience**: Business stakeholders reviewing store locations and expansion planning
- **Live Deployment**: Static HTML file, can be hosted on any web server or GitHub Pages

## Tech Stack

| Technology | Purpose | Version |
|------------|---------|---------|
| HTML5 | Page structure | - |
| CSS3 | Styling (embedded) | - |
| JavaScript | Interactivity (embedded) | ES6+ |
| Leaflet.js | Interactive mapping | 1.9.4 |
| OpenStreetMap | Map tiles | - |

## Project Structure

```
Vestigingen-kaart/
├── index.html      # Single-page application (all code embedded)
├── README.md       # Brief project description
└── CLAUDE.md       # This file - AI assistant guide
```

### index.html Architecture

The application is a single HTML file with three main sections:

1. **`<style>` block (lines 8-233)**: All CSS styling
   - Brand colors: `#77041c` (primary red), `#ce1537` (Kitchen4All), `#1a2e34` (Sani4All), `#f39c12` (shortlist)
   - Responsive design with mobile breakpoint at 768px
   - Custom marker styling for map

2. **HTML structure (lines 235-275)**: Page layout
   - Header with branding
   - Legend explaining marker colors
   - Map container (`#map`)
   - Locations list (`#locationsList`)
   - Info box

3. **`<script>` block (lines 278-473)**: JavaScript application logic
   - **Location data** (lines 291-339): Array of store objects with `name`, `city`, `type`, `status`
   - **City coordinates** (lines 342-373): Lat/lng lookup for Dutch cities
   - **Marker rendering** (lines 389-435): Custom Leaflet markers
   - **Location cards** (lines 438-466): Clickable list items that zoom to markers

## Key Data Structures

### Location Object
```javascript
{
  name: "Sani4All Amsterdam",    // Store display name
  city: "Amsterdam",            // City for coordinate lookup
  type: "sani4all",             // One of: "sani4all", "kitchen4all", "shortlist"
  status: "Actieve vestiging",  // Status text (Dutch)
  brand: "Sani4All"             // (optional) Only for shortlist items
}
```

### Location Types
- `sani4all`: Existing Sani4All stores (dark blue-gray: `#1a2e34`)
- `kitchen4all`: Existing Kitchen4All stores (red: `#ce1537`)
- `shortlist`: Potential expansion locations (orange: `#f39c12`)

## Development Workflow

### Running Locally
No build step required. Simply open `index.html` in a browser or use a local server:

```bash
# Python 3
python -m http.server 8000

# Node.js (npx)
npx serve .

# Then open http://localhost:8000
```

### Making Changes

**Adding a new location:**
1. Add a new object to the `locations` array (around line 291)
2. If the city doesn't exist, add coordinates to `cityCoordinates` (around line 342)

**Changing brand colors:**
- Update `typeColors` object (line 376)
- Update corresponding CSS classes (`.marker-*`, `.type-*`)

**Adding a new location type:**
1. Add color to `typeColors` object
2. Add label to `typeLabels` object
3. Add CSS classes for `.marker-{type}`, `.type-{type}`
4. Add legend item in HTML

### Testing
- Manual testing in browser
- Check responsive design at different viewport sizes
- Verify all markers appear at correct coordinates
- Test click interactions (cards zoom to markers)

## Code Conventions

1. **No build tools**: Keep as single HTML file with embedded CSS/JS
2. **Dutch content**: All user-facing text is in Dutch
3. **English code**: Variable names, comments in English
4. **Brand consistency**: Follow Kitchen4All/Sani4All brand colors
5. **Mobile-first responsive**: Ensure functionality on mobile devices

## External Dependencies

All loaded from CDN (unpkg.com):
- Leaflet CSS: `https://unpkg.com/leaflet@1.9.4/dist/leaflet.css`
- Leaflet JS: `https://unpkg.com/leaflet@1.9.4/dist/leaflet.js`
- Map tiles: OpenStreetMap (free, no API key required)

## Common Tasks for AI Assistants

### Adding New Store Locations
```javascript
// Add to locations array:
{ name: "Brand City", city: "City", type: "sani4all|kitchen4all|shortlist", status: "Actieve vestiging" }

// If new city, add coordinates:
"CityName": [latitude, longitude]
```

### Updating Styling
- All styles are in the `<style>` block at the top of index.html
- Brand colors are defined both in CSS and JavaScript - keep them in sync

### Modifying Map Behavior
- Map initialization: line 280 (`L.map('map').setView([52.2, 5.5], 7)`)
- Default zoom: 7 (overview of Netherlands)
- Click zoom: 11 (city level)

## Notes

- The map is centered on the Netherlands at coordinates [52.2, 5.5]
- Location counts in legend (~22 Sani4All, ~20 Kitchen4All) are approximate and hardcoded
- No backend/API - all data is embedded in the HTML file
- Attribution for OpenStreetMap is required and included
