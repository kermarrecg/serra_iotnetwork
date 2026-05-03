# serra_iotnetwork
Python script used to run the analysis in "Correcting scale-dependent bias in urban climate models]{Correcting scale-dependent bias in high-resolution urban climate models: a geostatistical framework" submitted to SERRA Springer

# Scale-dependent bias correction in urban climate models

Python code accompanying:

> Kermarrec G., Scholz R., Montillet J.-P. (2026)
> *Correcting scale-dependent bias in high-resolution urban climate
> models: a geostatistical framework.*
> Stochastic Environmental Research and Risk Assessment, in revision.

## What this repository contains

The five Python modules below implement the methodology described in
Sect. 4 of the manuscript:

| Script | Purpose | Manuscript reference |
|---|---|---|
| `rk_lko.py`           | Regression kriging (RK) and leave-$k$-out cross-validation across the five prediction methods (IDW, OK, RK, RF, GBM) | Sect. 4.2, Sect. 5.3, Table 1 |
| `bootstrap_rstar.py`  | Bootstrap of the optimal averaging radius $R^*$ | Sect. 5.6, Fig. 6 |
| `spatial_blocking.py` | Leave-block-out (LBO) cross-validation on 500 m blocks | Sect. 5.7, Table 3, Fig. 7 |
| `variogram_diag.py`   | Directional variograms (N–S, E–W) before and after RK trend removal | Sect. 5.5, Fig. 5 |
| `mixed_beta.py`       | Mixed-effects ICC analysis of $\beta_1$ across nights | Sect. 5.9, Fig. 9 |

A small helper module `geostats_utils.py` groups Matérn/exponential
variogram functions and the kriging routines used by all five scripts.

## Data availability

**The empirical sensor data and FITNAH-3D output used in the manuscript
are not publicly redistributable.**

- The IoT sensor network data are proprietary to the City of Mannheim
  ("sMArt City" programme).
- The FITNAH-3D model output was produced by GEO-NET Umweltconsulting
  GmbH under contract with the City of Mannheim.

Researchers interested in obtaining access for replication can contact
the corresponding author to discuss data
sharing arrangements with the data owners.

The scripts can be inspected and adapted to any analogous dataset
(a high-resolution urban climate model output paired with a network of
in-situ temperature observations).

## Software requirements

- Python ≥ 3.9
- numpy, scipy, pandas, scikit-learn, scikit-gstat, matplotlib

```bash
pip install numpy scipy pandas scikit-learn scikit-gstat matplotlib
```

## File structure expected by the scripts

The scripts read three inputs:

```
data/
├── stations.csv          # columns: station_id, x, y, T_obs (one row per station × timestep)
├── fitnah_field.tif      # 5 m raster of FITNAH-3D autochthonous temperature
└── nights.csv            # list of selected tropical autochthonous nights
```

Paths are configured at the top of each script. Adapt to your local
file layout.

## How the canonical numerical results were produced

All numerical results reported in the manuscript (RMSE values,
$\bar{\beta}_1 = 0.79 \pm 0.32$, ICC = 0.14, $R^* = 200$ m, etc.) were
produced on the LUIS HPC cluster (Leibniz Universität Hannover) using
the scripts in this repository. The exact run configuration and SLURM
submission scripts are kept on the cluster; the modular logic is
preserved here so the analysis can be repeated on any compatible
dataset.

## Citation

If you use this code, please cite:

> Kermarrec G., Scholz R., Montillet J.-P. (2026). Correcting
> scale-dependent bias in high-resolution urban climate models:
> a geostatistical framework. Stochastic Environmental Research
> and Risk Assessment.

## Licence

MIT licence. See `LICENSE` file.

## Contact

Gaël Kermarrec — kermarrec@meteo.uni-hannover.de
Institut für Meteorologie und Klimatologie, Leibniz Universität Hannover

