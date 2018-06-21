****BitCoin-Regression using R****
**Introduction:**
	In 2008, an unknown programmer using the pseudo name of Satoshi Nakamoto wrote a document called Bitcoin: 
  A Peer-to-Peer Electronic Cash System. Bitcoin (BTC) is a decentralized digital crypto-currency system, 
  meaning the transfer of funds are operated independently of a central bank through the internet. Most notably, 
  these transactions occur with anonymity. 
  Bitcoin has shown significant market capitalization growth in last few years. It is important to understand what 
  drives the fluctuations of the Bitcoin exchange price and to what extent they are predictable.   The graphical representation
  in [https://github.com/NupurShrivastava27/BitCoin-Regression/issues/1] resemble the blue print of a roller coaster more than a financial asset. 
  
  Data Description: The actual historical data for analysis, obtained from blockchain website (https://blockchain.info/stats), comprised of 13 integer variables and 1715 observations from August 2009 to May 2018. Each of the 13 variables are downloaded at a time in excel sheet The dataset has no missing values.
	The main objective of this project is to fit a linear regression for Bitcoin market price (USD). Since a Bitcoin dataset is a time series dataset and this project is a regression analysis, the date column will not be considered for regression analysis.
	Before diving into the regression models, it can be useful to determine how the independent variables such as (Day, Week, Total Transaction Fees, Number of Transactions, Output Value, Estimated Transaction Value, Miners Revenue, Cost per Transaction, Difficulty, Hash Rate, Trade Volume) are correlated to the dependent variable (Price in USD) and each other. A correlation matrix plot shown in Exhibit 2 provides a quick overview of 12 numeric variables correlation in the Bitcoin data frame. At the intersection of each row and column pair, the diagonal (with color navy blue) is always 1 shows the perfect correlation between a variable and itself. [https://github.com/NupurShrivastava27/BitCoin-Regression/issues/2] also depicts that the variables: miner’s revenue, estimated transaction value, difficulty, cost per transaction, and hash rate are highly correlated i.e. (>=.75) to variable price. 
**Analysis:**	Now it’s time to run the regression models and do the analysis. By running the first additive model having all independent variables, assuming that error terms (or "residuals") have a mean of zero and constant variance, the output shows how close the data are to the fitted regression line. In other words, the coefficient of multiple determination i.e. R squared from first model is equal to .9947, indicating that 99.47% of variability in Bitcoin price ($) is explained by the fitted model. This result was an absolutely over fitting the model and variances explained error (or "residuals") were not constant. Result is explained in Exhibit 3. In other words, the variance of the error terms must be constant, and they must have a mean of zero. If this isn't the case, the model may not be valid. This process is called diagnostic(s) test.
	Since dataset has 11 independent variables against dependent variable (Bitcoin market price), we have two options. First option is to perform Principal Components Regression (PCR), which is a dimensionality reduction technique on a high dimensional dataset and then fit a linear regression model to a smaller set of variables (discussed later in detail*). The other option is to perform an Akaike Information Criterion (AIC) using step function to estimates the quality of each model, relative to each of the other models. In other words, AIC provides a means for initial quality model selection to kick start our core analysis.
	After performing PCR, trial models were not showing the good / ideal model, i.e. R square equal to 99.15% and because the variance was again not constant, the model may not be valid. Next, we tried with transformation which is the good ways to improve the model but all kind of transformations trials failed when the residuals were not constant. In other words, if the residuals increase or decrease with the fitted values in a pattern, the errors may not have constant variance. Thus, the model may not be true. Plots are explained in Exhibit 4. 
	Akaike information criterion (AIC) was tried which provides the quality model by choosing with lowest AIC. According to this step( ) function, suggested variables are Day, Week, Transaction fees,  no. of transactions, Output value, estimated transaction value, Miners revenue, Cost per transaction, Difficulty, Hash rate with lowest AIC value. Thus rerun the model and check for the residuals test using Breusch-Pagan test for non-constant variance and Shapiro Wilk, a test for normality. According to model, residuals indicate heteroscedasticity (non-constant variances) and the data are still deviated from the normal. Thus, again the model is not valid. Plots are explained in Exhibit 5.
	Exhibit 4 and 5 explains that we should not use the regression models that produced such results. So, what to do? There's no single answer, but there are several options are knows for transformations. Data transformation definitely requires a "trial and error" approach. In building the model, we try a transformation and then check to see if the transformation eliminated the problems with the model. If it doesn't help, we try another transformation and so on. 
	In our situation, polynomial transformation and percentage change could take place. Polynomial regression models are useful when there is reason to believe the relationship between two variables is curvilinear. In Exhibit 5, there is a curvilinear relationship between the variables which appears to be quadratic. Hence, it fits a polynomial regression model of order 2. But unfortunately, transformations could not make much impact on the residuals data. Finally arrived no where but back to square one. 
	Since in the early years 2009-2016, there were not a lot of price fluctuations in the Bitcoin market price. Hence, bifurcating this dataset from mid 2016 onwards was a smart move for this regression analysis to reflect the current high-volume trading state of the Bitcoin marketplace. The graphical representation in [https://github.com/NupurShrivastava27/BitCoin-Regression/issues/4] would resemble the Bitcoin Price Fireworks from 2017 - 2018. We have a marathon from correlations to the ideal regression model with an updated dataset, lets have a look!! 
	We rerun all steps one by one with an updated dataset from mid June 2016 till May 2018. First, most of the variables are highly correlated to the Bitcoin market price, explains in[https://github.com/NupurShrivastava27/BitCoin-Regression/issues/4]. Next, kick start with full additive model having  all 11 independent variables plugged in, where R^2 is 99.66% of variability in Bitcoin price($). This is explained by the fitted model, which indicates over fitting as earlier with some insignificant variables. After checking the residuals, no big surprises!! Residuals indicate heteroscedasticity that means variances were still nhttps://github.com/NupurShrivastava27/BitCoin-Regression/issues/4ot constant and the data deviates from normality. (likewise both Breusch-Pagan test and Shapiro Wilk test fails!!)
	Running step ( ) function to get a model with the lowest AIC did not do much impact on residuals. We found, weighted least squares regression might be useful and an efficient method that makes good use of small bitcoin dataset after bifurcation. The main advantage of weighted least squares over other methods is an ability to handle regression situations in which the data points are of varying quality. If the standard deviation of the random errors in the data is not constant across all levels of the explanatory variables, using weighted least squares with weights that are inversely proportional to the variance at each level of the explanatory variables yields the most precise parameter estimates possible. But after applying weighted least square regression too, the residuals don’t seem to be constant.
	Next, we could think of using the logarithmic transformed variables to percentage changes. But why? Before going further, let’s take a ride of what is it? A typical use of a logarithmic transformation variable is to pull outlying data from a positively skewed distribution closer to the bulk of the data in a quest to have the variable be normally distributed. In regression analysis the logs of variables are routinely taken, not necessarily for achieving a normal distribution of the predictors and/or the dependent variable but for interpretability. The standard interpretation of coefficients in a regression analysis is that a one unit change in the independent variable results in the respective regression coefficient change in the expected value of the dependent variable while all the predictors are held constant. Now, interpreting a log transformed variable can be done in a same manner. However such coefficients are routinely interpreted in terms of percent change. Since the dataset was not logarithmic scaled therefore logarithmic transformations are required to move further.  
	Next, both the dependent variable and independent variable(s) are log-transformed. This relationship is commonly referred to as elastic in econometrics. In a regression setting, we’d interpret the elasticity as the percent change in Y (dependent variable), while X (the independent variable) increases by one percent. 
	Since from [https://github.com/NupurShrivastava27/BitCoin-Regression/issues/5], after weighted average, we observed that transaction fee BTC, miner revenue seem having curvilinear relationship which appears to be quadratic. Therefore, polynomial transformation is needed for those independent variables i.e transaction fee BTC, miner revenue, resultant to the good model. Yes!! Finally multiple R squared is equals to 30.61% with all independent variables being significant and residuals 'seems to be constant'. According to Breusch Pegan test, p-value > 0.05, therefore we can assume the data has constant variance and W = .98 which is close to 1 proving the data pass the test of normality according to Shapiro Wilk test, explained in Exhibit 10. Final Model equation and its interpretation  as follows:
Bitcoin market price (%) =  -21.89 - 29.68(transaction fee) - 26.05 (transaction fee ^2) + 0.0000014 ( no of transaction) - 360.6 (hash rate) +65.87 (miner revenue %) - 25.76 (miner revenue (%) ^ 2 + 1.4 ^ -11(difficulty) .  Fewer interpretation for instance,
o	A unit change in transaction fee will result in the change in Bitcoin market price(%) by -29.68 minus twice of  26.05 of transaction fees. It will go up in quadratic, when transaction fee go down, holding other variables constant.
o	A unit change in Miner revenue will result in a change in Bitcoin price(%) by 65.87 minus twice of  27.76 times miner revenue, holding other variables constant.
o	A unit change in 'no of transaction', will result in the increase in Bitcoin market price(%) by 0.0000014, holding other variables constant and so on..
Multiple R squared is equal to .3061, that means 30.61% explains the variability in Bitcoin price(%) is explained by the this model, recalling that our dependent variable (Price) is in % change, therefore R square 30.61% is consider to be a good multiple coefficient determination.   
	Once the final model is arrived, next is to investigate about outliers and influential observations, if any. In regression, we assume that there are no influential observations which can have a significant impact on model otherwise, observation with high leverage will affect the intercept and slope of a model significantly. [https://github.com/NupurShrivastava27/BitCoin-Regression/issues/8] shows that in the Bitcoin model,  observation 1335 is an influential outlier however since it has a low leverage ( less hat value according to the bubble chart), removing probably will not change the model by much  therefore we would like to keep it in the model. 
**Conclusion:**	From our final model, we concluded that the predictors such as Transaction fees, no. of transactions, Cost per transaction, Hash rate, Miners revenue and Difficulty explained the fluctuations in the Bitcoin market price. 
	Future project could be to take it even further to explore time series analysis, after a truly extraordinary run over the last eight years, where will Bitcoin be a decade from now? Final graphical plots and tables are given [https://github.com/NupurShrivastava27/BitCoin-Regression/issues/6] that explains that the model has been following the trend of actual data, except for a few spikes. Next graph is the forecast of 2018 Bitcoin market price ($) with a positive trend in dotted line.

  
