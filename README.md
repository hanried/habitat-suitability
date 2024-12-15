# Analysis of Habitat Suitability of the Sheyenne and Caddo National Grasslands for Indiangrass (*Sorghastrum nutans*)

[![DOI](https://zenodo.org/badge/891814932.svg)](https://doi.org/10.5281/zenodo.14425230)


## Project description:
This project analyzes soil, topographic, and climate data to determine whether the Sheyenne and Caddo National Grasslands in the United States will be suitable habitats for the grass species *Sorghastrum nutans* from 2076-2080 depending on the Representative Concentration Pathway (RCP). The Sheyenne National Grasslands are in the southeastern corner of the state of North Dakota and the Caddo National Grasslands are in the northwestern part of Texas, near the Texas-Oklahoma border.

For the soil data, pH is analyzed. The topographic data is aspect (degrees) derived from elevation (m), and the climate data is precipitation (mm). More specifically for the climate data, the predicted average annual precipitation (mm) from 2076-2080 is being compared between two different emissions scenarios: RCP 4.5 and RCP 8.5. To look at all three data together, it is assumed that soil pH and aspect will be very similar, if not the same, between current day, 2024, and 2076-2080. So current day soil pH and aspect will be used.

## How to run the code:
* Follow the order of the Jupyter Notebooks in the 'notebooks' folder from 00-06.
    * The fuzzy model in notebook 05 only has pseudocode, so this would need to be completed by any future users.
* All variables for the Sheyenne National Grasslands will start with 'sheyenne' and all variables for the Caddo National Grasslands will start with 'caddo'.

* All packages used:
    * import os
    * from glob import glob
    * import pathlib
    * from math import floor, ceil

    * import earthaccess
    * import geopandas as gpd
    * import matplotlib.pyplot as plt
    * import pandas as pd
    * import rioxarray as rxr
    * from rioxarray.merge import merge_arrays
    * import skfuzzy as fuzz
    * import xarray as xr
    * import xrspatial

