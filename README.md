XGBoost.jl
==========

eXtreme Gradient Boosting Package in Julia

## Abstract

This package is a Julia interface of [XGBoost](https://github.com/tqchen/xgboost),
which is short for eXtreme gradient Gradient Boosting.  It is an efficient and scalable implementation of
gradient boosting framework.The package includes efficient linear model
solver and tree learning algorithms. The library is parallelized using OpenMP,
and it can be more than 10 times faster some of than existing gradient boosting packages.
It supports various objective functions, including regression, classification and ranking.
The package is also made to be extensible, so that users are also allowed to define their own objectives easily.

## Installation
```julia
Pkg.add("XGBoost")
```
or
```julia
Pkg.clone("https://github.com/antinucleon/XGBoost.jl.git")
```

then run

```julia
Pkg.build("XGBoost")
```

The `XGBoost` package also depends on the `BinDeps`


## Minimal examples

To show how XGBoost works, here is an example of dataset Mushroom

- Prepare Data
XGBoots use DMatix as inner data struct, DMatrix can be built from libsvm txt, XGBoost buffer file, Julia sparse Matrix and Julia dense matrix.
```julia
using XGBoost

dtrain = DMatrix("demo/agaricus.txt.train")
dtest = DMatrix("demo/agaricus.txt.test")
```

- Fit Model
```julia
param = ["max_depth"=>2, "eta"=>1, "silent"=>1]
num_round = 2
bst = xgboost(dtrain, num_round, param=param)
```

## Predict
```julia
pred = predict(bst, dtest)
```

## Cross-Validation
```julia
nfold=5
metrics = ["auc"]
nfold_cv(dtrain, num_round, nfold, param, metrics=metrics)
```

## Feature Walkthrough
Check [demo](https://github.com/antinucleon/XGBoost.jl/blob/master/demo/)

- [Basic walkthrough of wrappers](demo/basic_walkthrough.jl)
- [Cutomize loss function, and evaluation metric](demo/custom_objective.jl)
- [Boosting from existing prediction](demo/boost_from_prediction.jl)
- [Predicting using first n trees](demo/predict_first_ntree.jl)
- [Generalized Linear Model](demo/generalized_linear_model.jl)
- [Cross validation](demo/cross_validation.jl)


## Model Parameter Setting
Check [XGBoost Wiki](https://github.com/tqchen/xgboost/wiki)


