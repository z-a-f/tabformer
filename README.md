
# Before Everything

```
git config --local include.path ../.gitconfig
git submodule sync
git submodule update --init --recursive
```

# To Train XGBoost Models

1. Run the `XGBT_Adult_Demo.ipynb`
2. Models are stored under `models/gbdt/<dataset_name>.{json,png}`

![It takes very long](assets/images/resource_utilization.png)
**Before training all the models using a grid search, make sure you have a GPU-enabled XGB**