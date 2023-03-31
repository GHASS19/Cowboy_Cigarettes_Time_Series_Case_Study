# Cowboy Cigarettes Time Series 

![image](https://user-images.githubusercontent.com/86930309/228976763-220ad79d-9dbd-4d9f-8f58-975f779f0f1e.png)

You're working in the US federal government as a data scientist in the Health and Environment department. You've been tasked with determining whether sales for the oldest and most powerful producers of cigarettes in the country are increasing or declining. Cowboy Cigarettes (TM, est. 1890) is the US's longest-running cigarette manufacturer.

Like many cigarette companies, however, they haven't always been that public about their sales and marketing data. The available post-war historical data runs for only 11 years after they resumed production in 1949; stopping in 1960 before resuming again in 1970. 

Your job is to use the 1949-1960 data to predict whether the manufacturer's cigarette sales actually increased, decreased, or stayed the same. You need to make a
probable reconstruction of the sales record of the manufacturer. Predicting the future from the perspective of the past and to contribute to a full report on US public
health in relation to major cigarette companies. The results of your analysis will be used as part of a major report relating public health and local economics, and will be combined with other studies executed by your colleagues to provide important government advice.

## 1. Sourcing and loading

- Load relevant libraries

- Load the [data](https://github.com/GHASS19/Cowboy_Cigarettes_Time_Series_Case_Study.ipynb/blob/main/Data/CowboyCigsData%20(Time%20Series%20Analysis).csv)

- Explore the data

A. 144 Rows and 3 columns.

B. No null values.

## 2. Cleaning, transforming and visualizing

- Dropping the unwanted unnamed column

- Nomenclature. Change column year to month

- Type conversions. Change the month column object to a datetime

- Making a predictor variable y. Our dependant variable will be cigarette sales column since we want to predict the manufacturer's sales

- Getting summary statistics for y

- Plotting y

![image](https://user-images.githubusercontent.com/86930309/229005100-4dd019cf-694d-4aa5-8b1c-51debb8c1d03.png)

The sales have a positive trend

## 3. Modelling

- Decomposition

A. The Cowboy Cigarettes data is actually multiplicative.

B. As time progresses the general trend seems to be increasing at a rate that's also increasing. We also see that the seasonal fluctuations, (the peaks and troughs) get bigger and bigger as time progresses.

- Trend, Seasonality and Noise graph of the cigarette sales:

![image](https://user-images.githubusercontent.com/86930309/229006792-7083d6da-7b5d-45ac-aca1-72c5d4c11bb2.png)

The seasonal trends are increasing over time.

- Testing for stationarity with KPSS

Since our p-value is less than 0.05, we should reject the Null hypothesis and deduce the non-stationarity of our data. Our data need to be stationary! So we need to
do some transforming.

- Making the data stationary

A. We have a constant variance, but we also need a constant mean. We can do this by differencing our data.

B. This is a graph of the sales using .diff() to make the data stationary:

![image](https://user-images.githubusercontent.com/86930309/229015554-bc48e2f3-d8c5-480c-8cbe-8a95987b0625.png)

- The ARIMA Model

The ARIMA models are based around the idea that it's possible to predict the next value in a time series by using information about the most recent data points. The model also accounts for completely random data points that cannot be predicted.

- Make a function to find the MSE of a single ARIMA model

- Make a function to evaluate the different ARIMA models with different p, d, and q values 

The best p,d, q parameters for our ARIMA model are 2, 1, 1 respectively.

- Visualize the results:

![image](https://user-images.githubusercontent.com/86930309/229018731-23605d59-e16d-4312-8419-73fdc1da02bb.png)

Our Arima model fits the data pretty well.

- Application: Forecasting

This is a graph of of the ARIMA model predicting cigarette sales starting in December of 1960 with the original y variable:

![image](https://user-images.githubusercontent.com/86930309/229020741-b66cf696-7ccf-4ec3-81ce-452f3277c2ba.png)

## 4. Evaluating and concluding

- What is our conclusion?

Our model captures the centre of a line that's increasing at a remarkable rate. Cowboy Cigarettes sell more cigarettes in the summer. Perhaps due to the good weather, disposable income and time off that people enjoy. The least amount of sales are in the winter when people might be spending less and enjoying less free time outdoors.

Remarkably our ARIMA model made predictions using just one variable. We can only speculate on the causes of the behaviour predicted by our model. We should also take heed that spikes in data, due to sudden unusual circumstances like wars, are not handled well by ARIMA. The outbreak of the Vietnam War in the 1960s would likely cause our model some distress.

We could suggest to our employers that they execute a regression analysis in addition to this time series.
