# Dynamic Pricing Strategies for Short–Term Rentals

_A dynamic revenue management framework for optimizing nightly rates on Airbnb listings in Chicago._

## Table of Contents

1. [Description](#description)  
2. [Key Features](#key-features)  
3. [Tech Stack](#tech-stack)  
4. [Installation](#installation)  
5. [Data](#data)  
6. [Usage](#usage)  
7. [Project Structure](#project-structure)  
8. [Configuration](#configuration)

---

## Description

This project implements a two-layer dynamic pricing model for short-term rental listings in Chicago. It combines second-degree price discrimination (segmentation by listing attributes) with third-degree discrimination (temporal adjustments for seasonality and weekends) to maximize expected nightly profit per listing segment.

## Key Features

- **Listing Segmentation**: K-means clustering to distinguish value vs. premium segments within neighborhoods.
- **Demand Estimation**: Logistic demand curves calibrated to historical booking rates.  
- **Elasticity Analysis**: Point-wise price elasticity computation for each segment.  
- **Static Optimization**: Analytical derivation of per-segment profit-maximizing prices.  
- **Dynamic Pricing**: Time-varying price modifiers (±10% seasonal sine wave, +5% weekend uplift).  
- **Policy Comparison**: Simulation of static, seasonal-only, weekend-only, and hybrid strategies over a one-year horizon.

## Tech Stack

- **Language:** Python 3.8+  
- **Notebooks:** Jupyter Notebook  
- **Libraries:** pandas, numpy, scikit-learn, matplotlib, lifelines  
- **Data:** listings.csv, feature_imp.csv  

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/dynamic-pricing-airbnb.git
   cd dynamic-pricing-airbnb
   ```
2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/macOS
   venv\Scripts\activate  # Windows
   ```
3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

## Data

- **`listings.csv`**: Cleaned dataset of 5,207 Chicago Airbnb listings (price, bedrooms, bathrooms, amenities, cleaning fee, occupancy flag).  
- **`feature_imp.csv`**: Feature importance scores or additional attributes used in clustering and modeling.  

> **Note:** The original raw data was scraped in May 2017; booking flags are simulated where missing.

## Usage

1. **Launch Jupyter Notebook**:
   ```bash
   jupyter notebook Group_Project_Team5_V3.ipynb
   ```
2. **Run the analysis** cells sequentially:
   - Data preparation and feature engineering.  
   - Neighborhood-level clustering.  
   - Demand curve fitting and elasticity calculation.  
   - Profit optimization and dynamic policy simulation.  
3. **View visualizations** of demand curves, profit curves, and hybrid dynamic paths.

## Project Structure

```
dynamic-pricing-airbnb/
├── README.md                # This file
├── requirements.txt         # Libraries and versions
├── listings.csv             # Cleaned listing data
├── feature_imp.csv          # Feature importance data
├── Group_Project_Team5_V3.ipynb  # Analysis notebook
└── figures/                 # Output visualizations (optional)
    ├── demand_curves.png
    └── hybrid_paths.png
```

## Configuration

- **Variable cost (`Cv`)**: Default set to $50 per booking (cleaning/service fee).  
- **Logistic steepness (`γ`)**: Default 0.05; adjust in notebook for calibration.  
- **Seasonal amplitude (`α`)**: ±10%; modify in the `s(t)` function.  
- **Weekend uplift (`ω`)**: +5% on Friday–Sunday; change in `ω(t)` definition.
