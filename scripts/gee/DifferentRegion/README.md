# Applying the Trained OBIA Classifier to a New Region

This tutorial accompanies [`NewRegion`](./NewRegion) and walks
through how to use the classifier trained in this repository (originally on New Zealand imagery)
to map glacial lakes / ice in **any other region**.

## Overview

The script is the original working example (previously used to apply the classifier to
Patagonia) with six numbered `#` comments marking the only places you need to make changes.
Everything else in the script can be left exactly as it is.

## Step 1 — Get access to the trained classifier (`#1`)

The classifier is stored as a Google Earth Engine (GEE) asset, exported with
`Export.classifier.toAsset()`. Other users cannot load it unless it has been shared with them.

- **Asset owner (repo maintainer):** In the GEE Code Editor, go to the **Assets** tab, select the
  classifier asset, click **Share**, and either add specific users' email addresses or set the
  asset visibility to "Anyone can read" if you're happy for it to be publicly reusable.
- **New user:** Once shared, update the asset path at marker `#1`:

  ```js
  var savedClassifier = ee.Classifier.load('projects/ee-tomosdanielmorgan/assets/NZ_OBIA_Classifier');
  ```

> If you get a "not found" or "permission denied" error here, this is almost always a
> sharing/permissions issue rather than a bug in the script.

## Step 2 — Define your region of interest (`#2`)

The script expects a variable called `area` (an `ee.Geometry`). Define this before the line
marked `#2`, either by:

- Drawing a polygon directly in the GEE Code Editor's geometry tools, or
- Importing a shapefile/GeoJSON as an Earth Engine asset and referencing it as an
  `ee.FeatureCollection` or `ee.Geometry`, or
- Pasting coordinates directly (e.g. `ee.Geometry.Polygon([...])`).

## Step 3 — Set your Landsat search parameters (`#3`)

At marker `#3`, adjust the arguments passed to `funcs.allLandsat(...)`:

```js
var all = funcs.allLandsat(area, 20, 20, 2017, 2026, 1, 3, 1, 31)
```

| Argument (in order) | What it controls |
|---|---|
| `area` | Your region of interest (from Step 2) |
| `20, 20` | Max scene cloud cover (%) and max land cloud cover (%) |
| `2017, 2026` | Year range to search |
| `1, 3, 1, 31` | Seasonal window: start month, end month, start day, end day |

## Step 4 — Restrict to a specific path/row (optional) (`#4`)

The `.filter(ee.Filter.and(...))` block at marker `#4` locks the search to one Landsat WRS-2
path/row footprint:

```js
.filter(
  ee.Filter.and(
    ee.Filter.eq('WRS_PATH', 231),
    ee.Filter.eq('WRS_ROW', 95)
  )
)
```

- If you know the path/row that covers your AOI, update the numbers.
- If your AOI spans multiple footprints, or you're not sure which one you need, **delete this
  `.filter(...)` block entirely** and the script will search the whole AOI instead.

## Step 5 — Update the preview scene (`#5`)

Marker `#5` hard-codes a single Landsat scene ID for the quick false-colour preview layer:

```js
var ROI = ee.Image('LANDSAT/LC08/C02/T1_TOA/LC08_231095_20210303').clip(area)
```

Replace this with any scene ID that actually falls within your own AOI/path-row — this is just
for visually sanity-checking your AOI, and doesn't affect the classification itself. You can find
scene IDs by browsing the relevant Landsat collection in the GEE Code Editor for your date range
and location.

## Step 6 — Rename your exports (`#6`)

At marker `#6`, rename the Drive export folders/filenames so they reflect your region instead of
`'Patagonia_OBIA'` / `'Patagonia_image'`:

```js
batch.Download.ImageCollection.toDrive(Obia_clipped, 'Patagonia_OBIA', { ... });
batch.Download.ImageCollection.toDrive(all, 'Patagonia_image', { ... });
```

## Running and checking the output

Once all six markers are updated, run the script. Check the `'false colour'` map layer to confirm
your AOI and imagery look correct, then check the `'OBIA'` classification layer to confirm
water/ice/land are being separated sensibly.

**Important:** the classifier was trained on a different region's imagery. Illumination geometry,
surface materials, and seasonal snow/ice conditions all vary between regions, so classification
accuracy is not guaranteed to match the original training region. Where possible, validate the
output against independent reference data (e.g. manually digitised outlines for a handful of
scenes) before using results for scientific reporting.

## Summary of files

| File | Purpose |
|---|---|
| `TrainClassifier` | Trains the OBIA classifier on labelled reference data |
| `SegmentationClassification` | Shared segmentation/GLCM/reduction functions used by both training and application scripts |
| `ApplyingClassifier` | Shared function that applies a loaded classifier to an image |
| `OBIA_GlacialLakeExtraction` | Applies the classifier within the original training region |
| **`NewRegion`** | **Applies the trained classifier to any new region — six `#`-marked lines to edit (this tutorial)** |

Want to try it yourself? [Open the script directly in Google Earth Engine](https://code.earthengine.google.com/?scriptPath=users%2Ftomosdanielmorgan%2FGlacialLakeExtraction%3APatagoniaExample).

If anything here doesn't work as described, please open an issue on this repository.
