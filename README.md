# Hydrotempo globe tiles

The tiles the 3D water globes of [hydrotempo.com](https://hydrotempo.com/) draw, served from this repository's Pages
site (<https://limpidmaja.github.io/hydrotempo-tiles/>). They are built on the owner's Mac by the scripts named in
`manifest.json` (in the site's repository) and published here as one commit, replaced on every publish, so old tiles
never pile up in the history.

Scheme: equirectangular, level z has 2^(z+1) x 2^z tiles, row 0 at the north, files `<layer>/<z>/<x>_<y>`.

| Layer | What | Levels | Source | Licence and credit |
| --- | --- | --- | --- | --- |
| `earth/` | The Earth picture, 512 px WebP. Level 7 (about 300 m a pixel) only on and near land | 0-7 | [NASA Blue Marble Next Generation](https://science.nasa.gov/earth/earth-observatory/blue-marble-next-generation/), August 2004, 500 m | Public domain. NASA Earth Observatory, Blue Marble Next Generation by Reto Stöckli |
| `coast/` | Land share per pixel, 512 px PNG, with `index.json` (tiles crossing a coast, tiles wholly land) | 0-7 | [OpenStreetMap land polygons](https://osmdata.openstreetmap.de/data/land-polygons.html) | [ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/). © OpenStreetMap contributors |
| `relief/` | Seafloor hillshade, 512 px WebP | 0-5 | [GEBCO 2026 Grid](https://doi.org/10.5285/4f68d5c7-45eb-f999-e063-7086abc036fa) | Public domain. GEBCO Compilation Group (2026) GEBCO 2026 Grid (doi: 10.5285/4f68d5c7-45eb-f999-e063-7086abc036fa) |
| `terrain/` | Land heights, 65 x 65 lossless WebP, metres = red x 256 + green (below sea level stored as 0), land only | 0-7 | GEBCO 2026 Grid, averaged to 1 arc-minute | As above |

`manifest.json` lists every level's file count, bytes and one SHA-256 over all its files.

Only `earth/` level 7 and `terrain/` are partial: a tile exists where the coast index lists it (at level 7, its
level-6 parent) as crossing a coast or wholly land. Everywhere else the globe uses the level above, or flat ground.
