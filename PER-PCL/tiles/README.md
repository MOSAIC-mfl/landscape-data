# PER-PCL base map tiles

Read by the Ucayali map explorer (`catalog/landscapes/PER-PCL/explorer.yaml`). Both cover only the
explorer's `map.max_bounds` (-78.0, -12.3, -68.44, -6.41).

| File | Content | Source |
|---|---|---|
| `s2_rgb.pmtiles` | Sentinel-2 true colour, WebP, z5-12. Department bounding box: 30 m 2025 mosaic; beyond it: 60 m 2025 median, gaps from 2023-2025 then 2020-2025; sea (DEM at or below 0 m) in one flat colour. | Copernicus Sentinel-2 L2A via Earth Engine (MOSAIC export, 2026-11-26) |
| `terrain.pmtiles` | Terrain-RGB (Mapbox encoding), lossless WebP, z5-10, heights rounded to 1 m. Relief shading and 3D only. | Copernicus DEM GLO-30, resampled to ~60 m (MOSAIC export, 2026-11-26) |

Scripts: `MOSAIC internal/per-pcl-square-basemap_2026-11-25/` in the private ai-context repo
(`wide_export.py`, `wide_tiles.py`, `terrain_shrink.py`, `crop.py`).
