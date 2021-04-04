# MechanismOfActionPredictions
The notebooks from the Kaggle competition Mechanisms of Action (MoA) Prediction from Andy and Andre. The notebook TabNet+ANN|0.01612LB was our best submission, scoring a top 4% in the leaderboard. A brief overview of our solution:

## Preprocessing/Feature Engineering

  - Removed control group
  - Deleting the features with an information gain of 0.06 or less, acheieved using the ``` mutual_info_classif``` function from sklearn.
  - Perform PCA, selecting the top 20, 60 features from cells, genes, respectively, then adding them back to the original data.
  - Perform normalization to the data using the ```GaussRankScaler```.
  - Calculating the statistics of the features, performed on genes and cells seperately.
  - Added the ```cp_dose_time``` feature by combining ```cp_time``` and ```cp_dose```.
  - Label encoded  ```cp_time``` and ```cp_dose_time```, then one hot encoded the rest of the categorical features.
  
## Models and Training
  
  - We trained two TabNets on different seeds and one two layer Neural Network, then blended the predictions with weighted average.
  - Optimizers: TabNet, AdaBelief. NN, AdamW.
  - LrScheduler: ReduceLROnPlateau
  - Validation Scheme: MultiStratifiedKFold
  - Folds: 10
