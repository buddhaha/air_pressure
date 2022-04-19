# AirPump failures

A customer is manufacturing devices containing air pumps that provide pressure for a machine cycle. Ideally, the air pressure rises sharply and remains stable throughout the machine's cycle, where it drops sharply. However, it can happen that the air pressure drops due to pump failure, or the air pressure rises or drops slowly.

The goal of the project is to detect a pump failure.
The typical air pump failure is a temporary pressure decrease in the first half of the cycle.


## Data structure


### Data

The data consists of the following columns (in this particular order):

- MachineId - Id of the machine
- MeasurementId - Id of the measured cycle
- Pressure - Air pressure (kPa)

The data does not consist timestamps as they are not relevant.

### Labels

The labels consists of the following columns (in this particular order):

- MachineId - Id of the machine
- MeasurementId - Id of the measured cycle
- PumpFailed - True if pump failed
- SlowStart - True if the preasure rised slowly
- SlowEnd - True if the presure dropped slowly


## Your task:

- Develop a predictive model for the PumpFailed column and report its accuracy in appropriate metrics.
- Explain your model.


## Notes

- We suggest you to use Python and Jupyter notebook for this assignment.


## Requirements

- Spend maximum of one working day on this assignment
- Document your work so the Jupyter notebook is self-explanatory

# Approach
1) As a first step, I want to build MVP (a model in the easiest possible way: dropping nans and working with simplified columns.)
   1) explore and clean data
   2) Make a comparison of few models that might work for binary classification (like log reg; random decission tree, svm) to have an idea
   3) fine tuning e.g. grid search
   
after approximately 6-8h of focused work:
- I managed to build a basic model (LogReg; I tried also others but with similar poor results) for binary classification (on imbalanced data ~90% False) based on statistical values from Pressure measurements
- 1st improvement: using bins from Pressure vals histogram; however model was even worse
 
- NOTE: as the dataset is imbalanced, we cannot use just accuracy to evaluate the model, but also precision, recall, and F1 score is needed

### proposed ways: try several things to improve model:
## 0) combine several features from Pressure measurements seems to be necessary : think about what might be the most influential
## 1) normalization of features, up to now I've tested histogram values with density=True/False (should normalize hists), however, performance is still poor
## 2) include more features in the model : not just histogram values, but also count/% of values where Pressure=0; Pressure is around mean value etc. ; maybe fit histogram with some distribution?
## 3) improve input data : fill missing values (build separe model for e.g. slowstart/slowend col, use interpolate functions to approximate missing values)
## 4) try to deal with the imbalanced data set problem (e.g. Resampling (Oversampling and Undersampling); SMOTE;BalancedBaggingClassifier)
## 5) try more algorithms for classification / find best params with gridsearch
