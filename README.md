# FaIR Climate Model Emulator
Exploring extreme warming outcomes under policy scenarios using the FaIR simple climate model

Erica Simon, Woodwell Climate Risk Intern

January to March 2024

## Project Overview
This repository contains code to setup FaIR in a manner that reproduces historical warming trends and is optimized for probabilistic runs under different policy scenarios. These policy scenarios are translated into emissions trajectories via three IAM-produced datasets published by NGFS (Network for Greening the Financial System) in collaboration with the IIASA. Additionally, an aggregated historical dataset is harmonized with these future trajectories to address any inconsistencies (see `notebooks/README.md` Data Preprocessing for more on harmonization). To account for uncertainty, a parameter ensemble provided by the creators of FaIR is incorporated, resulting in 800 climate configurations for each scenario. Using these configurations, each future emissions dataset is input into FaIR, generating a probability distribution of temperature outcomes for seven IAM scenarios (Current Policies; NDCs; Fragmented world; Delayed transition; Below 2℃; Net zero 2050; Low demand). This repository also includes methods to visualize these outputs with a focus on the high-end tail of the distribution (95th to 100th percentile). Additionally, an ensemble mean is generated by averaging annual temperature outputs across the three IAMs for each scenario, allowing for more concise visualizations. 

The "summary plot" below displays the probabilities of crossing warming thresholds by 2100, as calculated from the ensemble mean of the three IAMs.
<img width="841" alt="final plot" src="https://github.com/WoodwellRisk/FaIR/assets/129074733/ec3e5fed-ae13-43e3-9436-b52e2c5ad08c">


## Introduction to FaIR
The Finite Amplitude Impluse Response (FaIR) model is a climate model emulator that is calibrated to fully-coupled GCM outputs, reproducing their representation of the climate system with enhanced computational efficiency (it takes ~90 s to run 6000 projections in parallel). This section contains resources published by the FaIR Development Team in addition to notebooks I created, which can help users gain a better understanding of FaIR.

`FAIR/examples`

I've added a submodule that links to [this repo](https://github.com/OMS-NetZero/FAIR/tree/master) made by Dr. Chris Smith from University of Leeds, the creator of FaIR. The `examples` directory is very useful if you are interested in understanding how FaIR works, especially if you'd like to modify/create an instance of the model. The notebook `FAIR/examples/basic_run_example.ipynb` in particular is a great introduction.

## Directories

`FAIR`

As described above, this submodule contains examples of setting up and running FaIR (authored by the model's creators).

`notebooks`

This directory contains the code to run set up and FaIR as detailed in the project overview. 

`inputs`

This directory contains input files for future emissions trajectories, downloaded from the [NGFS Scenarios Portal](https://www.ngfs.net/ngfs-scenarios-portal/).

`outputs`

This directory contains all data produced as a result of running the notebooks, including the cleaned input data and FaIR output data.

`plots`

All plots that were produced in the analysis were saved into this directory.

`archive`

This directory contains notebooks that were useful in the learning process of this project but were not ultimately used in the final methods.
