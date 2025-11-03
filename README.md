# MATH_789_final_project

# Credit Default Risk Simulation  
**Author:** *Your Name*  
**Course / Final Project Submission – [Insert Course Name or Institution]*  

---

## Overview
This project analyzes credit default risk using data from the UCI Default of Credit Card Clients dataset (available on Kaggle).  
It combines Exploratory Data Analysis (EDA) and a Monte Carlo simulation based on the Vasicek model to estimate portfolio losses, evaluate Value at Risk (VaR), and calculate Conditional Value at Risk (CVaR).

The goal is to understand potential credit losses under varying default probabilities and economic conditions by simulating correlated defaults across a portfolio of credit clients.

---

## Project Structure

```
.
├── 00_eda.ipynb              # Exploratory Data Analysis notebook
├── 01_simulations.ipynb      # Monte Carlo simulation and risk metrics
├── requirements.txt          # Python dependencies
└── README.md                 # Project documentation
```

---

## Dataset
**Source:** [UCI Default of Credit Card Clients Dataset](https://www.kaggle.com/uciml/default-of-credit-card-clients-dataset)

This dataset contains information on 30,000 Taiwanese credit card clients, including demographic variables, credit limits, past payment history, and default status.  
For this analysis, key variables used include:

- `LIMIT_BAL`: Credit line amount  
- `TARGET: Binary outcome variable indicating whether or not the client defaulted 
- `ID`: Unique client identifier  

---

## Methodology

### 1. Exploratory Data Analysis (EDA)
Performed in `00_eda.ipynb`, the EDA phase:
- Loads and cleans the dataset.  
- Examines variable distributions and correlations.  
- Identifies key features relevant to credit risk (focus on credit line and default status).

### 2. Monte Carlo Simulation
Implemented in `01_simulations.ipynb`, this step models **portfolio credit losses** under a correlated default framework:

#### Model Assumptions:
- Default correlation: `ρ = 0.04`  
- Probability of default: `p = 0.05`  
- Portfolio size: 30,000 clients  
- Number of simulations: 1,000  

Each simulation introduces:
- A **systematic factor** (economic environment) shared across borrowers.  
- An **idiosyncratic factor** unique to each borrower.  
- Defaults determined by the **Vasicek model threshold** `X < Φ⁻¹(p)`.

#### Computed Metrics:
- **Expected Loss (EL)** – Average simulated portfolio loss  
- **Value at Risk (VaR)** – 90%, 95%, and 99% quantiles of loss distribution  
- **Conditional VaR (CVaR)** – Mean losses beyond each VaR threshold  

---

## Results Summary

| Metric | 90% | 95% | 99% |
|:--------|:----:|:----:|:----:|
| **Value at Risk (VaR)** | NT$ *VaR₉₀* | NT$ *VaR₉₅* | NT$ *VaR₉₉* |
| **Conditional VaR (CVaR)** | NT$ *CVaR₉₀* | NT$ *CVaR₉₅* | NT$ *CVaR₉₉* |

*(Actual numerical results printed in the notebook output)*

The histogram of total simulated losses illustrates a right-skewed loss distribution, emphasizing tail risk.  
Interpretation examples:
- In 95% of cases, losses do not exceed the 95% VaR threshold.
- In the worst 5% of cases, expected losses correspond to the 95% CVaR.

---

## ⚙️ Installation and Setup

### 1. Clone the repository:
```bash
git clone https://github.com/jordanandrewww/credit-default-simulation.git
cd credit-default-simulation
```

### 2. Install dependencies:
```bash
pip install -r requirements.txt
```

### 3. Run the notebooks:
Open the Jupyter notebooks in VS Code, Jupyter Lab, or Google Colab:
```bash
jupyter notebook 00_eda.ipynb
jupyter notebook 01_simulations.ipynb
```

---

## Dependencies
From `requirements.txt`:
```
pandas
numpy
matplotlib
seaborn
scipy
kagglehub
```

---

## Interpretation and Insights
The simulation highlights:
- The importance of default correlation in amplifying portfolio losses.
- How VaR and CVaR capture tail risk exposure in credit portfolios.
- Even with a moderate 5% individual default rate, correlated defaults can cause significant aggregate losses.

---

## Future Work
- Vary correlation and default rates to stress-test outcomes.  
- Incorporate time-dependent macroeconomic factors.  
- Visualize joint distribution of defaults and losses interactively. 
