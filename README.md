# FaIR Climate Model Emulator
Erica Simon, Climate Risk Intern

January to March 2024

## Project Overview
This repository contains code to setup FaIR in a manner that reproduces historical warming trends and is optimized for probabilistic runs under different policy scenarios, which are formulized as emissions trajectories. Additionally, it contains methods to visualize key outputs of FaIR with a focus on the high-end tail of the distribution (95th percentile).

## Recommended Workflow

### Introduction to FaIR

`FAIR/examples`

I've added a submodule that links to [this repo](https://github.com/OMS-NetZero/FAIR/tree/master) made by Dr. Chris Smith, the main creator of FaIR. The `examples` directory is very useful if you are interested in understanding how FaIR works, especially if you'd like to modify/create an instance of the model. The notebook `basic_run_example.ipynb` in particular is a great introduction. However, if you are just interested in running an exisiting instance and visualizing the outputs, then this step may not be necessary.

`FaIR_hist.ipynb` 

this notebook...

`FaIR_harmonized`


### Data Preprocessing

`hist_emis_clean.ipynb`

`NGFS_clean_interp.ipynb`

`harmonization.ipynb`

### Running FaIR


`run_ens.ipynb`



### Postprocessing & Visualization of Outputs

`visualize_ens.ipynb`

`ensemble_mean.ipynb`
