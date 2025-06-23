# CO2BLOCKSEISM

![CI](https://github.com/imanrahimzadeh/CO2BLOCKSEISM/actions/workflows/ci.yml/badge.svg?branch=main)

An analytical tool for screening subsurface CO<sub>2</sub> storage resources
constrained by induced seismicity

CO2BLOCKSEISM extends the tool [CO2BLOCK](https://github.com/co2block/CO2BLOCK),
which estimates and optimizes CO<sub>2</sub> storage capacity subject to
reservoir injectivity limitations. To learn more about the theory behind
CO2BLOCKSEISM, please refer to the following paper:

- Kivi, I.R., De Simone, S. and Krevor, S., 2024. A simplified physics model for
  estimating subsurface CO<sub>2</sub> storage resources constrained by fault
  slip potential. EarthArXiv. <https://doi.org/10.31223/X5KM65>

The CO2BLOCKSEISM tool is provided here in the context of two demonstration
studies: [Oklahoma
seismicity](https://github.com/imanrahimzadeh/CO2BLOCKSEISM/tree/main/Oklahoma%20seismicity)
and [Utsira storage
capacity](https://github.com/imanrahimzadeh/CO2BLOCKSEISM/tree/main/Utsira%20storage%20capacity).
A general version of the code that can be applied to any study will be provided
soon in this repository.

Should you have any questions/comments/suggestions, please contact Iman R. Kivi
through the email <i.rahimzadeh-kivi@imperial.ac.uk>

CO2BLOCKSEISM is open-source software. If you use it for academic purposes,
please cite the reference paper above.

## **Code structure**

The tool comprises a number of scripts and functions as detailed below:

- "CO2BLOCKSEISM.m": this is the main script, where all input data for the study
  are specified. This script calls several functions to perform the required
  calculations,
- "read_data.m": this function reads the input parameters from the input Excel
  file,
- "hydrogeology.m": this function involves analytical solutions of the pressure
  response of saline aquifers to multi-site CO<sub>2</sub> injection at
  time-varying rate,
- "Geomech_prob.m": this function develops a Monte Carlo-type probabilistic
  model for evaluating the probability of fault slip under inherent
  uncertainties of the geomechanical parameters of the subsurface,
- "Analytical_solution.m" and "FD_Nor_2zones.m": these functions calculate
  pressure changes in a saline aquifer in response to two phase flow of
  CO<sub>2</sub> and water around a single injection site based on the
  analytical solution by Nordbotten et al. (2005). A simplified solution for
  single phase flow of water is used for the demonstration study of induced
  seismicity in Oklahoma,
- "stress_projection.m": this function projects shear and normal stress
  components onto the fault planes for different realizations of the Monte Carlo
  simulation,
- "eos.m": this function returns brine viscosity and CO<sub>2</sub> density and
  viscosity using appropriate equations of state,
- "plot.m": this script visualizes the output data through appropriate plots.
  Scientific colormaps developed by Fabio Crameri (2018) are used in these
  plots. The functions, database and instructions for using Crameri's colormaps
  are also provided.

## **Input**

Input parameters are introduced to the tool either directly within the script
"CO2BLOCKSEISM.m" or through the input .xlsx file. The input file involves
average values of the hydraulic properties of the aquifer required to estimate
injection-induced pressure changes and the geomechanical properties of the
seismogenic rock layers needed to estimate the potential for induced seismicity.
The seismogenic layer can be the storage aquifer or hydraulically connected
formations overlying or underlying the storage aquifer. Note that the input file
has a fixed structure and the order of the input variables must not be changed.
There is a set of strictly required parameters, while there is the possibility
of using default values for the others, as explained in the example input data
files. Although default values provide reasonable estimations, we recommend the
use of precise data which would allow for a more accurate prediction of the
storage capacity.

Information about the statistical distributions of uncertain geomechanical
parameters, discretization in time and space, injection schedules and
distributions of injection sites and faults are specified in the script
"CO2BLOCKSEISM.m". The script reads data for the distributions of the injection
sites and faults from separate input .xlsx files. Additional information, e.g.,
geographical data or induced seismicity records may be added for use in the
plots.

## **Output**

The main outputs of the tool are the spatial and temporal evolution of
injection-induced pore pressure changes, fault slip probability, possible
earthquake magnitudes and the maximum CO<sub>2</sub> storage capacity that can
be safely achieved. The tool saves the plots in the specified directory.

The results of the tool calculations for the two demonstration studies are
provided as "Results_Utsira.mat" and "Results_OK.mat". One may simply load the
results and just run the script "plot.m" to reproduce all figures presented in
the reference paper mentioned above. Alternatively, the script "CO2BLOCKSEISM.m"
with the provided input data can be run to regenerate the results.
