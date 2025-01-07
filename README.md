# Fee Optimization and Forecasting Model

This repository contains Python code for optimizing broker fees across different plans and forecasting future fees using ARIMA and XGBoost hybrid models. The code integrates data processing, fee calculation, plan optimization, and advanced forecasting techniques.

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Data Requirements](#data-requirements)
  - [Key Functions](#key-functions)
  - [Execution](#execution)
- [Dependencies](#dependencies)
- [Outputs](#outputs)
- [Contact](#contact)

## Project Overview

This project is designed to:
1. Process trade and fee data to calculate monthly fees for different plans.
2. Identify optimal plans that minimize fees using linear programming.
3. Perform time-series decomposition and hybrid ARIMA-XGBoost forecasting to predict future fees.

## Features

- **Data Processing**: Preprocesses trade and fee schedules for analysis.
- **Fee Calculation**: Computes monthly fees for various plans, including minimum commitments.
- **Plan Optimization**: Solves a Mixed-Integer Linear Programming (MILP) problem to optimize plan selection, considering switching costs.
- **Forecasting**: Implements a hybrid ARIMA-XGBoost model for future fee prediction.
- **Visualization**: Plots plan selections and forecasting results.

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/your-repo/fee-optimization.git
   ```
2. Install required Python libraries:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Data Requirements

The program expects an Excel file containing the following sheets:
1. **Trade Details**: Includes columns such as `Trade Date`, `DateUsedFeeCalc`, `Product`, `Local Size`, etc.
2. **Fee Schedules**: Contains fee rates and minimum monthly commitments for each plan.
3. **GBP Reference Fee**: Provides GBP exchange rates for different months.

### Key Functions

#### Data Loading and Processing
- `load_data(file_path)`: Loads data from an Excel file.
- `process_trade_details(trade_details_df)`: Processes trade details by calculating days differences and assigning maturity brackets.
- `prepare_monthly_data(merged_df, gbp_ref_fee_df)`: Merges monthly data with GBP reference fees.

#### Fee Calculation
- `calculate_plan_fees(merged_df, plan_prefix)`: Computes fees for a specific plan.
- `calculate_monthly_fees(merged_df, fee_schedules_df)`: Calculates fees for all plans monthly.

#### Optimization
- `create_optimization_problem(optimal_plan_df, switching_cost)`: Sets up and solves a fee optimization problem.
- `_add_plan_constraints(prob, x, switch, plans, months)`: Adds constraints to the optimization problem.

#### Forecasting
- `test_stationarity(data, column)`: Performs the Augmented Dickey-Fuller test for stationarity.
- `decompose_time_series(data, column, frequency)`: Decomposes time-series data into trend, seasonal, and residual components.
- `arima_xgb_hybrid_forecast(data, column, test_data, forecast_periods, arima_order)`: Performs ARIMA-XGBoost hybrid forecasting.

### Execution

1. Prepare your Excel file with the required data.
2. Run the main function with the file path as input:
   ```python
   result = main("path_to_your_file.xlsx")
   ```
3. Outputs include optimized plan details, fee results, and visualizations.

## Dependencies

- Python 3.7+
- pandas
- numpy
- seaborn
- matplotlib
- pulp
- statsmodels
- xgboost
- sklearn

Install dependencies using the provided `requirements.txt`.

## Outputs

- **Excel File**: `detailed_plan_results.xlsx` containing optimized plans and fees.
- **Plots**:
  - Monthly plan selection based on optimization.
  - Time-series decomposition and forecasting results.
- **Metrics**:
  - Root Mean Square Error (RMSE)
  - R-squared (R2)

## Contact

For questions or feedback, please contact:
- **Name**: Jills Jose
- **Email**: j.jose@student.vu.nl

---

**Note**: Ensure data confidentiality when working with sensitive trade and fee data.

