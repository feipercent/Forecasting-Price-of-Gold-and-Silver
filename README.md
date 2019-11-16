# GOLD AND SILVER PRICE ANALYSIS AND PREDICTION

### DATASET:

I have used 2 datasets for this, historic daily prices of gold and silver from below two URLS (January 01, 2019 till November 12, 2019). 

• Gold data: https://www.investing.com/commodities/gold-historical-data

• Silver data: https://www.investing.com/commodities/silver-historical-data

Each dataset contains seven columns: Date, Price, Open, High, Low, Vol., and Change %. Both gold and silver are only transacted. Gold is transacted every 5 days from Monday to Friday, silver is transacted every 6 days from Monday to Saturday.

### OBJECTIVE:

The goal is to predict the prices of gold and silver in next four days, November 13~16, 2019, and use at least two model to predict the performance of models. The above website can be used to check newly updated prices comparing with my predicitons. 

### PREPROCESSING:

I checked the data type of each column to make sure the date has date type and price columns have float types. Date is formatted to a common format which would be understood by matplotlib for plotting it appropriately. I also checked whether there is any missing value for date and price columns. 

### STATISTIC PROPERTIES DESCRIPTIONS:

I used combinations of plots and tables in this part. 
  - showed statistic summary of each variable, for example, count, mean, std, min, and max
  - histogram distribution of each column 
  - correlation heatmap and others

### Data Stationarity Test 

● Check Stationarity

To check the stationarity of the data I first plotted the data along with the dates.
Just by looking at the plot we can conclude that the data is non-stationary, since the mean values is not constant along time.

To identify stationarity quantitatively, I performed the dickey-fuller test to confirm the stationarity. We can see the ADF statistic is higher than any of the critical values, and the p value is much greater than 0.05, so we cannot reject the null hypothesis that the data is non-stationary.

● Make Data Stationary

To make the data stationary, three different methods can be used, 1) Exponential Average, 2) Differencing, 3) Decomposing. 

### MODEL FORECASTING:

● Linear Regression

I  first tried a simple regression model. It is a multiple regression model with
input parameters as the moving average of the past 2 days and the past 5 days. The resulted R square is 70% for gold prediction, which is not bad, while RMSE is 8.02, which is not small difference compared with actual price. The R square is quite sensitive to the chosen window size of moving average. Other methods, such as grid search for optimal window size, can be potentially used. But in this analysis, I used linear regression just for the purpose of exploring. 

● SARIMA model

I model this data using a SARIMA model. A SARIMA model stands for a Seasonal ARIMA model. SARIMA Model is better over a simple ARIMA model when there is seasonal data. I.e. the timeseries data has repeating cycles. I observe that the model fits much better than any of the previous models.

Below are the results and the diagnostics of the model.We see that the R square value is 73% which is acceptable and the RMS Error has
reduced to 1715 from 5000, which is a good sign.

● SELECTION of BEST MODEL
Mean Absolute Percentage Error（MAPE) was considered as the selection of the best model from liner regression model and SARIMA model. The result shows that the MAPE of 

### FINDING TRENDS:

I was trying to find the interesting trends in the price fluctuation. Interestingly for various mongth the prices of gold and silver in2019. Though there are no obvious trends in the data. The maximum price has always been March-April or September-October which falls during or just before the wedding season.


### OBSERVATIONS and CONCLUSION:

Finally, the predicted gold price with almost 0.44% Mean Absolute Percentage Error for linear regression model and 0.95% Mean Absolute Percentage Error with SARIMA model. For Silver, 0.6% and 1.85% Mean Absolute Percentage Error for linear regressio model and SARIMA model.

For future work, we can use and build upon our existing model to build a recommendation system suggesting the users the right time to buy and sell gold for people who take interest in investing in gold. What I found was that the trend of gold and silver are very close. Also, the peak price of gold and silver occured near the September, and the lowest price is near the middle of May. For the further analysis, for the potential investigation, we can collect all the historical data and analyze whether this patten was existing in every years. 

Although ARIMA/SARIMA is commonly used model for rare metal (gold or silver) price prediciton, other existing research work also has been done to predict gold price using different models, such as Rolling and recursive neural network models by Antonino P. (https://www.sciencedirect.com/science/article/pii/S1042444X08000030) or Artificial Neural Network by Hossein M. (https://www.semanticscholar.org/paper/Modeling-Gold-Price-via-Artificial-Neural-Network-Mombeini-Yazdani-Chamzini/0fc93f118843be44345f3c9116793f3d824d4d85). These two papers can be interesting to take a look. 
