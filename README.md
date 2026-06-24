# Ocean Chlorophyll-a

A worldwide map of ocean chlorophyll-*a* built on NASA satellite imagery.
Pick a sensor and date, optionally average over a week or month, and compare
two dates as a difference map.

It's a **single static file** (`index.html`) — no build step, no server, no API
keys. Just open it or upload it anywhere that serves static files.

## What it does

- **Sensors:** MODIS-Aqua (2002–), VIIRS NOAA-20 (2017–), PACE OCI (2024–), via NASA GIBS.
- **More layers:** sea-surface temperature & anomaly (GHRSST/MUR), NOAA Coral Reef
  Watch (SST, DHW, bleaching alerts), significant wave height (WaveWatch III,
  2017–), and ocean depth / bathymetry (SRTM30+).
  - *Ocean depth* is **hybrid**: a stored ~0.2° image paints the overview
    instantly (offline), and live full-resolution (~1 km) WMS tiles load from
    PacIOOS when you zoom in (z5+, where tiles are small and fast). Click any
    point for depth, read instantly from a local ~0.1° grid.
  - *Wave height* map tiles come from PacIOOS ERDDAP (sometimes offline); point
    values + trends always work, sourced from the global WaveWatch III model.
- **Averaging:** single day, or weekly / monthly composites computed in the
  browser (per-pixel geometric mean of the cloud-free days), which fills gaps
  from clouds and missing passes.
- **Compare dates:** tick *Compare with another date* to show log₁₀(A ÷ B) on a
  diverging blue–white–red scale — red = higher at A, blue = lower. Respects the
  averaging setting, so you can compare two months or two years.
- **Change over last 7 / 30 days:** the *Change* dropdown maps the difference
  between the selected date and 7 (or 30) days earlier — a quick "how has it
  shifted lately" view. Same diverging scale; combine with weekly/monthly
  averaging to fill cloud gaps.
- **Fixed color scale** so colors are comparable across dates.

## Run locally

Just open `index.html` in a browser. (It loads map tiles from NASA over the
internet, so you need a connection.)

## Deploy (easiest path — Cloudflare, ~15 min, ~$10/yr)

1. Create a free account at <https://dash.cloudflare.com>.
2. **Buy the domain:** *Domain Registration → Register Domains* (at-cost pricing,
   free Whois privacy).
3. **Host:** *Workers & Pages → Create → Pages → Upload assets* and drag in this
   folder. It deploys to a `*.pages.dev` URL instantly.
4. **Attach the domain:** in the Pages project → *Custom domains → Set up a
   domain*. DNS and HTTPS configure automatically because the domain is already
   in Cloudflare.

**No-domain instant share:** drag this folder onto <https://app.netlify.com/drop>
for an immediate public URL.

## Credits

Imagery from NASA's Global Imagery Browse Services (GIBS) / EOSDIS; chlorophyll
products processed by the NASA Ocean Biology Processing Group (OB.DAAC). Map by
[Leaflet](https://leafletjs.com). Not affiliated with or endorsed by NASA.

Weekly/monthly averages are derived from NASA's color-coded image tiles, not
source data values — intended for visualization and education, not quantitative
or navigational use. For research-grade data use
[NASA Giovanni](https://giovanni.gsfc.nasa.gov) or the
[NASA Ocean Color](https://oceancolor.gsfc.nasa.gov) archive.
