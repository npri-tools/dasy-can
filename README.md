# dasy-can
dasy-can delinates Canadian Census boundaries by populated areas. It aims to be a Canadian equivalent to the US Environmental Protection Agency's Dasymetric Toolbox: https://www.epa.gov/enviroatlas/dasymetric-toolbox

## What's Here
- Raster
 - Zipfile containing TIF isolating areas identified as "urban" from Natural Resources Canada's 2020 land cover mapping (https://open.canada.ca/data/en/dataset/ee1580ab-a23d-4f86-a09b-79763677eb47)
 - Zipfile containing TIF isolating areas identified as "settlement" from Agriculture and Agri-Food Canada's 2020 land use mapping for Canada south of 60N (https://open.canada.ca/data/en/dataset/fa84a70f-03ad-4946-b0f8-a3b481dd5248)
- Vector
 - Zipfile containing shapefile (.shp) with 2021 Canadian Census boundaries modified to conform to areas identified as "urban" based on Natural Resources Canada's 2020 land cover mapping (https://open.canada.ca/data/en/dataset/ee1580ab-a23d-4f86-a09b-79763677eb47)
 - Zipfile containing shapefile (.shp) with 2021 Canadian Census boundaries modified to conform to areas identified as "settlement" based on Agriculture and Agri-Food Canada's 2020 land use mapping for Canada south of 60N (https://open.canada.ca/data/en/dataset/fa84a70f-03ad-4946-b0f8-a3b481dd5248)

## What It Looks Like
TBD (screenshots)

## How It Works
1. Rasters are mosaic-ed (in the case of AAFC's land use rasters, which are separated by UTM zones across Canada) or loaded (in the case of NRC's land cover raster)
2. Areas identified as "urban" (value = 17 in NRC's dataset) or "settlement" (in AAFC's dataset) are isolated
3. The focal statistics tool in ArcGIS Pro 3.x is used to remove "smooth" the dataset to produce a more realistic representation of areas where people live. Parameters: A 6 cell rectangular window (so approximately 200m N/E/S/W) is used to calculate the majority value (0 = not urban/settlment, 1 = urban/settlement) for each pixel. The results are the two raster files.
4. The raster to polygon tool in ArcGIS Pro 3.x is then used to convert the raster files to vectors.
5. The vectors are then used in a pairwise clip to isolate only the parts of Census dissemination boundaries that fall within the bounds of urban/settlement areas.

