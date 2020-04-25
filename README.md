GEOG5990 Final Project

This project explores the relationship between global night time lighting, global population, and global GDP at the national level. Combining all of this data in a GIS and processing statistics based on each country, the data is used in MS Azure Machine Learning Studio to explore these relationships.   

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

ArcGIS or QGIS

MS Azure Machine Learning Studio

### Installing

A step by step series of examples that tell you how to get a development env running

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

---

Upload the .csv into MS Azure Machine Learning Studio.  Begin an experiment using this data.  Select the columns (GDP, sum zonal stats for NTL, and sum zonal stats for population).  Clean the missing data from those columns.  



```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)



## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc

