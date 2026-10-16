# Comparative Evaluation of Machine Learning Algorithms for Land Cover Classification Using Sentinel-2 Satellite Imagery over Addis Ababa Ethiopia

Code accompanying the manuscript submitted to *Discover Earth Observation*.

**Author:** Garamu Tilahun Iticha
**Affiliation:** Ethiopian Space Science and Geospatial Institute (ESSGI), Addis Ababa, Ethiopia
**Contact:** garamutilahun@gmail.com
**ORCID:** https://orcid.org/0000-0001-9041-6939

---

## Overview

This repository contains the Google Earth Engine (JavaScript) and Python code used to compare four machine learning classifiers for land cover mapping over Addis Ababa and its surrounding landscape using Sentinel-2 Level-2A imagery:

- Random Forest (RF)
- Support Vector Machine (SVM, RBF kernel)
- Extreme Gradient Boosting (XGBoost)
- K-Nearest Neighbors (KNN)

Classification and accuracy assessment were run in two environments: Google Earth Engine (RF, CART, SVM) and Python/scikit-learn (RF, SVM, XGBoost, KNN).

**Study design in brief**

| Item | Description |
|---|---|
| Study area | Addis Ababa and surroundings, Ethiopia (15 km buffer around 38.75°E, 9.02°N) |
| Imagery | Sentinel-2 Level-2A, January to December 2021 (91 scenes), cloud-free median composite |
| Predictors | Bands B2, B3, B4, B8, B11, B12 plus NDVI, NDWI, NDBI |
| Reference data | ESA WorldCover 2021 (v200), quality-controlled and class-balanced |
| Samples | 1,800 points (300 per class, six classes); 1,267 training and 533 validation |
| Metrics | Overall accuracy, Cohen's kappa, per-class precision, recall and F1, macro-F1 |

---

## Repository structure

```
.
├── README.md
├── LICENSE
├── gee/
│   ├── figure1_study_area.js          # Figure 1: study area map (included)
│   ├── [composite_and_sampling].js    # Sentinel-2 composite, indices, sample points
│   └── [gee_classification].js        # RF, CART, SVM in Google Earth Engine
├── python/
│   ├── [classification].ipynb         # RF, SVM, XGBoost, KNN in scikit-learn
│   └── requirements.txt               # Python dependencies
└── data/
    └── [sample_points.csv]            # Training / validation sample points
```

Items in square brackets are placeholders: rename them to match the files you upload, and delete any line you do not include.

---

## Data sources

All input data are free and openly available.

| Dataset | Access |
|---|---|
| Sentinel-2 Level-2A (`COPERNICUS/S2_SR_HARMONIZED`) | Copernicus Data Space Ecosystem: https://dataspace.copernicus.eu/ and Google Earth Engine |
| ESA WorldCover 2021 v200 (`ESA/WorldCover/v200`) | https://esa-worldcover.org/ and Google Earth Engine |

---

## Requirements

### Google Earth Engine
- A registered Google Earth Engine account (https://earthengine.google.com/)
- Scripts are written for the Earth Engine **Code Editor** (JavaScript API). To run one, open https://code.earthengine.google.com/, create a new script, paste the file contents and click **Run**.

### Python
- Python 3.[x]
- numpy, pandas, scikit-learn, xgboost, matplotlib
- Install with:

```bash
pip install -r python/requirements.txt
```

---

## Usage

Run the scripts in this order:

1. **`gee/figure1_study_area.js`**
   Draws the study area map (Figure 1). It buffers the centre of Addis Ababa by 15 km (AOI) and 65 km (context window), displays ESA WorldCover 2021 clipped to the wider area, outlines the Sentinel-2 tile footprint (T37PDK) in blue and the AOI in red, marks Addis Ababa in yellow, and adds a legend. Take a screenshot or export the map view for the figure.
2. **`gee/[composite_and_sampling].js`**
   Builds the cloud-free median composite, calculates NDVI, NDWI and NDBI, and generates the balanced sample points.
3. **`gee/[gee_classification].js`**
   Trains and evaluates RF, CART and SVM inside Earth Engine.
4. **`python/[classification].ipynb`**
   Trains and evaluates RF, SVM, XGBoost and KNN with scikit-learn, with feature standardization for SVM and KNN.

> **Note:** SVM requires feature standardization. Without it, SVM failed in the Earth Engine experiments (overall accuracy 14.45%, kappa = 0.000), as reported in the manuscript.

---

## Land cover classes

Derived from ESA WorldCover 2021 (six classes used in the classification):

[List the six classes used in your study, e.g. tree cover, shrubland, grassland, cropland, built-up, water]

---

## Citation

If you use this code, please cite the manuscript and the archived repository:

> Iticha, G. T. (2026). Comparative Evaluation of Machine Learning Algorithms for Land Cover Classification Using Sentinel-2 Satellite Imagery over Addis Ababa Ethiopia. *Discover Earth Observation* [under review].

> Iticha, G. T. (2026). [Repository title] (v1.0) [Software]. Zenodo. https://doi.org/10.5281/zenodo.[XXXXXXX]

---

## License

This project is released under the MIT License. See the `LICENSE` file for details.

---

## Acknowledgements

Contains modified Copernicus Sentinel data (2021) processed with Google Earth Engine. Reference land cover from ESA WorldCover 2021 © ESA WorldCover project / Contains modified Copernicus Sentinel data (2021) processed by the ESA WorldCover consortium.
