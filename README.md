# MLGEO2024_NaCl_EoS
Fall 2024 ESS 569 project to increase efficiency of equation of state calculations for NaCl(aq) up to 10 GPa, 8 mol/kg.

The data are sourced from the Gibbs energy local basis function equation of state (EoS) for NaCl(aq) by JM Brown and B Journaux, currently hosted in the open source SeaFreeze repository (https://github.com/Bjournaux/SeaFreeze). The python implementation was developed by P Espinoza and myself last winter. The dataset spans 22 thermodynamic variables for NaCl-water solutions of 0-7 mol/kg NaCl from 240-501 K and 0-1,000 MPa (1 GPa). Variables and units are as follows:

| Quantity  (PT and PTm)      |  Symbol in SeaFreeze  |  Unit (SI)  |
| --------------- |:---------------------:| :----------:|
| Gibbs Energy           | `G` | J/kg |
| Entropy                | `S` | J/K/kg |
| Internal Energy        | `U` | J/kg |
| Enthalpy               | `H` | J/kg |
| Helmholtz free energy  | `A` | J/kg |
| Density                |`rho`| kg/m^3 |
| Specific heat capacity at constant pressure|`Cp`| J/kg/K |
| Specific heat capacity at constant volume|`Cv`| J/kg/K |
| Isothermal bulk modulus      |`Kt`| MPa |
| Pressure derivative of the Isothermal bulk modulus|`Kp`| - |
| Isoentropic bulk modulus     |`Ks`| MPa |
| Thermal expansivity     |`alpha`| /K |
| Bulk sound speed     |`vel`| m/s |
| Solute Chemical Potential           | `mus` | J/mol |
| Solvent Chemical Potential                | `muw` | J/mol |
| Partial Molar Volume        | `Vm` | cc/mol |
| Partial Molar Heat Capacity               | `Cpm` | J/kg/K/mol |
| Apparent Heat Capacity  | `Cpa` | J/kg/K/mol |
| Apparent Volume                |`Va`| cc/mol |
| Excess Volume|`Vex`| cc/mol |
| Osmotic Coefficient|`phi`| -|
| Water Activity      |`aw`| - |
| Activity Coefficient|`gam`| - |
| Excess Gibbs Energy     |`Gex`| J/kg |

These thermodynamic models are self consistent, as all properties are derived as combinations of derivatives of Gibbs energy. They designed for ease of implementation in models of icy moon and water rich exoplanet interiors, as these are the environments in which solutions and ice are found at extreme pressure and low temperature conditions. However, the current routine of evaluating the spline functions (especially over a list of scattered points) is computationally slow relative to the needs of the most sophisticated models. Therefore, my goal is to use supervised learning to develop an ML algorithm that will accurately predict properties without evaluating the full EoS.

The model data I am using is currently hosted on google drive (available here): https://drive.google.com/drive/folders/1_uFESfnrcsbmZZ5INQRrxB_oK4BcsKiu?usp=drive_link 

Necessary packages include:
- seafreeze
- pyarrow 
- os
- pandas
- numpy
- seaborn
- matplotlib
- sklearn
