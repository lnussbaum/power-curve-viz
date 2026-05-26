# Power Curve Viewer

A single-page web application for visualizing cycling power curves. No build step or server required — runs entirely in the browser.

## Features

- Paste CSV data (compatible with [intervals.icu](https://intervals.icu) exports) to generate interactive power curve charts
- Toggle visibility of individual curves with color-coded checkboxes
- Filter by duration range and power range using sliders
- Switch between linear and logarithmic scales for both axes
- Export the chart as a 1920×1080 PNG
- Data is cached in localStorage so it persists between visits

## Usage

1. Open `index.html` in a browser
2. Paste your CSV data into the text area and click **Load Data**
3. Use the controls at the top to filter, toggle curves, and adjust scales

### CSV Format

The expected CSV format has:

- First column: `secs` (duration in seconds)
- Remaining columns: power values in watts for different time periods/conditions
- Missing values are represented as empty cells and are skipped during rendering

Example:

```csv
secs,This Season,Last Season
1,756,619
5,710,563
60,400,380
3600,250,240
```

## Architecture

- **Plotly.js** (loaded from CDN) handles chart rendering, hover tooltips, and zoom/pan
- All state (filters, visibility) is ephemeral; only raw CSV text is persisted in localStorage
- X-axis uses a two-tier tick system with cycling-friendly labeled durations (1m, 5m, 1h, etc.) and unlabeled minor ticks for accurate hover snapping
