# MLGEO2024_NaCl_EoS
Fall 2024 ESS 569 project to increase efficiency of equation of state calculations for NaCl(aq) up to 1 GPa, 500 K, 7 mol/kg.

[Project Description](#project-description) •
[Installation](#installation) •
[How to Run](#how-to-run) •
[Notebook Descriptions](#notebook-descriptions) •
[License](#license)
</div>

## Project Description
Fall 2024 ESS 569 project to increase efficiency of equation of state calculations for NaCl(aq) up to 1 GPa,  500 K, 7 mol/kg.

### Motivations
There is currently a need in the planetary science community for flexible representations describing the thermodynamic conditions of water and solutions at extreme low temperature and high pressure conditions relevant to icy moon and water rich exoplanet interiors. My group has developed a number of such equations of state, including one for aqueous NaCl. However, current calculations using novel b-spline EoS for ice and solutions at extreme conditions are often too slow for implementation in icy moon and exoplanet geodynamic models--therefore, I am aiming to increase calculation efficiency with this project.

### Objectives 
Recent benchmarking shows it takes ~20 seconds to calculate 1,000 pts; an optimisitic goal is to decrease this by a factor of 10. I will used a supervised learning approach to train on model PTM data up to 1 GPa, 500 K, and concentrations of 7 mol/kg. 

### Data
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

These thermodynamic models are self consistent, as all properties are derived as combinations of derivatives of Gibbs energy. They are designed for ease of implementation in models of icy moon and water rich exoplanet interiors, as these are the environments in which solutions and ice are found at extreme pressure and low temperature conditions. However, the current routine of evaluating the spline functions (especially over a list of scattered points) is computationally slow relative to the needs of the most sophisticated models. Therefore, my goal is to use supervised learning to develop an ML algorithm that will accurately predict properties without evaluating the full EoS.

The model data I am using is currently hosted on google drive (available here): https://drive.google.com/drive/folders/1_uFESfnrcsbmZZ5INQRrxB_oK4BcsKiu?usp=drive_link 

## Installation
Copy the project onto your local machine with git clone:

```bash
git clone https://github.com/UW-MLGEO/MLGEO2024_ulajones.git
```
Then cd to the location of the local repo, create a conda environment using the eos_env.yml file, and activate it:
```bash
cd path_to_repo/
conda env create -f eos_env.yml -n eos_env
conda activate eos_env
```

Necessary packages include:
- seafreeze
- pyarrow 
- os
- pandas
- numpy
- seaborn
- matplotlib
- sklearn
- pycaret
- keras 

## How to Run

Open jupyter notebook or jupyter lab:
```bash
jupyter notebook
```
And navigate to the first notebook, titled "generate_and_clean_model_NaClaq_data.ipynb" 

## Notebook Descriptions

**generate_and_clean_model_NaClaq_data.ipynb**: generates and cleans the dataset for aqueous NaCl solutions, preparing it for further analysis and modeling

**Dimensionality_Reduction.ipynb**: applies dimensionality reduction techniques to the NaCl aqueous solutions dataset, such as Principal Component Analysis (PCA), to reduce the number of features while retaining essential information, with the aim of improving model efficiency 

**EDA.ipynb**: performs exploratory data analysis (EDA) on the dataset, visualizing key features and identifying patterns to inform subsequent modeling efforts.

**auto_ml.ipynb**: uses automated machine learning techniques from pycaret to find the best model(s) and tuned hyperparameters for the regression 

**model_training_assessment.ipynb**: trains various machine learning models on the cleaned NaCl dataset, evaluates their performance, and assesses accuracy and generalization capabilities

**computational_time_analysis.ipynb**: analyzes the computational time required for training and deploying different machine learning models, exploring the trade-offs between accuracy and computational cost

**deep_learning_exploration.ipynb**: implements several DL approaches including an FNN, an RNN, and a physically informed custom loss function. Benchmarks DL approaches aghainst CML and discusses tradeoffs.

## License
This open source code is distributed under an MIT license, which allows its usage, modification, and distribution subject to basic preservation of copyright and license notices.
