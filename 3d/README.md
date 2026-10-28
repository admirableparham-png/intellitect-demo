# Hosted 3D demo page (M1 context and massing on a live basemap)

_As of 2026-10-28. Page: `docs/demo/3d/index.html`, data: `docs/demo/m1-context-locations.json` (open data only; no client data). Research and demonstration, not legal or engineering advice._

## What it shows
The three public plots of the walkthrough (Al Barsha Second, Al Khawaneej, Al Awir First) on a live 3D basemap: the plot outline, a massing block of chosen storeys and storey height [assumption], 50 m and 100 m circles, Dubai Municipality's official entrance points with Makani numbers, and sun shadows for any date and hour (Cesium's sun light driven by the clock; our own NOAA-class sun angles in the panel).

## Providers
| Provider | Status | What you get | Terms to log |
|---|---|---|---|
| Cesium ion (default) | needs an access token | Cesium World Terrain, Bing Maps aerial imagery, Cesium OSM Buildings (white blocks, heights only where OSM has them, so thin in villa communities) | Free (individual) plan: "individual projects and evaluation", "exploratory commercial or government development" allowed; 15 GB streaming, 1,000 imagery sessions a month; Commercial plan USD 149 a month (individual) or 524 (team) (cesium.com/platform/cesium-ion/pricing, read 2026-10-28) |
| Google Photorealistic 3D Tiles | not usable for Dubai | Textured 3D where Google has it | UAE shows 2D-only on Google's coverage page (last updated 2026-10-27); Cesium forum 2023-08-02 reports no Dubai buildings [third-party]. Policies if ever used: attribution kept visible, no caching or pre-fetching, no extraction or tracing from tiles, Enterprise SKU USD 6.00 per 1,000 events up to 100,000 a month, 1,000 free (Google pricing page, 2026-10-27) |

## Why the claude.ai artifact cannot do this
The artifact sandbox blocks every runtime request to other hosts, so live tiles need a page served from our own origin.

## Hosting
1. The page must be served over http(s) (it fetches `../m1-context-locations.json`). Opening the file directly does not work.
2. GitHub Pages: the main repo is private. GitHub's docs give conflicting statements on Pages for private repositories (Pro or Team feature lists vs. "publishing privately needs Enterprise Cloud"); a separate public repository holding only `docs/demo/3d/` and the open-data JSON avoids the question and exposes nothing confidential. Parham decides (rule 14: deploy nothing without him).
3. Restrict the Cesium ion token to the page's domain in the ion dashboard once the domain exists. Never commit a token; the page keeps it in the browser only.
4. Later: OCI Dubai static bucket, per the hosting plan.

## Checks before showing it
- Open the page, choose Cesium ion, paste the token, Load, then switch locations and play the day.
- The credits strip at the bottom must stay visible (Cesium and data providers); our "Data sources" box is separate from it on purpose.
