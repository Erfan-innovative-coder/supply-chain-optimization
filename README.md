## Project Overview

This project combines **Machine Learning** and **Operations Research** for data-driven supply chain planning.

A Random Forest model is used to forecast customer demand. The predicted demand is then used in a Mixed-Integer Linear Programming (MILP) model developed with PuLP to optimize supplier allocation, warehouse utilization, and customer fulfillment.

The synthetic supply chain consists of 3 suppliers, 5 warehouses, and 20 customers.

## Using Libraries

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-lightblue)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-blue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-Machine%20Learning-orange)
![PuLP](https://img.shields.io/badge/PuLP-Optimization-green)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-blue)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-lightblue)
![NetworkX](https://img.shields.io/badge/NetworkX-Network%20Analysis-yellow)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)

## Project Workflow

1. Synthetic data generation
2. Exploratory data analysis
3. Demand analysis and visualization
4. Supply chain network construction
5. Baseline supply chain optimization
6. Supplier capacity sensitivity analysis
7. Customer demand forecasting using Random Forest
8. Forecast-based supply chain optimization
9. Historical vs. forecast-driven comparison
10. Model evaluation and visualization

## Supply Chain Network

![Supply Chain Network](figures/supply_chain_network.png)

### Dataset

| Component | Quantity |
|---|---:|
| Suppliers | 3 |
| Warehouses | 5 |
| Customers | 20 |
| Products | 1 |
| Historical demand period | 30 days |
| Forecast horizon | 30 days |

### Supplier Information

| Supplier | Daily Capacity | Unit Cost |
|---|---:|---:|
| S1 | 100 | 12.0 |
| S2 | 150 | 10.5 |
| S3 | 120 | 13.0 |

Total supplier capacity: **370 units per day**.

### Customer Priority

- High: Shortage penalty = 30
- Medium: Shortage penalty = 20
- Low: Shortage penalty = 10

## Exploratory Data Analysis

### Daily Demand

![Daily Total Demand](figures/daily_total_demand.png)

![Historical Daily Demand](figures/historical_daily_demand.png)

### Demand Distribution

![Average Demand by Customer](figures/average_demand_by_customer.png)

![Demand by Priority](figures/demand_by_priority.png)

## Optimization Model

The optimization model is developed using **PuLP** and the CBC solver.

The objective is to minimize total supply chain cost, including:

- Supplier purchasing costs
- Inbound transportation costs
- Outbound transportation costs
- Warehouse fixed operating costs
- Customer shortage penalties

### Model Constraints

- Supplier capacity
- Warehouse flow balance
- Warehouse throughput capacity
- Customer demand fulfillment
- Warehouse activation decisions

### Supplier and Warehouse Allocation

![Supplier Warehouse Allocation](figures/supplier_warehouse_allocation.png)

![Warehouse Customer Allocation](figures/warehouse_customer_allocation.png)

### Cost Analysis

![Cost Breakdown](figures/cost_breakdown.png)

![Cost Comparison](figures/cost_comparison_40_vs_50.png)

## Capacity Sensitivity Analysis

Supplier capacity is increased under different scenarios to evaluate its impact on fulfillment and total modeled cost.

### Supplier Capacity

![Supplier Capacity Analysis](figures/supplier_capacity_analysis.png)

![Capacity Saturation Analysis](figures/capacity_saturation_analysis.png)

### Historical Demand Scenarios

![Historical Scenario Fill Rate](figures/scenario_fill_rate.png)

![Historical Scenario Total Cost](figures/scenario_total_cost.png)

### Forecast Demand Scenarios

![Forecast Scenario Fill Rate](figures/forecast_scenario_fill_rate.png)

![Forecast Scenario Total Cost](figures/forecast_scenario_total_cost.png)

## Demand Forecasting

A Random Forest Regressor is used to forecast customer demand.

### Input Features

- `lag_1`
- `lag_7`
- `rolling_mean_7`
- `day_of_week`
- `average_daily_demand`

### Model Evaluation

The Random Forest model is compared with a 7-day lag baseline.

| Model | MAE | RMSE | WAPE |
|---|---:|---:|---:|
| 7-Day Lag Baseline | 6.69 | 8.31 | 13.66% |
| **Random Forest** | **5.65** | **7.09** | **11.54%** |

### Actual vs. Predicted Demand

![Demand Forecast](figures/demand_forecast_actual_vs_predicted.png)

### Feature Importance

![Random Forest Feature Importance](figures/random_forest_feature_importance.png)

### Forecasting Error Analysis

![Customer Forecasting Error](figures/customer_forecasting_error_analysis.png)

## Optimization Results

### Historical vs. Forecast-Driven Optimization

| Metric | Historical Demand | Forecast Demand |
|---|---:|---:|
| Total Demand | 29,388.00 | 29,357.10 |
| Delivered Quantity | 11,100.00 | 11,100.00 |
| Unmet Demand | 18,288.00 | 18,257.10 |
| Fill Rate | 37.77% | 37.81% |
| Total Modeled Cost | 505,215.28 | 504,744.92 |

### Delivered Quantity Comparison

![Delivered Quantity Comparison](figures/comparison_delivered.png)

### Fill Rate Comparison

![Fill Rate Comparison](figures/comparison_fill_rate.png)

### Total Cost Comparison

![Total Cost Comparison](figures/comparison_total_cost.png)

### Customer Fulfillment

![Customer Fulfillment Comparison](figures/customer_fulfillment_comparison.png)

![Fulfillment by Priority](figures/fulfillment_by_priority.png)

## Key Findings

- Supplier capacity is the main bottleneck in the baseline scenario.
- Increasing supplier capacity improves customer fulfillment.
- Random Forest outperforms the 7-day lag baseline across MAE, RMSE, and WAPE.
- Forecast-driven optimization produces results close to the historical-demand scenario.
- Higher shortage penalties encourage prioritization of high-priority customers.

## Project Structure

```text
supply-chain-optimization/
│
├── Supply_Chain_Optimization_Organized.ipynb
│
├── figures/
│   ├── average_demand_by_customer.png
│   ├── capacity_saturation_analysis.png
│   ├── comparison_delivered.png
│   ├── comparison_fill_rate.png
│   ├── comparison_total_cost.png
│   ├── cost_breakdown.png
│   ├── cost_comparison_40_vs_50.png
│   ├── customer_forecasting_error_analysis.png
│   ├── customer_fulfillment_comparison.png
│   ├── daily_total_demand.png
│   ├── demand_by_priority.png
│   ├── demand_forecast_actual_vs_predicted.png
│   ├── forecast_scenario_fill_rate.png
│   ├── forecast_scenario_total_cost.png
│   ├── fulfillment_by_priority.png
│   ├── historical_daily_demand.png
│   ├── random_forest_feature_importance.png
│   ├── scenario_fill_rate.png
│   ├── scenario_total_cost.png
│   ├── supplier_capacity_analysis.png
│   ├── supplier_warehouse_allocation.png
│   ├── supply_chain_network.png
│   └── warehouse_customer_allocation.png
│
├── README.md
└── requirements.txt
```

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Erfan-innovative-coder/supply-chain-optimization.git
cd supply-chain-optimization
```

### 2. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn networkx scikit-learn pulp jupyter
```

### 3. Check the Optimization Solver

The notebook uses PuLP with the CBC solver through `pulp.COIN_CMD`.

```python
import pulp

print(pulp.listSolvers(onlyAvailable=True))
```

Make sure CBC is installed and available in your environment.

### 4. Run the Notebook

```bash
jupyter notebook
```

Open `Supply_Chain_Optimization_Organized.ipynb` and run the cells in order.

## Notes

- All datasets are synthetically generated.
- The optimization model uses an aggregate 30-day planning horizon.
- Warehouse capacity represents throughput capacity, not storage capacity.
- Capacity expansion investment costs are not included.
- The forecasting test period is limited to 7 days.
- Some optimization scenarios returned a `GapLimit` status; these solutions should not be interpreted as certified global optima.
'''

path = Path("/mnt/data/README.md")
path.write_text(readme, encoding="utf-8")
print(f"Created: {path}")
print(f"Size: {path.stat().st_size:,} bytes")
