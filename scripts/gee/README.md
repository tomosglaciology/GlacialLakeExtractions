## Google Earth Engine (GEE) Scripts

This folder contains Google Earth Engine scripts used for data extraction, preprocessing, and development of the Object-Based Image Analysis (OBIA) workflow.

The scripts are designed to be used together and contribute to different stages of filter and visualise the image collection and the OBIA process.

### Contents

The folder includes three main scripts:

- **SegmentationClassification** (`segtools`)  
  Performs image segmentation and prepares features for object-based image analysis.

- **TrainClassifier** (`training_class`)  
  Trains the classification model using labelled data.

- **ApplyingClassifier** (`applying_class`)  
  Applies the trained classifier to segmented imagery to generate the final OBIA classifications.

## Supporting scripts 
- **Landsat Filtering and Export** (`funcs`)  
  Function for filtering, visualising, and batch exporting Landsat 4–9 Collection 2 Tier 1 Top-of-Atmosphere (TOA) imagery over a defined area and time range.  
  More information is available [**here**](https://github.com/tomosglaciology/Landsat_filter_export). 

All steps contribute to the final OBIA implementation, which is consolidated in the main script:  
[OBIA_GlacialLakeExtraction](https://github.com/tomosglaciology/GlacialLakeExtractions/blob/main/scripts/gee/OBIA_GlacialLakeExtraction).

For a more detailed breakdown, [Open the script directly in Google Earth Engine](https://code.earthengine.google.com/?scriptPath=users%2Ftomosdanielmorgan%2FGlacialLakeExtraction%3AOBIA_GlacialLakeExtraction).

### Notes

- Scripts are written for execution within the Google Earth Engine Code Editor.  
- Users will need access to a GEE account to run the code. 
