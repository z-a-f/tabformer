
# Before Everything

If contributing, make sure you run these commands

```
git config --local include.path ../.gitconfig
git submodule sync
git submodule update --init --recursive
```

# Models

## XGBoost (non-DP)

### Training

1. Run the `XGBT_Adult_Demo.ipynb`
2. If need to change the grid search parameters, or skip the grid search completely (for debugging)
   - Find the cell where `grid_search_parameters` is defined, and comment out its contents
4. Models are stored under `models/gbdt/<dataset_name>.{json,png}`

### Training results (XGBoost)

| Dataset    | best_ntree_limit | max_depth | alpha | lambda | eta | error (T) | error (V) | auc (T) | auc (V) |                Training History                |
|------------|------------------|-----------|-------|--------|-----|-----------|-----------|---------|---------|:----------------------------------------------:|
| creditg    | 53               | 10        | 1e-06 | 1e-06  | 0.3 | 0.00      | 0.26      | 1.00    | 0.80    |    ![creditg](models/gbdt/creditg_plot.png)    |
| income     | 26               | 6         | 1.0   | 1e-08  | 0.3 | 0.12      | 0.13      | 0.94    | 0.92    |     ![income](models/gbdt/income_plot.png)     |
| diabetes   | 30               | 2         | 1e-08 | 0.1    | 0.3 | 0.16      | 0.27      | 0.92    | 0.83    |   ![diabetes](models/gbdt/diabetes_plot.png)   |
| calhousing | 40               | 4         | 1.0   | 1.0    | 0.3 | 0.10      | 0.20      | 0.97    | 0.90    | ![calhousing](models/gbdt/calhousing_plot.png) |
| blood      | 24               | 2         | 1.0   | 1e-08  | 0.3 | 0.21      | 0.12      | 0.80    | 0.42    |      ![blood](models/gbdt/blood_plot.png)      |
| heart      | 8                | 4         | 0.01  | 1.0    | 0.3 | 0.07      | 0.18      | 0.98    | 0.90    |      ![heart](models/gbdt/heart_plot.png)      |
| car        | 28               | 10        | 1e-07 | 1e-08  | 0.3 | 0.00      | 0.21      | 1.00    | 0.94    |        ![car](models/gbdt/car_plot.png)        |
| jungle     | 43               | 2         | 0.1   | 1.0    | 0.3 | 0.15      | 0.22      | 0.93    | 0.88    |     ![jungle](models/gbdt/jungle_plot.png)     |
| bank       | 25               | 2         | 1.0   | 1.0    | 0.1 | 0.06      | 0.15      | 0.93    | 0.80    |       ![bank](models/gbdt/bank_plot.png)       |

#### Model Comparison

| Dataset    | XGBoost | XGBoost + DP ($\varepsilon=5$) | Tab Transformer | Tab Transformer + DP ($\varepsilon=5$) |
|------------|---------|--------------------------------|-----------------|----------------------------------------|
| creditg    | 0.80    | 0.78                           | 0.81            | 0.80                                   |
| income     | 0.92    | 0.91                           | 0.85            | 0.83                                   |
| diabetes   | 0.83    | 0.76                           | 0.81            | 0.72                                   |
| calhousing | 0.90    | 0.89                           | 0.84            | 0.77                                   |
| blood      | 0.42    | 0.63                           | 0.86            | 0.69                                   |
| heart      | 0.90    | 0.90                           | 0.74            | 0.72                                   |
| car        | 0.94    | 0.93                           | 0.92            | 0.88                                   |
| jungle     | 0.88    | 0.80                           | 0.81            | 0.73                                   |
| bank       | 0.80    | 0.74                           | 0.63            | 0.64                                   |


# Notes

## Before training all the models using a grid search, make sure you have a GPU-enabled XGB
![It takes very long](assets/images/resource_utilization.png)
