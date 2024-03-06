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

`FaIR_hist.ipynb` 

this notebook...

`FaIR_harmonized`


### Data Preprocessing

`hist_emis_clean.ipynb`

This notebook details the source of the historical emissions dataset used and renames a handful of variables to match formatting needed for FaIR/aneris.

`NGFS_clean_interp.ipynb`

`harmonization.ipynb`

### Running FaIR


`run_ens.ipynb`



### Postprocessing & Visualization of Outputs

`visualize_ens.ipynb`

`ensemble_mean.ipynb`
