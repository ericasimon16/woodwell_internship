# FaIR Climate Model Emulator
Erica Simon, Climate Risk Intern

January to March 2024

## Project Overview
This repository contains code to setup FaIR in a manner that reproduces historical warming trends and is optimized for probabilistic runs under different policy scenarios. These policy scenarios are translated into emissions trajectories via three IAM-produced datasets published by NGFS (Network for Greening the Financial System) in collaboration with the IIASA. Additionally, an aggregated historical dataset is harmonized with these future trajectories to address any inconsistencies (see Data Preprocessing for more on harmonization). To account for uncertainty, a parameter ensemble provided by the creators of FaIR is incorporated, resulting in 800 climate configurations for each scenario. Using these configurations, each future emissions dataset is input into FaIR, generating a probability distribution of temperature outcomes for seven IAM scenarios (Current Policies; NDCs; Fragmented world; Delayed transition; Below 2℃; Net zero 2050; Low demand). This repository also includes methods to visualize these outputs with a focus on the high-end tail of the distribution (95th to 100th percentile). Additionally, an ensemble mean is generated by averaging annual temperature outputs across the three IAMs for each scenario, allowing for more concise visualizations. 

The "summary plot" below displays the probabilities of crossing warming thresholds by 2100, as calculated from the ensemble mean.
<img width="841" alt="final plot" src="https://github.com/WoodwellRisk/FaIR/assets/129074733/ec3e5fed-ae13-43e3-9436-b52e2c5ad08c">

## Recommended Workflow

### Introduction to FaIR
The Finite Amplitude Impluse Response (FaIR) model is a climate model emulator that is calibrated to fully-coupled GCM outputs, reproducing their representation of the climate system with enhanced computational efficiency (it takes ~90 s to run 6000 projections in parallel). This section contains resources published by the FaIR Development Team in addition to notebooks I created, which can help users gain a better understanding of FaIR.

`FAIR/examples`

I've added a submodule that links to [this repo](https://github.com/OMS-NetZero/FAIR/tree/master) made by Dr. Chris Smith from University of Leeds, the creator of FaIR. The `examples` directory is very useful if you are interested in understanding how FaIR works, especially if you'd like to modify/create an instance of the model. The notebook `basic_run_example.ipynb` in particular is a great introduction.

`FaIR_harmonized`


### Data Preprocessing

`hist_emis_clean.ipynb`

This notebook details the source of the historical emissions dataset used and renames a handful of variables to match formatting needed for FaIR/aneris.

`NGFS_clean_interp.ipynb`

This notebook cleans the NGFS datasets used to map policy scenarios to emissions trajectories, in addition to providing background information on the source and methods to update projections as new data becomes available.

Cleaning the data involves the following steps: 
- Renaming variables to match FaIR species
- Adjusting units to ensure consistency with the hist. dataset (e.g. CO2 changed from Mt to Gt)
- Infilling missing species: ~30 gas species required to run FaIR were not included in the NGFS dataset. These were mostly minor F-gases with low emissions magnitude but high GWP. To infill the missing species, they are first separated into F-gases and non-F-gases. For the F-gases, the trend in the total "F-gas basket" projection is used to infill. For the non-F-gases, the trend in CO2 projections is used.
- Interpolating to annual timesteps, as the NGFS projections are at 5-year intervals

`harmonization.ipynb`

Since the historical and future emissions datasets come from different sources, there can be inconsistencies in emissions values at the year of overlap (in this case, 2022). For instance, in one case the historical dataset contains 380 Mt CH4 in 2022, while GCAM projects 320 Mt CH4 in 2022 (since projections start in 2020). Thus, harmonization is a methodology to provide a smooth transition between the two timeseries without compromising the details of the projected trend. Since there are multiple valid harmonization methods (see figure below), the Python software [Aneris](https://github.com/iiasa/aneris) is employed to automate choosing the harmonization method. 


Thus, this notebook runs the Aneris harmonizer on the historical and projected datasets. It also includes plots to demonstrate the results of harmonization.

<img width="357" alt="Gidden 2018 fig" src="https://github.com/WoodwellRisk/FaIR/assets/129074733/4b0c3233-ae1d-4c66-bfc3-88373075c81f">

[Gidden et al. (2018)](https://doi.org/10.1016/j.envsoft.2018.04.002)

### Running FaIR


`run_ensemble.ipynb`

This notebook sets up a probabilistic run of FaIR, using the parameter ensemble provided in the FaIR GitHub. For each IAM-generated emissions dataset, FaIR is run with ~800 configurations for each scenario for a total of ~6000 runs per model. The temperature output is saved as a netcdf to avoid the need to run the projections again.


### Postprocessing & Visualization of Outputs

`visualize_ensemble.ipynb`

In this notebook, the temperature datasets from `run_ens.ipynb` are imported and visualizations are made with the data. In particular, the plots focus on the tails of the distribution (95th to 100th percentile) in years 2030, 2050, and 2100. The temperature datasets are viewed probabilistically across the 800 climate configurations using a kernel density estimator, which is a non-parametric method to estimate the pdf of a variable.

`ensemble_mean.ipynb`

Since three datasets are used for future emissions projections, here I calculate an ensemble mean by averaging the temperature across the three outputs for each year, scenario, and climate config. This results in one dataset for each scenario with a temperature distribution of 814 configs, allowing for more concise visualizations. Also included here is code to plot the probabilistic bar charts for key years.