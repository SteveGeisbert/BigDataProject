## GEOG5990 Final Project

This project explores the relationship between global night time lighting, global population, and global GDP at the national level. Combining all of this data in a GIS and processing statistics based on each country, the data is used in MS Azure Machine Learning Studio to explore these relationships.   

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.  There is also a link to the AzureML experiment further down this file.

### Prerequisites

ArcGIS or QGIS

MS Azure Machine Learning Studio

### Installing

Data required:

ESRI world countries shapefile (https://hub.arcgis.com/datasets/a21fdb46d23e4ef896f31475217cbb08_1)

Global GDP at national level (https://data.worldbank.org/indicator/NY.GDP.MKTP.CD)

Nighttime lighting rasters (https://ngdc.noaa.gov/eog/viirs/download_dnb_composites.html); download all 6 tiles from the 2015 annual section.  Keep the vcm-orm-ntl file from each .tar for use.  

Global population raster (https://ghsl.jrc.ec.europa.eu/download.php); Download the entire file (GHS-POP, 2015, 250m, Mollweide); this downloaded at an incredibly slow rate, it took about 10 hours for a 505MB zipped file.  

---

Drag all of these as layers into QGIS or ArcGIS.  

Merge the 6 vcm-orm-ntl nighttime lighting rasters into one large raster.

Join the Global GDP .csv with the world countries shapefile, and only use the 2015 GDP data (population and nighttime lighting rasters are also 2015).  This will leave several null GDP values, most of which are not actually countries (the ESRI world countries shapefile has many features that are not countries).  However, there are also several that do not match the country names in the GDP .csv.  Use that list of null values to scrub the .csv country-by-country to match the countries shapefile, and rejoin the two.  

Use the zonal statistics process on the nighttime lighting raster (with the joined countries shapefile), and again on the global population raster (with the joined countries shapefile).  This should leave you with a countries shapefile containing GDP data, nighttime lighting zonal statistics, and population zonal statistics - all-in-one.  Export this as a .csv.  

## Running the tests

Upload the .csv into MS Azure Machine Learning Studio.  Begin an experiment using this data.  Select the columns (GDP, sum zonal stats for NTL, and sum zonal stats for population).  Clean the missing data from those columns by removing the entire row for any with a 0 value.  

Using the clip function, clip the 90th percentile peak, and select "missing" for the upper substitute value.

Select the new clipped NTL sum, Population sum, and GDP sum columns to conduct the remainder of the experiment.  Which columns you select will depend on which variables you are looking for a relationship between.  Split the data (.8 achieved the greatest R2 that I found).  Train the model for a linear regression with the default settings, and score and evaluate the model.  

This method was able to find a strong relationship between NTL and GDP, with an R2 of .79.  

This is a link to the published experiment on MS AzureML: https://gallery.cortanaintelligence.com/Experiment/GEOG5990-Big-Data-project

## Authors

**Steve Geisbert**

## Acknowledgments

* Much appreciation to Professor Xuantong Wang of the CU Denver Geography and Environmental Sciences department.

