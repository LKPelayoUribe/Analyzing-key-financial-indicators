# Analyzing-key-financial-indicators
### By: Laura Pelayo, Shawn Petersen, Josh Pickel, Justin Pickel
Statistical Modeling for Data Analytics - This research paper provides an analysis of key stock indicators and whether can they be used to predict next-day closing prices, with the following models:

- Linear regression
- Lasso regression 
- Ridge regression
- Generalized additive (GAM)

***Disclaimer:** We are aware that we violated the assumption that our observations are not independent. Be aware these models need to be taken with a grain of salt and not be used for day trading.*

## Datasource and approach
Our dataset ‘bitcoin_clean.csv’ was created by pulling in bitcoin price data from yahoo finance over the last 2 years. We then added 14 technical indicators to our data set by utilizing a technical indicator package in python.
Indicators - {volumne, macd_26, macd_9, macd_diff, adx, adx_neg, adx_pos, span_a, span_b, kijun, tenkan, rsi, cmf, sma}

Bitcoin (BTC) is a consensus network that enables a new payment system and a fully digital currency. Powered by its users, it peers into a payment network that does not require a central authority to operate. Our team has decided to answer the question, can we determine the best model to accurately predict the closing price of bitcoin? We will use various technical indicators used in financial trading as our predictor variables and the closing price of bitcoin as our response variable. Our team would also like to determine which predictors are statistically significant in predicting the closing price of bitcoin. We split the data into test and train datasets in order to compare the test MSE across our models. The model with the lowest test MSE will be considered the best model to predict the closing price of bitcoin. In order for our model to be useful, we decided to shift the technical indicator data by one day as this allows us to determine if we can use the previous day's technical indicator data to predict the current day's closing price.

## Linear regression

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Analyzing-key-financial-indicators/main/lm_model.PNG">

Given the p-values of the closing price of BTC, we may reject the null hypothesis for the following indicators.
- volume (previous days trading volume)
- macd_26 (moving average convergence divergence, 26 day trend)
- macd_9 (moving average convergence divergence, 9 day trend)
- span_a (measures momentum)
- Kijun (midpoint price the last 26 periods)
- Tenkan (japanese indicator)
- RSI (relative strength index)

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Analyzing-key-financial-indicators/main/Corr_Analysis_lm.PNG">

We are able to see the close price of BTC has a strong linear correlation with Kijun, Tenkan, and SMA indicators. Also with span_a and span_b but less so with macd_26 and macd_9. We can also see signs of high colinearity between different predictor variables.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Analyzing-key-financial-indicators/main/Kijun_indicator_lm.PNG">

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Analyzing-key-financial-indicators/main/Tenkan_indicator_lm.PNG">

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Analyzing-key-financial-indicators/main/SMA_indicator_lm.PNG">

Even though we can reject the null hypothesis for all the indicators above, the traditional linear regression model is not the best fit for most. It may be because the BTC prices are volatile, and we need a model that provides more flexibility.

## Lasso and Ridge regression

We are going to build a lasso and ridge regression model using all predictor variables in order to predict the close price. We will also determine which predictors went to zero using the lasso model and we will compare the test MSE for each model to determine which model performs the best. Both models will be tested using cross-validation with ten folds.

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Analyzing-key-financial-indicators/main/Lasso_Model.PNG">

<img src="https://raw.githubusercontent.com/LKPelayoUribe/Analyzing-key-financial-indicators/main/Ridge_Model.PNG">

The lasso model determined the predictor variables macd_9, span_a, span_b, and the SMA all had a coefficient of zero which indicates these variables are not important when trying to predict the close price of bitcoin. The test MSE for the lasso model is 2.7553602 × 10<sup>6</sup> which is quite a bit better than the test MSE of the ridge model of 3.4175114 × 10<sup>6</sup>. Overall a lasso model is preferred to a ridge model when predicting the close price of bitcoin.

## GAM

## Conclusion
Our team has evaluated four different models that can be used to predict the closing price of bitcoin. After looking at the test mse scores of the four models we have concluded that the GAM model which used natural splines at the optimal degree which was found by using cross validation techniques, was able to report a MSE of 2.4589802 × 10<sup>6</sup> a MAE of 969.4837132 and an r-squared of 0.9916912. We also were able to discover the coefficients for most important predictor variables that can be used to successfully predict the bitcoin close price which are the following:
– macd_26 with a natural spline of 13 degrees
– macd_9 with a natural spline of 12 degrees
– kijun with a natural spline of 15 degrees
– tenkan with a natural spline of 10 degrees
– rsi with a natural spline of 2 degrees


