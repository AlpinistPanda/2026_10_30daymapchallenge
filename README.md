# Coding Café – #30DayMapChallenge Kick-off (October 2026)

**Slides:** https://alpinistpanda.github.io/2026_10_30daymapchallenge/

---

These are the slides and data from the BE Coding Café special edition on 28 October 2026, Vertigo
9.06, TU/e: a kick-off for the [#30DayMapChallenge](https://30daymapchallenge.com), which runs from
1 to 30 November. We covered how the challenge works, how a map gets made in code (in R, Python,
Julia, web tools and QGIS), where to find Dutch open data, and how to use AI to make maps, and then
everyone made their Day 1 *Points* map.

## Related

- **Starter repo**, where the maps are submitted:
  https://github.com/TUe-BE-ISBE-Coding-Cafe/30daymapchallenge-2026
- **All the maps:** https://tue-be-isbe-coding-cafe.github.io/30daymapchallenge-2026/
- **Knowledge base**, with the written version of this session and a guide to all 30 themes:
  https://alpinistpanda.github.io/tue_codingcafe_knowledgebase/maps/
- **Session page:** https://www.becodingcafe.com/events/2026-10-28-30daymapchallenge

## Contents

```
├── slides.md        the slides (Slidev)
├── slide-bottom.vue the Coding Café footer on every slide
├── public/img/      images used in the slides
├── data/            the Eindhoven data used in the hands-on part, with its source and licence
└── .github/         builds the slides and publishes them to GitHub Pages
```

## Running the slides locally

```bash
npm install
npm run dev        # opens the slides at http://localhost:3030
npm run export     # PDF export (needs playwright-chromium)
```

The slides are made with [Slidev](https://sli.dev). Every push to `main` rebuilds them and
publishes them to GitHub Pages (Settings → Pages → Source: **GitHub Actions**).

## Licence

Slides: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The data in `data/` is
© OpenStreetMap contributors, under the [ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/);
see [data/README.md](data/README.md).
