# MODWT-MARS
Hybrid MODWT-MARS model for financial time series forecasting

A hybrid model that combines maximal overlap discrete wavelet transform multiresolution analysis with multivariate adaptive regression splines to give improved one-step-ahead forecasting.

The concept of this hyrbid model was inspired from this paper by Jothimani, D., Shankar, R., Yadav, S.S.:

[Discrete Wavelet Transform Based Prediction of Stock Index: A Study on National Stock Exchange FiftyIndex](https://arxiv.org/ftp/arxiv/papers/1605/1605.07278.pdf)

The premise of this model is to decompose the log-return of the closing price of a stock using MODWT multiresolution analysis and use the detail coefficients and smooth coefficient as inputs for the MARS model.

MODWT allows for decomposition of nondyadic lengthed data and is circular-shift invariant making it suitable for financial time series. MODWT decomposes a signal in time-frequency space, exposing hidden information in the orignal signal not seen otherwise.
Since the MODWT-MRA gives time-aligned decompositions it is used over MODWT alone. 

A level 3 MODWT-MRA, using a Dauchecies least asymtopic wavelet, is produced in R and a feature set is generated by taking the 4 previous values at each time step defined as: at time t, value x is defined as: 

![equation](http://latex.codecogs.com/gif.latex?x(t)%3Df(x(t-1),x(t-2),x(t-3),x(t-4))) This is done for the 3 detail coefficients D1, D2, D3 and the smooth coefficient S3

Each of these are used as input for the MARS model, where Adaboost and bagging regressor boosters are used and then combined using xgboost, then summed up afterwards to produce the final prediction vector.

**Requirments**
- numpy
- pandas
- statsmodels
- pandas datareader
- datetime
- matplotlib
- scipy
- xgboost
- [py-earth](https://github.com/scikit-learn-contrib/py-earth)
- sklearn



**In Sample Results**:
![alt text](https://github.com/Nicholas-Picini/MODWT-MARS/blob/master/Results/train.jpg)

**In Sample Results** (Zoomed in):
![alt text](https://github.com/Nicholas-Picini/MODWT-MARS/blob/master/Results/train_zoom.jpg)

**Directional Accuracy on predicted training set**:
![alt text](https://github.com/Nicholas-Picini/MODWT-MARS/blob/master/Results/DA_train.jpg)

**Out of Sample Results**:
![alt text](https://github.com/Nicholas-Picini/MODWT-MARS/blob/master/Results/test.jpg)

**Out of Sample Results** (Zoomed in, With one day ahead forecast):
![alt text](https://github.com/Nicholas-Picini/MODWT-MARS/blob/master/Results/test_zoom.jpg)

**Directional Accuracy on predicted test set with error metrics**:

![alt text](https://github.com/Nicholas-Picini/MODWT-MARS/blob/master/Results/DA_test.jpg)
