---
theme: seriph
title: "Coding Café – #30DayMapChallenge 2026"
class: text-center
transition: fade
---

# Coding Café - October 2026
## #30DayMapChallenge: one map a day in November

Intro session · Wed 28 Oct, 12:00–13:30 · Vertigo 9.06

https://github.com/TUe-BE-ISBE-Coding-Cafe/30daymapchallenge-2026

---

## Today

| Time | What |
|---|---|
| 12:00 | What is the challenge, and how we do it at the Coding Café |
| 12:15 | Pick your tool: R, Python, Julia, web-based or GIS |
| 12:30 | **Hands-on:** make your Day 1 map together |
| 13:15 | Share it, sign up for days, questions |

<div class="p-4 border border-green-400 rounded bg-green-50 text-gray-800 mt-6 text-left">

**Goal:** everybody leaves with one map on their laptop. One map is a success.

</div>

---

## What is the #30DayMapChallenge?

- A community challenge: **one map per day, 1–30 November**, each day has a theme
- **No sign-up and no jury:** make a map, post it with **#30DayMapChallenge**, look at what others made
- **Any tool is welcome:** R, Python, Julia, the browser, QGIS, pen and paper...
- **Fewer than 30 maps is completely fine.** Pick the themes you like
- Beginners very welcome

Official site: https://30daymapchallenge.com

---
layout: two-cols
---

## Our edition

- A starter **GitHub repo** with data and Day 1 scripts
- A **showcase website** that shows every map we make
- A **sign-up table** to spread the days
- A show-and-tell at the end of November, if enough people join

::right::

<img src="/img/day01-example.png" class="border rounded max-h-80 mx-auto" />

<p class="text-xs text-center opacity-70">Day 1 example: cafés in Eindhoven</p>

---

## The 2026 themes

<div class="grid grid-cols-5 gap-x-4 gap-y-1 text-sm text-left mt-2">
<div><b>01</b> Points</div>
<div><b>02</b> Lines</div>
<div><b>03</b> Polygons</div>
<div><b>04</b> Clusters</div>
<div><b>05</b> Senses: Sight</div>
<div><b>06</b> Vintage</div>
<div><b>07</b> 10 minute map</div>
<div><b>08</b> Utopia</div>
<div><b>09</b> Urban-rural</div>
<div class="text-red-600"><b>10</b> Prompting only</div>
<div><b>11</b> Senses: Sound</div>
<div><b>12</b> Power</div>
<div><b>13</b> Interactions</div>
<div><b>14</b> Borgesian map</div>
<div><b>15</b> Inside out</div>
<div class="text-red-600"><b>16</b> Collaborative map</div>
<div><b>17</b> Light & dark</div>
<div><b>18</b> NULL</div>
<div><b>19</b> Senses: Smell</div>
<div><b>20</b> Hexagons</div>
<div><b>21</b> OpenStreetMap</div>
<div><b>22</b> Projections</div>
<div><b>23</b> Senses: Taste</div>
<div><b>24</b> Network</div>
<div><b>25</b> Is this a map?</div>
<div><b>26</b> Water</div>
<div class="text-red-600"><b>27</b> New tool</div>
<div><b>28</b> Senses: Feeling</div>
<div><b>29</b> Raster</div>
<div><b>30</b> Pen & paper</div>
</div>

<div class="text-sm mt-6 text-left">

- **Day 10:** the map is made **entirely** through an AI chat or CLI
- **Day 16:** made **with another person** (AI doesn't count)
- **Day 27:** a good day to try a tool from the next slides you've never used

</div>

---

## Pick your tool

<div class="grid grid-cols-5 gap-3 mt-6 text-left text-sm">

<div class="p-3 border rounded">

### R
`sf` + `ggplot2`, `tmap`

Starter script in the repo

</div>

<div class="p-3 border rounded">

### Python
`geopandas` + `matplotlib`

Starter script in the repo

</div>

<div class="p-3 border rounded">

### Julia
`GeoDataFrames.jl` + `GeoMakie.jl`

</div>

<div class="p-3 border rounded">

### Web-based
Leaflet, MapLibre, Observable, kepler.gl, geojson.io

</div>

<div class="p-3 border rounded">

### GIS
QGIS (free), ArcGIS Pro

No code needed

</div>

</div>

<div class="mt-6 text-left">

All of them read the same files in `data/`: **GeoJSON in EPSG:4326** (lon/lat).
For the Netherlands, reproject to **EPSG:28992 (RD New)**, which is in metres.

</div>

---

## R

```bash
Rscript r/install.R              # installs sf + ggplot2 (once)
Rscript r/day01_points.R <you>   # writes maps/day01-<you>/map.png
```

```r
cafes    <- st_read("data/eindhoven_cafes.geojson")    |> st_transform(28992)
boundary <- st_read("data/eindhoven_boundary.geojson") |> st_transform(28992)

ggplot() +
  geom_sf(data = boundary, fill = "grey95", colour = "grey40") +
  geom_sf(data = cafes, colour = "#c8102e", size = 1.8, alpha = 0.8) +
  theme_void()
```

Or open `r/day01_points.R` in RStudio / Positron with the repo as working directory.
On Linux, `sf` needs GDAL/GEOS/PROJ first.

---

## Python

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r python/requirements.txt
python python/day01_points.py <you>   # writes maps/day01-<you>/map.png
```

```python
cafes    = gpd.read_file("data/eindhoven_cafes.geojson").to_crs(epsg=28992)
boundary = gpd.read_file("data/eindhoven_boundary.geojson").to_crs(epsg=28992)

fig, ax = plt.subplots(figsize=(7, 7))
boundary.plot(ax=ax, facecolor="0.95", edgecolor="0.25")
cafes.plot(ax=ax, color="#c8102e", markersize=10, alpha=0.8)
ax.set_axis_off()
```

Conda: `conda install -c conda-forge geopandas matplotlib`

---

## Julia

```julia
using Pkg; Pkg.add(["GeoDataFrames", "GeoMakie", "CairoMakie"])   # once
```

```julia
using GeoDataFrames, GeoMakie, CairoMakie

cafes    = GeoDataFrames.read("data/eindhoven_cafes.geojson")
boundary = GeoDataFrames.read("data/eindhoven_boundary.geojson")

fig = Figure(size = (700, 700))
ax  = GeoAxis(fig[1, 1]; dest = "EPSG:28992")
poly!(ax, boundary.geometry; color = :grey95, strokecolor = :grey40, strokewidth = 0.5)
scatter!(ax, cafes.geometry; color = "#c8102e", markersize = 6)
hidedecorations!(ax)
save("maps/day01-<you>/map.png", fig)
```

No starter script in the repo yet: if you make one, a PR is very welcome.

---

## Web-based

**No install:** drop the GeoJSON into [geojson.io](https://geojson.io), [kepler.gl](https://kepler.gl/demo) or [Felt](https://felt.com), style it, export a PNG.

**A bit of code:** [Leaflet](https://leafletjs.com), [MapLibre GL JS](https://maplibre.org) or [Observable Plot](https://observablehq.com/plot/)

```html
<div id="map" style="height: 600px"></div>
<script>
  const map = L.map("map").setView([51.44, 5.48], 12);
  L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
    attribution: "© OpenStreetMap contributors",
  }).addTo(map);
  fetch("data/eindhoven_cafes.geojson")
    .then((r) => r.json())
    .then((d) => L.geoJSON(d).addTo(map));
</script>
```

Web maps use Web Mercator (EPSG:3857): fine for Eindhoven, but try Day 22 (Projections) elsewhere.

---

## GIS: QGIS

1. Install [QGIS](https://qgis.org) (free, Windows / macOS / Linux)
2. Drag `data/eindhoven_boundary.geojson` and `data/eindhoven_cafes.geojson` into the window
3. Bottom right: set the project CRS to **EPSG:28992**
4. **Layer Properties → Symbology:** colours, sizes, labels
5. Optional background: **XYZ Tiles → OpenStreetMap** in the Browser panel
6. **Project → New Print Layout:** add the map, title, scale bar, credits → **Export as Image** (`map.png`)

Days that suit GIS well: 03 Polygons, 20 Hexagons (*Create Grid*), 29 Raster (AHN elevation from PDOK).

---

## Data

Pre-downloaded in `data/`: cafés and the municipal boundary of Eindhoven (OpenStreetMap).

<div class="text-xs">

| Source | What | Licence |
|---|---|---|
| OpenStreetMap (Overpass Turbo, `osmdata`, `osmnx`) | Amenities, roads, buildings, trees... | ODbL: credit **© OpenStreetMap contributors** |
| PDOK | BAG buildings, BGT, TOP10NL, AHN elevation, aerial photos | Mostly CC0 / CC BY 4.0 |
| CBS | Statistics per wijk / buurt, 100 m and 500 m grids | CC BY 4.0 |
| Eindhoven open data | Trees, lamp posts, parking, events... | Mostly CC0 / CC BY |

</div>

Write every source and its licence in your map's README.

---

## AI is welcome

This year's Coding Café theme is **AI in research software development**, so using an AI assistant is supported. It's not the main aim: maps made without AI are just as welcome.

**One rule:** every map's `README.md` has one line saying what the AI did and what you did.

> **AI disclosure:** AI wrote the plotting code, I chose the data and the projection.

> **AI disclosure:** No AI used.

- **Day 10 (Prompting only):** made fully through AI. Include your prompts (`prompts.md`)
- Whatever the AI made, **you** check that the data and the map are real and correct

---

## How to take part

1. **Join:** fill in the sign-up form (2 minutes): https://forms.cloud.microsoft/e/Qqk5yjSuVT
2. **Pick 1–2 days** and add your name to `signup.md` (optional)
3. **Fork** the repo on GitHub and clone it
4. **Make a map**, then add a folder `maps/dayNN-<github-handle>/` with:
   - `map.png`
   - your code (`.R`, `.py`, `.jl`, `.html`, `.qgz`, ...)
   - `README.md` from `maps/_TEMPLATE/`, **including the AI disclosure**
5. **Open a pull request.** One folder per map; don't edit other people's folders

Merged maps show up on the showcase site a few minutes later.

---
layout: center
---

# Hands-on: your Day 1 map

<div class="text-left mt-6">

1. Clone the repo (or download the ZIP from GitHub)
2. Pick your tool and run the Day 1 example from the previous slides
3. **Make it yours:** change the colours, the title, add another OSM layer...
4. Fill in `maps/day01-<you>/README.md` from the template

</div>

<div class="p-4 border border-green-400 rounded bg-green-50 text-gray-800 mt-6 text-left">

Stuck on installing? Pair up with someone, or start in QGIS or the browser.

</div>

---

## Share it

- **Pull request** to `TUe-BE-ISBE-Coding-Cafe/30daymapchallenge-2026`
- **Social media:** post with **#30DayMapChallenge** and the day's theme (Bluesky, Mastodon, LinkedIn, Instagram...). Credit your data
- **Optional:** tag **Rbanism** (TU Delft), who run an R-only edition

**See all the maps:** https://tue-be-isbe-coding-cafe.github.io/30daymapchallenge-2026/

---
layout: center
class: text-center
---

# Thank you!

Questions?

Repo: https://github.com/TUe-BE-ISBE-Coding-Cafe/30daymapchallenge-2026

Sign up: https://forms.cloud.microsoft/e/Qqk5yjSuVT
