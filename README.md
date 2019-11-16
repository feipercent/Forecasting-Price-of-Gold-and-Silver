# GOLD AND SILVER PRICE ANALYSIS AND PREDICTION

### DATASET:

Historic daily prices of gold and silver from below two URLS (January 01, 2019 till November 12, 2019). 

• Gold data: https://www.investing.com/commodities/gold-historical-data

• Silver data: https://www.investing.com/commodities/silver-historical-data

Each dataset contains seven columns: Date, Price, Open, High, Low, Vol., and Change %. Both gold and silver are only transacted. Gold is transacted every 5 days from Monday to Friday, silver is transacted every 6 days from Monday to Saturday.

### OBJECTIVE:

The goal of this project is to analyze the historical prices of gold and silver to predict the prices of gold and silver in next four days, November 13~16, 2019, and use at least two model to predict the performance of models.

### PREPROCESSING:

I checked the data type of each column to make sure the date has date type and price columns have float types. Date is formatted to a common format which would be understood by matplotlib for plotting it appropriately. I also checked whether there is any missing value for date and price columns. 

### STATISTIC PROPERTIES DESCRIPTIONS:

I used combinations of plots and tables in this part. 
  - showed statistic summary of each variable, for example, count, mean, std, min, and max
  - histogram distribution of each column 
  - correlation heatmap and others

### Data Stationarity Test 

● Check Stationarity

To check the stationarity of the data, data along with the dates was ploted. Just by looking at the plot we can conclude that the data is non-stationary, since the mean values is not constant along time.

To identify stationarity quantitatively, dickey-fuller test was conducted to confirm the stationarity. Basically, I interpret this result using the p-values, that is a p-value below a fixed threshold (e.g. 5%) indicates that we reject the null hypothesis(the time series is not stationary). Otherwise a p-value above that threshold indicates that we accept the null hypothesis.

● Make Data Stationary

By conducting check stationary, Observiously, the prices of gold and silver are not staionary. To make the data stationary, three different methods was used, 1) Exponential Average, 2) Differencing, 3) Decomposing.

### MODEL FORECASTING:

● Linear Regression

I  first tried a simple regression model. It is a multiple regression model with input parameters as the moving average of the past 2 days and the past 5 days. The resulted R square is 75% for gold prediction with a RSME of 8.78, and a mean absolute percentage error (MAPE) of 0.44% for the testing data. For silver, the R square is 78% with a MAPE of 0.6%. 

However, the R square is quite sensitive to the chosen window size of moving average. Other methods, such as grid search for optimal window size, can be potentially used. But in this analysis, I used linear regression just for the purpose of exploring and I focused more on later SARIMA model, which is commonly used method for times series data model for prediction. 

● SARIMA model

The prices of gold and silver are seasonality based on statioanary test. SARIMA Model is better over a simple ARIMA model when there is seasonality in the data. Seasonal Autoregressive Integrated Moving Average, SARIMA is an extension of ARIMA that explicitly supports univariate time series data with a seasonal component. It adds three new hyperparameters to specify the autoregression (AR), differencing (I) and moving average (MA) for the seasonal component of the series, as well as an additional parameter for the period of the seasonality. In the stationarity tests for both gold and silver, seasonality is found.

In the test data, the mean absolute percentage error was used as metric to evalaute the model performance. It showed that 0.96% and 1.85% and mean absolute percentage error were estimated for gold price and silver price. 

● SELECTION of BEST MODEL

Choosing MAPE as evaluation metric for models when comparing liner regression model and SARIMA model. The result shows that the MAPE of linear regression model is less than SARIMA model when predicting the price of silver. However, the MAPE of SARMA model is larger than the linear regression model when predicting the price of gold. In other word. The optimum model for predicting silver silver is linear regression, and the optimum model for predicting gold is SARIMA model.

### OBSERVATIONS and CONCLUSION:

I was trying to find the interesting trends in the price fluctuation. Interestingly for various mongth the prices of gold and silver in 2019. Though there are no obvious trends in the data. The maximum price has always been September-October which falls during or just before the wedding season.

The predicted gold price with almost 0.44% Mean Absolute Percentage Error for linear regression model and 0.95% Mean Absolute Percentage Error with SARIMA model. For Silver, 0.6% and 1.85% Mean Absolute Percentage Error for linear regressio model and SARIMA model.

For future work, we can use and build upon our existing model to build a recommendation system suggesting the users the right time to buy and sell gold for people who take interest in investing in gold. What I found was that the trend of gold and silver are very close. Also, the peak price of gold and silver occured near the September, and the lowest price is near the middle of May. For the further analysis and potential investment, we can collect all the existing historical data and analyze whether we can find any potential investment.

We also can change the metrics of our model performance to select the best model depending on the business target. Or using grid search to find the optimum parameter for each model. 

Although ARIMA/SARIMA is commonly used model for rare metal (gold or silver) price prediciton, other existing research work also has been done to predict gold price using different models, such as Rolling and recursive neural network models by Antonino P. (https://www.sciencedirect.com/science/article/pii/S1042444X08000030) or Artificial Neural Network by Hossein M. (https://www.semanticscholar.org/paper/Modeling-Gold-Price-via-Artificial-Neural-Network-Mombeini-Yazdani-Chamzini/0fc93f118843be44345f3c9116793f3d824d4d85). These two papers can be interesting to take a look. 
