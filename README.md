# MOSAIC landscape data

Data files behind the MOSAIC landscape profiles, served as static files from GitHub Pages.
There is one folder per landscape, named with the landscape code used by the
[catalog](https://github.com/MOSAIC-mfl/catalog) (`catalog/landscapes/<CODE>/`).

| Folder | Landscape | Catalog profile |
|---|---|---|
| [`KEN-LVB/`](KEN-LVB/) | Lake Victoria Basin | [`landscapes/KEN-LVB`](https://github.com/MOSAIC-mfl/catalog/tree/main/landscapes/KEN-LVB) |
| [`PER-PCL/`](PER-PCL/) | Ucayali, Peru | [`landscapes/PER-PCL`](https://github.com/MOSAIC-mfl/catalog/tree/main/landscapes/PER-PCL) |

Once GitHub Pages is enabled, a file at `KEN-LVB/meta/layers.json` is served at:

```
https://mosaic-mfl.github.io/landscape-data/KEN-LVB/meta/layers.json
```

## What goes here

Each landscape folder holds what the profile's map explorer reads from its `site` root, with the
same layout the explorer expects, for example:

```
<CODE>/
  meta/       layer list, story and study metadata
  series/     time series
  vectors/    boundaries, rivers, labels (GeoJSON)
  climate/    climate grids and derived indices
  fire/       fire grids
  query/      rasters queried by the explorer
  figures/
  fonts/
  tiles/      only tiles small enough for GitHub (see limits)
```

Large files (most `.pmtiles` and big rasters) stay on the landscape's Hugging Face dataset, which
is the profile's default root. Each profile's `explorer.yaml` in the catalog says which paths are
read from this site and which from Hugging Face (`data.roots`, `data.routes`).

## Rules

- **Size.** GitHub rejects files over 100 MB and warns above 50 MB; a Pages site should stay
  under 1 GB in total. Anything larger goes to Hugging Face. Git LFS does not work here, because
  GitHub Pages does not serve LFS files.
- **Withheld files.** Files listed under `data.withheld` in a profile's `explorer.yaml` (for
  example a boundary whose licence does not allow publication) are never committed.
- **Provenance.** Every layer comes from a source registered in the profile's `sources.yaml`
  and, where one exists, a catalog record. A landscape folder may include a `DATA_REPORT.md`
  describing how its files were produced.
- **No secrets.** Do not commit tokens, keys or credentials, including inside processing
  scripts or notebooks.

## How the catalog uses it

Each profile points its `site` root at its folder here, in `catalog/landscapes/<CODE>/explorer.yaml`:

```yaml
data:
  roots:
    site: https://mosaic-mfl.github.io/landscape-data/KEN-LVB/
    hf: https://huggingface.co/datasets/<owner>/<dataset>/resolve/main/
```

Records whose download location is a file here link to the same URL.

## Adding a landscape

1. Create a folder named with the landscape's catalog code and add its files.
2. Open a pull request to `main`.
3. Point the profile's `explorer.yaml` (and any records) at the new folder in a catalog pull request.

## Publishing

GitHub Pages serves this repository from the `main` branch, root folder
(*Settings → Pages → Deploy from a branch → main / (root)*). The `.nojekyll` file makes Pages
serve every file as is, without a Jekyll build.
