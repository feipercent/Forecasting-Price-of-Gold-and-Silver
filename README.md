# GOLD AND SILVER PRICES ANALYSIS AND PREDICTION

### DATASET:

Historic daily prices of gold and silver are obtained from below two URLS (January 01, 2019 till November 12, 2019). 

• Gold data: https://www.investing.com/commodities/gold-historical-data

• Silver data: https://www.investing.com/commodities/silver-historical-data

Each dataset contains seven columns: Date, Price, Open, High, Low, Vol., and Change %. Gold is transacted every 5 days from Monday to Friday, and silver is transacted every 6 days from Monday to Saturday.

### OBJECTIVE:

The goal of this project is to analyze the historical prices of gold and silver and predict the prices of gold and silver in next four days, November 13~16, 2019. At least two different models need to be implemented and the performances need to be compared.

### PREPROCESSING:

I checked the data type of each column to make sure the date has date type and price columns have float types. Date was formatted to a common format which would be understood by matplotlib for plotting it appropriately. I also checked whether there is any missing value for date and price columns. Vol. and Change % are not important columns here.  

### STATISTIC PROPERTIES DESCRIPTIONS:

I used combinations of plots and tables in this part to describe the statistic properties of the data:  
  - statistic summary of each variable, for example, count, mean, std, min, and max
  - histogram distribution of each feature 
  - correlation heatmap  

### Data Stationarity Test 

● Check Stationarity

To check the stationarity of the data, data along with the dates was ploted. Just by looking at the plot we can conclude that the data is non-stationary, since the mean values is not constant along time.

To identify stationarity quantitatively, dickey-fuller test was conducted to confirm the stationarity. Basically, I interpret this result using the p-values, that is a p-value below a fixed threshold (e.g. 5%) indicates that we reject the null hypothesis(the time series is not stationary). Otherwise a p-value above that threshold indicates that we accept the null hypothesis.

● Stationary Data Transformation

After confirming the data is none-stationary, I implemented three different methods in the code: 
  - Exponential Average 
  - Differencing 
  - Decomposing

### MODEL FORECASTING:

● Linear Regression

I  first tried a simple regression model. It is a multiple regression model with input parameters as the moving average of the past 2 days and the past 5 days. The resulted R square is 75% for gold prediction with a RSME of 8.78, and a mean absolute percentage error (MAPE) of 0.44% for the testing data. For silver, the R square is 78% with a MAPE of 0.6%. 

However, the R square is quite sensitive to the chosen window size of moving average. Other methods, such as grid search for optimal window size, can be potentially used. But in this analysis, I used linear regression just for the purpose of preliminary exploring and I focused more on later SARIMA model, which is commonly used method for times series data model for prediction. 

● Seasonal Autoregressive Integrated Moving Average (SARIMA) model

Both prices of gold and silver show seasonality based on statioanary test. SARIMA Model is better over a simple ARIMA model when there is seasonality in the data. SARIMA is an extension of ARIMA that explicitly supports univariate time series data with a seasonal component. It adds three new hyperparameters to specify the autoregression (AR), differencing (I) and moving average (MA) for the seasonal component of the series, as well as an additional parameter for the period of the seasonality. 

In the test data, the mean absolute percentage error was used as metric to evalaute the model performance. For gold and silver, the Mean Absolute Percentage Error (MAPE) is 0.96% and 1.85%, respectively for gold price and silver price predictions. 

● SELECTION of BEST MODEL

I used MAPE as evaluation metric for models when comparing liner regression model and SARIMA model. The result shows that the MAPE of linear regression model is less than SARIMA model when predicting the price of silver. However, the MAPE of SARMA model is larger than the linear regression model when predicting the price of gold. In other word. The optimum model for silver price prediction is linear regression, and the optimum model for gold price prediction is SARIMA model. Further efforts still are needed to improve on linear regression model. 

### OBSERVATIONS and CONCLUSIONS:

**1. SARIMA model gives Mean Absolute Percentage Error (MAPE) of 0.96% and 1.85%, respectively for gold price and silver price predictions.** 

 **2. By looking at the overal trend, we can see that gold price starts from ~$1300, kept relatively steady around $1320, decreased below $1300 between May and June, then begins to increases from June onward, hit to a peak about $1550, and then begins to decrease again, but still remains at the level of ~$1450, which is still at higher end. This whole changing trend is quite interesting; this trend also applies to silver, meaning gold and silver prices are probably quite highly correlated, which is not surprising. I can think of several factors that might influenced these change points. 
   - This trend actually alligns quite well with the trend I see in some stock prices (oil or big copporations), which is reasonaly.** 
   - **One international event that happend in Sep 2019 in Europe might caused the rapid increase in Sep ([News link](https://www.ecb.europa.eu/press/pr/date/2019/html/ecb.pr190726_1~3eaf64db9d.en.html)): The European Central Bank (ECB) and 21 other central banks that are signatories of the Central Bank Gold Agreement (CBGA) have decided not to renew the Agreement upon its expiry in September 2019. This means less stringent terms of gold purchase for those banks, which is high likely caused increased demand of gold on the market, and thus caused the price increasing rapidly.**
   - **Another factor that influences Sep is that Autumn is traditionally popular season for weddings in India, where gold demand is high, since people in India like gold for weddings. Also in the West, Sep and October is usually when people begin to prepare buying gifts for Thanksgiving or Christmas, which might also cause a higher demand for gold.** 
   - **Trade war is ongoing in 2019, which might also fluactures gold/silver price** 

**3. In this analysis, I tried linear regression and SARIMA. Although ARIMA/SARIMA is commonly used model for rare metal (gold or silver) price prediciton, I have also read some research papers using [ANN](https://www.semanticscholar.org/paper/Modeling-Gold-Price-via-Artificial-Neural-Network-Mombeini-Yazdani-Chamzini/0fc93f118843be44345f3c9116793f3d824d4d85) and [Rolling and Recursive Neural Network models by Antonino P](https://www.semanticscholar.org/paper/Modeling-Gold-Price-via-Artificial-Neural-Network-Mombeini-Yazdani-Chamzini/0fc93f118843be44345f3c9116793f3d824d4d85). Both of these papers have shown some interesting results. The disadvantage would be difficult to interpret.** 

**4. From decomposing analysis, I have detected some seasonality from both gold and silver price. But I am not sure yet about how to interpret this seasonality, since gold or silver's mined supply is essentailly constant year-round. This can be some interesting question to look into. This [link](http://www.zealllc.com/2014/goldstse.htm) provides some interesting explainings.** 

**5. In this analysis, only price information is used. For further efforts, additional related features potentially can be introduced as well, such as interest rate, bond price, or oil price, to do multivariate time series model.**  

**6. For future work, we can use and build upon our existing model to build a recommendation system suggesting the users/investers the right time to buy and sell gold for people who take interest in investing in gold.**
