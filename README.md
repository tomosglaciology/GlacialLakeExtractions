# Automated glacial lake extraction using an Object-Based Image Analysis approach in Google Earth Engine
Written by Tomos Morgan, Robert W. McNabb and Paul Dunlop.

**[Open the script directly in Google Earth Engine]()**.

# Motivation
Mapping water bodies over a large study area and over decades using multiple satellite images is data intensive, with file sizes ranging from ~200 MB for complete Landsat 4 and 5 scenes to ~1 GB for Landsat 8 and 9 scenes (Ali et al., 2023). Developing an approach using the cloud-based capabilities of Google Earth Engine (GEE; Gorelick et al., 2017) enables users to reduce the time and cost of downloading, storing and processing images locally, allowing this approach to be quickly applied to the whole Landsat collection for the chosen study area. In this study we present an OBIA approach to mapping glacial lakes developed using GEE. We apply this approach to various Landsat scenes, testing the impact of varying segmentation parameters and input features.

The aims of this research were:
1)	To determine the most efficient automated method to classify water by conducting experiments within GEE to investigate the effects of changing different segmentation and classifier parameters.
2)	To investigate the importance that the inclusion of input features such as hillshade, slope, MNDWI and NDVI has in the classification of water and other landcover types. 
3)	To study whether training a classifier with a single image can produce accurate classification maps when applied across the whole Landsat collection. 
4)	To compare the training of a single image against one image per Landsat sensor (five in total) to assess the changes in overall accuracies of detecting various landcover types in the OBIA classifier. 
5)	To produce a detailed accuracy assessment comparison between different water delineation methods and the OBIA to assess which method(s) is most efficient in extracting glacial lakes in an image collection. 
6)	To assess whether the OBIA classifier produced in this study can outperform pixel-based indices.

# Repository description
Below is all the information on each folder in our repository.

# Datasets

# External data

# Figures
The [figures](https://github.com/tomosglaciology/NewZealand_GlacialLakeExtractions/tree/main/figures) folder contains the PNG files of all figures generated in this study.

# Scripts

# References
* Ali, A., Dunlop, P., Coleman, S., Kerr, D., McNabb, R. W., and Noormets, R.: Glacier area changes in Novaya Zemlya from 1986–89 to 2019–21 using object-based image analysis in Google Earth Engine, J. Glaciol., 69, 1305–1316, https://doi.org/10.1017/jog.2023.18, 2023.
* Gorelick, N., Hancher, M., Dixon, M., Ilyushchenko, S., Thau, D., and Moore, R.: Google Earth Engine: Planetary-scale geospatial analysis for everyone, Remote Sens. Environ., 202, 18–27, https://doi.org/10.1016/j.rse.2017.06.031, 2017.
