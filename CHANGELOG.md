# Changelog

All notable changes to **SMVDU Green Atlas** (formerly **SMVDU Floris**) are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [3.1.1] - 2026-10-19

### Added
- **Rebrand to SMVDU Green Atlas**: Transitioned platform branding from *SMVDU Floris* across all five HTML pages, navigation headers, footers, `manifest.json`, and `SECURITY.md`[cite: 4]. Added a centred **GREEN ATLAS** wordmark to the sticky, scroll-aware navigation header[cite: 4].
- **Expanded & Verified Flora Catalogue**: Increased total records from 116 to **175 taxa** (`SMVDU-FL-001` through `SMVDU-FL-175`) across **69 documented families**, adding 59 new verified entries (`FL-117` to `FL-175`) and a per-record `verified` flag covering 73 records[cite: 4].
- **Verified Filtering & Datasheet Exports**: Added a **Verified Only** quick toggle, dynamic sector/habit dropdown filters, an **Unknown / Not assessed** toxicity filter, a separate **Verified CSV** export action, and bundled `master-datasheet.csv` (175 records) and `verified-datasheet.xlsx` (73 records)[cite: 4].
- **Local QR Generation**: Added locally vendored `js/qrcode.min.js` (`qrcode-generator` v1.4.4) for offline-first QR code generation and 4×6 printable botanical plaques, keeping the remote QR API strictly as a fallback[cite: 4].
- **WGS84 Geodesy & Campus Boundary**: Added GeographicLib (`v1.52.1`) ellipsoidal geodesy calculations for sector and campus areas/perimeters, a distinct campus boundary polygon, a retractable map legend, fullscreen mode, a **Clear** pinpoint button, and sector deep linking (`maps.html?sector=…`)[cite: 4].
- **Evidence-Based Ecological Audit**: Added a data-scope and limitations notice to `research.html`, live data-derived metrics, a sector composition table (including an *Unassigned* row), a 6-phase field survey timetable, interactive plant hovercards, and one-click institutional citation copying with `aria-live` feedback[cite: 4].
- **Safety Disclaimer & Unknown Toxicity Tier**: Added a clinical-limitation notice and a fourth **Unknown / Not assessed** toxicity tier to `safety.html` so missing values are never defaulted to *Safe*[cite: 4].
- **PWA Icon Suite**: Added 10 physical favicon, Apple touch, and PWA icon assets under `icons/` (`32×32`, SVG, Apple touch icon, and `72` to `512 px` PNGs)[cite: 4].
- **Security Hardening**: Implemented an enforcing `Content-Security-Policy` meta tag and `strict-origin-when-cross-origin` referrer policy across all five pages, plus SHA-512 Subresource Integrity (`SRI`) attributes on Font Awesome, Leaflet, MarkerCluster, and GeographicLib[cite: 4].

### Changed
- **Home Page Architecture**: Redesigned the hero into a stacked "SMVDU / Green Atlas" title with the tagline *Identify – Document – Map – Connect* and contained release telemetry cards, removing IndexedDB initialization from the landing page to speed up initial load[cite: 4].
- **Modular GIS Architecture**: Split the monolithic `js/maps.js` into `js/maps-core.js` (map setup, WGS84 geodesy, layers, markers) and `js/maps-controls.js` (sector controls, accessibility, export, pinpoint, session restore), retaining `js/maps.js` as a documentation stub[cite: 4].
- **GeoJSON Export**: Upgraded GeoJSON export to respect the active sector filter and include sector polygons, the campus boundary polygon, area/perimeter properties, and generation metadata alongside flora points[cite: 4].
- **IndexedDB Schema & Migration (v4)**: Upgraded `SMVDU_BIO_INDEXED_DB` to schema version 4 with a verification index, automatically relocating legacy user observations with IDs `117+` to prevent collisions with the 59 new seed records[cite: 4].
- **CSV Export Hardening**: Upgraded CSV generation to 16 columns with full text quoting, doubled internal quotes, spreadsheet formula-injection prefixing (`=`, `+`, `-`, `@`), UTF-8 BOM encoding for Dogri script compatibility, and Blob-based downloads[cite: 4].
- **Accessibility & Responsive Design**: Expanded ARIA attributes across the site from 20 to 184, added 25 `:focus-visible` style rules, skip links, `aria-current` navigation states, modal focus trapping, inert backgrounds, `prefers-reduced-motion` support, native `<details>`/`<summary>` hazard cards, and horizontal table scroll hints[cite: 4].
- **Service Worker Cache**: Bumped service worker cache to `smvdu-green-atlas-v3.1.1`, caching the new icon set, local QR library, and split GIS modules while removing the unused `html5-qrcode` dependency[cite: 4].

### Fixed
- **Unsupported Research Claims**: Removed unsubstantiated hardcoded claims from `research.html` (1,420 tCO₂e/yr sequestration, 3.18 Shannon–Wiener index, 14.2% invasive pressure, "PEER REVIEWED" badge, and 6/6 survey completion)[cite: 4].
- **Data Coercion & Observation Validation**: Stopped coercing missing toxicity to *Safe* or missing IUCN status to *Least Concern*; removed fallback coordinates from observation intake in favor of strict global/campus bounds validation, duplicate-entry warnings, image MIME/size validation (`10 MB` cap), and confirmed IndexedDB write reporting[cite: 4].
- **XSS & Injection Prevention**: Replaced unescaped HTML notification injection in the map controller with `textContent` and enforced HTML escaping across table rows, map popups, hazard cards, hovercards, and print plaques[cite: 4].
- **Medical Emergency Dialler**: Updated the SMVDU Medical Centre link on `safety.html` to `+91 1991 285524` without automatic DTMF pause dialling (`,,2222`), instructing callers to request extension `2222` manually[cite: 4].

---

## [2.3.0] - Baseline Release (SMVDU Floris)

### Added
- **5-Page Static PWA Architecture**: Built a zero-build progressive web app (`index.html`, `database.html`, `maps.html`, `research.html`, `safety.html`) with a web app manifest (`manifest.json`) and offline service worker (`sw.js`, cache `smvdu-floris-v2.3.0`) featuring network-first navigation, cache-first static assets, and a dedicated ArcGIS tile cache (`smvdu-floris-gis-tiles-v2`)[cite: 4, 5].
- **116-Taxa Master Botanical Dataset**: Curated 116 georeferenced vascular plant records (`SMVDU-FL-001` to `SMVDU-FL-116`) across 60 botanical families spanning four ecological zones (*Pine Ridge Belt*, *Academic Avenue*, *Lower Scrublands*, and *Ravine Corridors*) with scientific names, Dogri vernacular names, phenology, IUCN status, and toxicity metadata[cite: 4, 5].
- **IndexedDB Storage Engine (`js/data.js`)**: Implemented `SMVDU_BIO_INDEXED_DB` (v2) with in-memory synchronous caching, automatic baseline seeding, live telemetry aggregation, and client-side field observation persistence[cite: 5].
- **Herbarium Database & Plaque Engine (`database.html`, `js/database.js`)**:
  - 15-item paginated ledger with live search and multi-facet filtering (Sector Zone, Plant Habit, Toxicity Profile)[cite: 5].
  - Specimen detail inspection modal and dedicated QR code modal with `?q=ID` deep linking[cite: 5].
  - Field observation intake form with one-tap HTML5 Geolocation GPS capture and client-side canvas image resizing/compression (`1600px` HD JPEG)[cite: 5].
  - Printable 4×6 inch physical botanical plaque generator (`@page` print layout) and full-catalogue CSV export[cite: 5].
- **Interactive Vegetation GIS Atlas (`maps.html`, `js/maps.js`)**:
  - Leaflet (`v1.9.4`) and Leaflet.markercluster (`v1.5.3`) map with Street, Satellite, and Topographic ArcGIS basemaps[cite: 5].
  - Interactive sector polygons with geodesic area/perimeter calculations, collapsible Sector Inspector sidebar, coordinate pinpoint dropper, GeoJSON point export, and 24-hour `localStorage` session recovery toast[cite: 5].
- **Sustainability Audit & Safety Triage (`research.html`, `safety.html`)**:
  - Ecological sampling methodology overview, sector biomass breakdown, 6-phase DYD Batch of 2026 survey timetable, and click-to-select institutional citation box[cite: 5].
  - Clinical toxicity filter pills (*Safe*, *Mild Irritant*, *Toxic*), searchable hazard profile cards with active chemical compounds and first-aid actions, exposure triage table, and SMVDU Medical Centre quick-call action[cite: 5].
- **Theme & Navigation System (`css/style.css`, `js/main.js`)**: Implemented instant light/dark theme loading (`smvdu_floris_theme`) with OS `prefers-color-scheme` detection, cross-tab storage sync, retractable navigation drawer, and smooth page transitions[cite: 5].
