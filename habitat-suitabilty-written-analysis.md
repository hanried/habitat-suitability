
# Written Analysis: Will the Caddo and Sheyenne National Grasslands be suitable habitats for *Sorghastrum nutans* from 2076-2080 depending on emissions scenario?

## **Project Description**
This project analyzes soil, topographic, and climate data to determine whether the Sheyenne and Caddo National Grasslands in the United States will be suitable habitats for the grass species *Sorghastrum nutans* from 2076-2080 depending on the Representative Concentration Pathway (RCP). The Sheyenne National Grasslands are in the southeastern corner of the state of North Dakota and the Caddo National Grasslands are in the northwestern part of Texas, near the Texas-Oklahoma border.

For the soil data, pH is the analyzed variable. The topographic variable is aspect (degrees) derived from elevation (m), and the climate vairable is precipitation (mm). More specifically for the climate variable, the predicted average annual precipitation (mm) from 2076-2080 is being compared between two different emissions scenarios: RCP 4.5 and RCP 8.5. To look at all three data together, it is assumed that soil pH and aspect will be very similar, if not the same, between current day, 2024, and 2076-2080. So current day soil pH and aspect will be used.

<figure>
    <img
        src="/habitat-suitability-notebooks/habitat-suitability-plots-images/golden-sunset-indiangrass-01.png"
        alt="A photo of the Golden Sunset variety of *Sorghastrum nutans*."
        width="25%">
    <figcaption>Image source: <a href='https://license.umn.edu/product/golden-sunset-grass' target='_blank'>University of Minnesota</a></figcaption>
</figure>

## **Site Descriptions**
### Caddo National Grasslands:
Caddo National Grasslands is mainly in Texas, USA, although a small portion of it is in Oklahoma too. It includes two units: Bois d' Arc Creek Unit (13,360 acres) and Ladonia Unit (2,780 acres)<sup>2</sup> and 3 lakes: Lake Coffee Mill (651 acres), Lake Crockett (388 acres), and Lake Fannin (45 acres)<sup>1</sup>. In the Caddo Grasslands, several recreational activities are available such as camping, picnicking, and fishing.<sup>1</sup> The Caddo is also home to wildlife such as coyotes, waterfowl, turkey, largemouth bass, and sunfish.<sup>1</sup>

<img
    src="/habitat-suitability-notebooks/habitat-suitability-plots-images/cng_plot.png"
    alt="A plot of the Caddo National Grasslands on latitude and longitude axes. The grassland is a blue plot on a whitebackground."
    width="25%">

### Sheyenne National Grasslands:
According to the US Forest Service Sheyenne National Grasslands website, the Sheyenne National Grasslands are in the southeastern corner of North Dakota, USA and include 70,180 acres of public land amid 64,769 acres of private land. Camping, hiking, hunting, and backpacking are available as well as other recreational activities. This tallgrass prairie is home to prairie chickens, the Dakota skipper (a small butterfly), the Regal Fritillary (another type of butterfly), ferns, and the western prairie fringed orchid.<sup>5</sup>

<img
    src="/habitat-suitability-notebooks/habitat-suitability-plots-images/sng_plot.png"
    alt="A plot of the Sheyenne National Grasslands on latitude and longitude axes. The grassland is a blue plot on a whitebackground."
    width="25%">

## **Data Descriptions & Citations**
### Grassland Boundaries
The grassland boundaries are National Grassland units from the [National Grassland Units (Feature Layer) of the U.S. Forest Service - Geospatial Data Discovery open data site](https://data-usfs.hub.arcgis.com/datasets/usfs::national-grassland-units-feature-layer/about). Using their [API Explorer](https://data-usfs.hub.arcgis.com/datasets/usfs::national-grassland-units-feature-layer/api), I downloaded all National Grassland information including OBJECTID, NATIONALGRASSLANDID, GRASSLANDNAME, GIS_ACRES, SHAPE_AREA, SHAPE_LEN, and geometry. Full metadata for the National Grasslands Units can be found [here](https://www.arcgis.com/sharing/rest/content/items/b8db5d69787c408d9654a1f36438acbd/info/metadata/metadata.xml?format=default&output=html).

### Soil
The soil pH data comes from the POLARIS database. This database holds soil series probabilities for the contiguous United States at 30 m spatial resolution.<sup>3</sup> The soil varaibles that can be downloaded include silt percentage, clay percentage, and pH. Soil variables can be downloaded at depths ranging from 0 cm to 200 cm and statistics that can be downloaded are mean, mode, median, 5th percentile, and 95th percentile. See full list of varaibles and depths [here](http://hydrology.cee.duke.edu/POLARIS/PROPERTIES/v1.0/Readme) and access the [POLARIS dataset here](http://hydrology.cee.duke.edu/POLARIS/PROPERTIES/v1.0/?C=D;O=A).

### Elevation
Elevation data was downloaded via the [earthaccess API](https://github.com/nsidc/earthaccess/). The specific dataset used is the SRTMGL1 NASA Shuttle Radar Topography Mission Global 1 arc second V003 dataset. The dataset has about a 30m resolution.<sup>4</sup>

### Climate
Climate data was downloaded from the MACAv2 THREDDS data server as raster data. Specifically, the CanESM2 model was chosen, the climate variable is precipitation, the time period is from 2076-2080, the precipitatioon predictions are monthly, and the emissions scenarios being compared are RCP 4.5 and RCP 8.5.
* The RCP 8.5 metadata can be found [here](http://thredds.northwestknowledge.net:8080/thredds/catalog/MACAV2/CanESM2/catalog.html?dataset=REACCHDatasetScan_CanESM2_MACAV2/macav2metdata_pr_CanESM2_r1i1p1_rcp85_2076_2080_CONUS_monthly.nc)
* The RCP 4.5 metadata can be found [here](http://thredds.northwestknowledge.net:8080/thredds/catalog/MACAV2/CanESM2/catalog.html?dataset=REACCHDatasetScan_CanESM2_MACAV2/macav2metdata_pr_CanESM2_r1i1p1_rcp45_2076_2080_CONUS_monthly.nc)

## **Model Description**
A fuzzy model is used to determine habitat suitability of *S. nutans* from 2076-2080 depending on different RCP values, either 4.5 or 8.5. A fuzzy model was chosen because of the ability to assign any value between 0 and 1 as a "True" value. This is helpful because it allows for nuance and variation. For example, *S. nutans* has been found living in soils with a pH range of 4.8 to 8.0<sup>6</sup>. It may not be accurate to use a boolean logic model to say "If the pH is between 4.8 to 8.0, the soil is suitable for *S. nutans* and will be assigned a 1 for it's truth value". *S. nutans* may be best suited for soil pH values of 6-7, survive well in soils with pH values of 5.5 to 6 and 7 to 7.5, tolerate soil pH values of 4.8 to 5.5 and 7.5 to 8, and not survive in soil pH values below 4.8 and above 8. Using a fuzzy model allows all of those specific ranges and variation to be taken into account as a 1 could be assinged to soil pH values of 6-7, 0.75 could be assigned to soil pH values of 5.5 to 6 and 7 to 7.5, and so on. A fuzzy model was not able to be completed for this project, so instead 4 plots will be compared below, 2 for Caddo and 2 for Sheyenne.

## **Plots**
### 1. Comparing the predicted average annual precipitation (mm) from 2076-2080 in the Caddo National Grasslands for RCP values of 4.5 and 8.5:
<img
    src="/habitat-suitability-notebooks/habitat-suitability-plots-images/cng_bound_ave_ann_precip_rcp45_2076_2080_reproj_match_plot.png"
    alt="A plot of the boundaries of the Caddo National Grasslands on latitude and longitude axes is overlaid on top of a plot of the predicted average annual precipitation (mm) from 2076-2080 for the Caddo grasslands and surrounding areas for an emssisions scenario of RCP 4.5."
    width="100%">
<img
    src="/habitat-suitability-notebooks/habitat-suitability-plots-images/cng_bound_ave_ann_precip_rcp85_2076_2080_reproj_match_plot.png"
    alt="A plot of the boundaries of the Caddo National Grasslands on latitude and longitude axes is overlaid on top of a plot of the predicted average annual precipitation (mm) from 2076-2080 for the Caddo grasslands and surrounding areas for an emssisions scenario of RCP 8.5."
    width="100%">

The black outline in both of the plots above are the boundaries of the Caddo National Grasslands. Both plots show the predicted average annual precipitation (mm) from 2076-2080 for two different emissions scenarios: RCP 4.5 and RCP 8.5. Both precipitation plots have been reprojected and matched to the Caddo soil pH DataArray. 

*S. nutans* prefers areas receiving 28-114 cm (280-1140 mm) of annual precipitation.<sup>6</sup> Looking at the plots above, in the RCP 4.5 emissions scenario, the predicted average annual precipitation ranges from about 1070 mm to 1130 mm for the Caddo National Grasslands and surrounding areas. It can be concluded then that in an RCP 4.5 emissions scenario, the Caddo National Grasslands would still be a suitable habitat for *S. ntans* from 2076 to 2080 based on predicted average annual precipitation. The predicted average annual precipitation would be on the high end of *S. nutans* preferred range and it's possible that the grass would prefer the western and southern parts of the Caddo National Grasslands over the northeastern part as the northeastern area of the grassland is predicted to receive a higher average annual precipitation.

Comparing the RCP 4.5 and RCP 8.5 emissions scenarios, it can be condluded that in the RCP 8.5 emissions scenario, from 2076-2080, the Caddo National Grasslands would receive too much annual precipitation for *S. nutans*. In the plot above, it can be seen that the minimum predicted average annual precipitation is about 1380 mm, 240 mm higher than the upper range of *S. nutans*'s preferred annual precipitation. It is possible that the grass species could adapt by 2076 and could tolerate the higher level of annual precipitation.

### 2. Comparing the predicted average annual precipitation (mm) from 2076-2080 in the Sheyenne National Grasslands for RCP values of 4.5 and 8.5:
<img
    src="/habitat-suitability-notebooks/habitat-suitability-plots-images/sng_bound_ave_ann_precip_rcp45_2076_2080_reproj_match_plot.png"
    alt="A plot of the boundaries of the Sheyenne National Grasslands on latitude and longitude axes is overlaid on top of a plot of the predicted average annual precipitation (mm) from 2076-2080 for the Sheyenne grasslands and surrounding areas for an emssisions scenario of RCP 4.5."
    width="100%">
<img
    src="/habitat-suitability-notebooks/habitat-suitability-plots-images/sng_bound_ave_ann_precip_rcp45_2076_2080_reproj_match_plot.png"
    alt="A plot of the boundaries of the Sheyenne National Grasslands on latitude and longitude axes is overlaid on top of a plot of the predicted average annual precipitation (mm) from 2076-2080 for the Sheyenne grasslands and surrounding areas for an emssisions scenario of RCP 8.5."
    width="100%">

## **Citations**
1. “Caddo-LBJ National Grasslands.” National Forests and Grasslands in Texas, U.S. Forest Service, U.S. Department of Agriculture, www.fs.usda.gov/detail/texas/about-forest/districts/?cid=fswdev3_008440. Accessed 2 Dec. 2024.
2. Caddo National Grasslands WMA, Texas Parks and Wildlife Department, tpwd.texas.gov/huntwild/hunt/wma/find_a_wma/list/?id=4. Accessed 2 Dec. 2024.
3. Chaney, N. W., Wood, E. F., McBratney, A. B., Hempel, J. W., Nauman, T. W., Brungard, C. W., & Odgers, N. P. (2016). POLARIS: A 30-meter probabilistic soil series map of the contiguous United States. Geoderma, 274, 54–67. USGS Publications Warehouse. https://doi.org/10.1016/j.geoderma.2016.03.025
4. NASA JPL (2013). <i>NASA Shuttle Radar Topography Mission Global 1 arc second</i> [Data set]. NASA EOSDIS Land Processes Distributed Active Archive Center. Accessed 2024-12-15 from https://doi.org/10.5067/MEaSUREs/SRTM/SRTMGL1.003
5. “Sheyenne National Grassland.” Dakota Prairie Grasslands, U.S. Forest Service, U.S. Department of Agriculture, www.fs.usda.gov/recarea/dpg/recarea/?recid=79470. Accessed 2 Dec. 2024.
6. USDA. “Sorghastrum Nutans (L.) Nash Indian Grass Characteristics.” USDA Plants Database, USDA Natural Resources Conservation Service, plants.sc.egov.usda.gov/plant-profile/SONU2/characteristics. Accessed 15 Dec. 2024. 