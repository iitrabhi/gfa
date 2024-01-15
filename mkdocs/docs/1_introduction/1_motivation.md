# List of Code
- [**floating\_elastic.inp**] ABAQUS input file for floating ice shelves with constant density assuming linear elastic rheology.
- [**floating\_visco.inp**] ABAQUS input file for floating ice shelves with constant density assuming elasto-visco-plastic rheology.
- [**floating\_var\_rho.inp**] ABAQUS input file for floating ice shelves with depth-varying density assuming elasto-visco-plastic rheology.
- [**CZM\_elastic.for**] ABAQUS user-defined elements subroutine for water-filled cohesive zone elements.
- [**CZM\_visco.for**] ABAQUS user-defined elements subroutine for water-filled cohesive zone elements and ABAQUS user-defined material subroutine for ice with elasto-visco-plastic rheology.
- [**CZM\_sep.for**] ABAQUS user-defined elements subroutine for water-filled cohesive zone elements and ABAQUS user-defined material subroutine for ice with elasto-visco-plastic rheology. The crevasse depth and separation are recorded at each increment.
- [**CZM\_temp.for**] ABAQUS user-defined elements subroutine for water-filled cohesive zone elements and ABAQUS user-defined material subroutine for ice with elasto-visco-plastic rheology and depth-varying temperature.
-  [**generate.ipynb**] Jupyter notebook for generating multiple tasks to run simulations in batches.
- [**get_results.ipynb**] Jupyter notebook for getting crack depth results from multiple simulations.
- [**submit.py**] Python script for submitting Abaqus tasks in batches.
- [**submit.bat**] Run `submit.py` with double-click in Windows.

# Getting Started
## Environment setup for ABAQUS standard and subroutine
Please follow the ABAQUS documentation to set up the environment for ABAQUS standard  
and subroutines. If you want to run tasks in batches, please install Python and Jupyter notebook. To acquire all results by `get_results.ipynb`, please install Pandas (Python package).

## Numerical examples
### Single simulation
The output path needs to be stated by modifying the `open` function in the subroutines (.for files) before running. The simulations can be run via the following command in the environment.

- Surface crevasse depth predictions for floating ice shelves with constant density and temperature assuming linear elastic rheology
`abaqus job={job name} user=CZM_elastic.for inp=floating_elastic.inp ask_delete=OFF int` 

- Surface crevasse depth predictions for floating ice shelves with constant density and temperature assuming elasto-visco-plastic rheology
`abaqus job={job name} user=CZM_visco.for inp=floating_visco.inp ask_delete=OFF int `

- Surface crevasse depth predictions for floating ice shelves with depth-varying density and constant temperature assuming elasto-visco-plastic rheology
`abaqus job={job name} user=CZM_visco.for inp=floating_var_rho.inp ask_delete=OFF int `

- Surface crevasse depth predictions for floating ice shelves with constant density and depth-varying temperature assuming elasto-visco-plastic rheology
`abaqus job={job name} user=CZM_temp.for inp=floating_visco.inp ask_delete=OFF int `

- Surface crevasse depth predictions for floating ice shelves with depth-varying density and temperature assuming elasto-visco-plastic rheology
`abaqus job={job name} user=CZM_temp.for inp=floating_var_rho.inp ask_delete=OFF int `

To modify $\sigma_{max}$, change the value after `sig = ` ($Pa$ for elastic and $10^6 Pa$ for viscoelastic) in the subroutine. To midify $h_s/d_s$, change the value after `hs_ratio =` in the subroutine.
### Run simulations in batches

 1. Put `generate.ipynb`, `get_results.ipynb`, `submit.py`, `submit.bat`, Abaqus input file and subroutine in a same folder.
 2. In `generate.ipynb`, modify `open("CZM.for")` according to the subroutine file name.
 3. In `generate.ipynb`, add the interested meltwater ratio values to the `hs_ratio_list`.
 4. In `submit.py`, add the meltwater ratio values of the task that going to be submitted to the `hs_ratio_list`. Please ensure you have enough memory and Abaqus license to run multiple tasks in parallel.
 5. You can directly run `submit.py` or in Windows, run `submit.bat` to run simulations in parallel.
 6. In `get_results.ipynb`, add the interested meltwater ratio values to the `hs_ratio_list` to get the results.
 
 ### Reproduce results in the paper
 - Fig. 5(a): Run simulations in batches with `floating_elastic.inp` and `CZM_elastic.for` by taking `sig = 1d3`, `sig = 35d3`, `sig = 110d3` and `sig = 220d3` in the subroutine.
 - Fig. 5(b): Run simulations in batches with `floating_visco.inp` and `CZM_visco.for` by taking `sig = 35d-3`, `sig = 110d-3` and `sig = 220d-3` in the subroutine.
 - Fig. 6(a)(b): run simulations with `floating_visco.inp` and `CZM_sep.for` by taking `sig = 35d-3`, `sig = 110d-3` and `sig = 220d-3` in the subroutine.
 - Table 1: Taking `hs_ratio = 0d0` in the subroutine. Run simulations follow the tutorial in single simulation section by  taking `sig = 35d-3`, `sig = 110d-3` and `sig = 220d-3` in the subroutine.
 - Table 2: Taking `hs_ratio = 0.9d0` in the subroutine. Run simulations follow the tutorial in single simulation section by  taking `sig = 35d-3`, `sig = 110d-3` and `sig = 220d-3` in the subroutine.

