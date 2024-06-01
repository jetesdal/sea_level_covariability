# Lapenta Summer Internships 2024: Spatial Coherence in Sea Level Variability

This repository is for the spatial coherence in sea level variability project as part of the Lapenta Summer Internships 2024.

Theo Avila, University of Illinois Urbana-Champaign<br>
Jan-Erik Tesdale ([jetesdal](https://github.com/jetesdal)), Princeton University/GFDL<br>
Jake Steinberg ([jakesteinberg](https://github.com/jakesteinberg)), GFDL<br>
Katherine Turner ([keturner8](https://github.com/keturner8)), University of Arizona/GFDL<br>
John Krasting ([jkrasting](https://github.com/jkrasting)), GFDL
    
## Objective
Using dynamic sea level (zos) from GFDL models, identify regions of co-variability as a function of timescale.

## Motivation
Over much of the ocean, steric sea level dominates zos variability. Using sea level to integrate sterodynamic variability and changes, we can identify regions of co-variability. If we can derive expectations as to where sea level co-varies, we can link these changes to their drivers.

## Tasks/Questions
1. Explore clustering methods:
    - Dimensionality reduction methods, such as EOF analysis (e.g., Nerem et al., 1997; Volkov et al., 2019)
    - Agglomerative Hierarchical Cluster Analysis (Thompson and Merrifield, 2014)
    - Community detection (Infomap), see Falasca et al. (2024), Smiljani´c et al. (in review), Lancichinetti and Fortunato (2009)
    - Gaussian Mixture Modeling
    - Self Organizing Maps (Camargo et al., 2023)
2. Optionally filter in time to select a timescale of interest:
    - Determine relevant time scales (e.g., seasonal, interannual, decadal)
3. Determine spatial patterns of sea level variability for a given timescale.
4. Compare to observational assessments (e.g., Thompson and Merrifield, 2014; Volkov et al., 2019; Little et al., 2021).
5. Can we reconcile the spatial pattern with our dynamical understanding of ocean circulation and variability in heat content?
6. Do these regions change as ocean heat content changes? (piControl vs. historical vs. SSP runs of CM4)
7. Difference between models (high vs. low resolution, coupled vs. ocean-only)

## Literature
- Camargo, C. M. L., et al. (2023). Regionalizing the sea-level budget with machine learning techniques. Ocean Science, 19(1), 17–41. https://doi.org/10.5194/os-19-17-2023
- Falasca, F., et al. (2024). Data-driven dimensionality reduction and causal inference for spatiotemporal climate fields. Physical Review E, 109(4), 044202. https://doi.org/10.1103/physreve.109.044202
- Lancichinetti, A., & Fortunato, S. (2009). Community detection algorithms: A comparative analysis. Physical Review E, 80(5), 056117. https://doi.org/10.1103/physreve.80.056117
- Little, C. M., et al. (2021). North American East Coast Sea Level Exhibits High Power and Spatiotemporal Complexity on Decadal Timescales. Geophysical Research Letters, 48(15). https://doi.org/10.1029/2021gl093675
- Nerem, R. S., Rachlin, K. E., & Beckley, B. D. (1997). Characterization of Global Mean Sea Level Variations Observed by TOPEX/POSEIDON Using Empirical Orthogonal Functions. Surveys in Geophysics, 18(2–3), 293–302. https://doi.org/10.1023/a:1006596211926
- Smiljani´c, J., Blöcker, C., Holmgren, A., Edler, D., Neuman, M., & Rosvall, M. (2023). Community detection with the map equation and infomap: Theory and applications. arXiv:2311.04036. https://arxiv.org/abs/2311.04036
- Sonnewald, M., Wunsch, C., & Heimbach, P. (2018). Linear Predictability: A Sea Surface Height Case Study. Journal of Climate, 31(7), 2599–2611. https://doi.org/10.1175/jcli-d-17-0142.1
- Thompson, P. R., & Merrifield, M. A. (2014). A unique asymmetry in the pattern of recent sea level change. Geophysical Research Letters, 41(21), 7675–7683. https://doi.org/10.1002/2014gl061263
- Volkov, D. L., et al. (2019). Interannual Sea Level Variability Along the Southeastern Seaboard of the United States in Relation to the Gyre‐Scale Heat Divergence in the North Atlantic. Geophysical Research Letters, 46(13), 7481–7490. https://doi.org/10.1029/2019gl083596

## Useful links and references

###  Infomap 
- Tool: https://www.mapequation.org/infomap/
- GitHub repository: https://github.com/mapequation/infomap
- Tutorial notebooks: https://github.com/mapequation/infomap-tutorial-notebooks

### Nemi
- NEMI: https://compclimate.github.io/NEMI/

## Setup

Documented here we use a common Python environment to ensure the analysis in the notebooks work across platforms.

Common practice is to run the analysis on the GFDL system or on a GFDL workstation. 
For detailed instructions on configuring an SSH tunnel, see [this documentation](https://hackmd.io/E9g3SumVSGurIV6ai7E1bw).

If you are on the PP/AN system, you can use a shared Python environment with the following commands:
```bash
module load conda
conda activate /nbhome/ogrp/python/envs/dev
```

If you already have conda installed from an existing setup, you only need to run the second command (`conda activate <path>`). The shared environment includes a comprehensive set of packages not all required for this project. You can view the list of installed packages [here](https://github.com/jkrasting/ocean-python). If you wish to build your own Python environment, you can use [environment.yml](./environment.yml) which lists a subset of Python packages that are relevant for this project.

Once your environment is set up, you can start Jupyter Lab. It is best to run this in the `/work $USER` directory on your workstation. Use the following command to start Jupyter Lab on a specified port (e.g., 8784):

```bash
jupyter lab --port=<port-number> --no-browser
```
Then, open your browser and navigate to:
`http://localhost:<port-number>/lab`
Replace `<port-number>` with your chosen port number (e.g., `8784`). This setup allows you to run Jupyter Lab on your local machine while accessing it through your browser.



