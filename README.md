# Mathematical Model of Cherry Tomato Growth 🍅

> Differential-equation models of cherry tomato biomass growth driven by real greenhouse sensor data (temperature, soil moisture, electrical conductivity and light), with parameter fitting and a sensitivity analysis of environmental factors.

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white)

Course project for **Modelos Matemáticos I**, Universidad Nacional de Colombia, Bogotá, 2024-2.

## Motivation

Climate change threatens food security, so getting the most out of each crop matters. Differential-equation models can help optimise irrigation, fertilisation and other agronomic practices. They do this by describing how a crop responds to its environment.

**Goal:** build a model of cherry tomato growth as a function of solar exposure, temperature, humidity and dissolved salts in the soil, then use it to find which conditions favour or harm growth.

## Data

[MoniFlora backup (Kaggle)](https://www.kaggle.com/datasets/andresaftari/moniflora-backup-rtdb) provides IoT plant-sensor time series with **conductivity, light, moisture and temperature**. The data was loaded with `mlcroissant`, cleaned (constant and irrelevant columns removed) and normalised.

## Models

1. **Biomass accumulation model.** Growth is driven by photosynthetically active radiation and resource-use efficiency. A resource function `recursos(T, M, C, L)` combines temperature, moisture, conductivity and light.
2. **Expo-linear model.** Growth is exponential early on and switches to linear after a transition time `t_switch`. This form best matches the growth patterns described in the plant-physiology literature.

Both ODE models are solved with `scipy.integrate.solve_ivp`. Total biomass is then split into fruit, leaf and stem fractions using typical cherry tomato biomass ratios.

## Parameter fitting & analysis

- No real biomass measurements were available, so **synthetic biomass data** was generated from the expo-linear model and perturbed with noise.
- The model parameters (α, γ, t_switch, k₁–k₄) were recovered by minimising the squared error with `scipy.optimize.minimize` (Powell, bounded). The fitted model was then used to **forecast** plant growth under the recorded sensor conditions.
- In the **sensitivity analysis**, each environmental input was varied by ± percentages to measure its effect on growth at each stage.

**Result:** in the model, adequate soil moisture, conductivity and good light have the strongest positive effect on growth. Low temperatures, low moisture and poor light are the most harmful.

## Possible extensions

- Calibrate with real biomass measurements.
- Apply the approach to other horticultural crops (peppers, strawberries, lettuce) by re-fitting the coefficients.

## How to run

Open [`Proyecto_Modelos.ipynb`](Proyecto_Modelos.ipynb) in Jupyter or Google Colab. The dataset is downloaded with `mlcroissant`.

```bash
pip install numpy pandas scipy matplotlib mlcroissant
```

## Team

Sofía Salinas Rico · **Laura Nicole Bermúdez Santa** · Vanessa Lozano Landinez
