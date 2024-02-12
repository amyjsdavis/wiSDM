# Alien species risk modelling and mapping

This repository contains the framework and R code in development for risk modelling and mapping of alien species throughout Belgium and greater Europe at 1 km<sup>2</sup> resolution as part of the TrIAS project.

## Repo structure

```
├── README.md              : Description of this repository
├── LICENSE                : Repository license
├── risk-modelling-and-mapping.Rproj : RStudio project file
├── .gitignore             : Files and directories to be ignored by git
│
├── data
│   ├── external          : external files (e.g. climate rasters, occurrence data, GIS files) required to run the   model. Download via Zenodo (see below).
│   └── processed         : Risk maps and associated files needed for reproducibility GENERATED
└── src                    : R Code
```

Although theoretically possible, this workflow is not applied to all species listed in the published [unified checklist](https://doi.org/10.15468/xoidmd) and whose occurrences are found.  We limit our analysis to a list of species labelled as **emerging**. The emerging status is object of another work package and it is a semi-automated process described in repository [indicators](https://github.com/trias-project/indicators): see [webpage](https://trias-project.github.io/indicators/).

## What you need to do run this workflow (see below for more details):
1) Species scientific name.
2) Climate and habitat raster data files downloaded from Zenodo (links will be provided when data is available)
3) R studio installed in your computer.
4) After cloning this repository, add folders to the existing folder structure shown above as shown below. This will allow you to use the relative path structure in the trias_sdm.R file.
``` 
├── data
    ├── external
          ├── bias_grids (Global taxonomic occurrence grids, downloaded from Zenodo here )
          ├── climate (put climate rasters downloaded from Zenodo here)
          ├── GIS (GIS data downloaded from Zenodo)
          ├── habitat (put habitat rasters downloaded from Zenodo here)
 ```
 ## Workflow  
 
The automated workflow can be divided in three sections:

1. Develop global scale climate-only species distribution models (SDMs)
2. Generate European level SDMs
3. Forecast species distributions under climate change scenarios
 
## What does the Trias modeling workflow do?
1.	Automatically generates IAS risk maps using machine learning. 
Our workflow requires only a species name and generates an ensemble of machine learning algorithms stacked together as a meta-model to produce the final risk map at 1 km2 resolution. Risk maps are generated automatically for standard IPCC greenhouse gas emission scenarios (RCP).  
2.	Automatically generates confidence maps for each IAS risk map. These illustrate confidence of each individual prediction across your study extent.
3.	Addresses geographic sampling bias
4.	Incorporates best practices for the placement of pseudo-absences: pseudo absences are placed in the same ecoregions where presences occur. We use the global model to restrict pseudo absences to areas of low predicted suitability. We use the taxonomic occurrence grid (aka bias grid) to not place pseudoabsences in areas of low sampling effort. The taxonomic occurrence grid summarize the sampling effort of the higher taxon ,the modelled species belongs to.
5.	Flag highly correlated predictors. Highly correlated predictors can have undesirable effects and confuse the interpretation of variable importance
6.	Integrates multiple machine learning algorithms to predict risk. It has been consistently demonstrated that the choice of algorithm has the largest impact on predicted risk and area of predicted risk.
7.	Assesses spatial autocorrelation in the residuals to assess the impacts of clustering. If high, thinning can be employed.


Inputs required run the workflow:
1.	Species name and the GBIF taxon Key (which can be retrieved using the workflow). A list of species can be used to retrieve global occurrences for each species using the global_download.Rmd 
2.	Predictor data (download using the links below )
```
Download CHELSA data: https://envicloud.wsl.ch/#/?prefix=chelsa%2Fchelsa_V1%2Fclimatologies 
Download TrIAS EU Climate data from Zenodo: https://doi.org/10.5281/zenodo.3694065
Download habitat predictors from Zenodo: https://doi.org/10.5281/zenodo.7841324
Download taxonomic occurrence grids from Zenodo: https://doi.org/10.5281/zenodo.7556851
```

## Contributors

[List of contributors](https://github.com/trias-project/risk-modelling-and-mapping/contributors)

## License

[MIT License](https://github.com/trias-project/risk-modelling-and-mapping/blob/master/LICENSE)
