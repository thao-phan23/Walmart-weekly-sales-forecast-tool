# Flatiron_Project_Phase_4
## Walmart weekly sales forecast tool with time series model
![Walmart-Sign](https://github.com/thao2023/Flatiron_Project_Phase_4/assets/131706716/e5db594a-e48e-4609-8740-dc3b9e267de0)
## 1. Business problems:
With 45 stores and 99 departments, Walmart's forecasting process extends to the individual departments of each store. However, in the dynamic retail industry, these departments are constantly encountering changes that require them to assess the impact on their forecasts and take swift actions. While waiting for the formal forecast from the planning team is the standard procedure, it can be time-consuming and the planning team may not always have the capacity to promptly address all changes. All relevant departments want to have a sales forecasting tool that they can access at any time, and generate quick forecasts within a certain level of accuracy.

#### Key business questions:
How to generate sales forecasts quickly and at any time with a certain level of accuracy?

## 2. Data understanding:
Weekly sales data spans from Feb 2010 to Oct 2012 will be used to analyze and do modeling. 

Weekly sales mainly depend on holidays and markdowns.

![image](https://github.com/thao2023/Flatiron_Project_Phase_4/assets/131706716/bd430f06-6af2-4647-8380-5de9c8822da9)

Overall, the sales during holiday weeks were higher compared to the sales during normal weeks. Even though there was not a significant increase but we can explain in the next graph.

![image](https://github.com/thao2023/Flatiron_Project_Phase_4/assets/131706716/0fc95f44-4913-4ff8-98c5-a233335db65a)

The red dotted lines in the chart represent holiday weeks. However, since the complete yearly holiday data is not available and it is unlikely that big holidays would occur within a single week, we can observe certain patterns. For smaller or medium holidays, sales tend to increase during the holiday week itself. On the other hand, for major holidays, sales show an increase in the week before and a few weeks before the holiday. Despite the limitations in holiday data, there appears to be a relative correlation between holidays and sales, indicating that sales tend to increase around holiday periods.

Besides, other factors might impact on week sales, which are temperature, fuel price, CPI, and unemployment rate but there are no clear correlations between sales and them.

## 3. Modeling:
In this analysis, our focus will be on analyzing and modeling a specific department (92) within a specific store (20). We will evaluate the performance of the models using two key metrics: RMSE (root mean squared error) and MAE (mean absolute error).

We will apply classical time series models (ARIMA and SARIMAX) as well as machine learning models (XGBoost Regressor and Random Forest Regressor) and then evaluate which model is the most suitable one.

## 4. Model evaluation:

Below is the summary table for the different models' results:

![image](https://github.com/thao2023/Flatiron_Project_Phase_4/assets/131706716/2b33a914-7343-4c0c-85f4-a70d1d343a66)

With ARIMA and SARIMAX models, removing the trend and seasonality is crucial to ensure accurate forecasts. However, considering the large number of combinations resulting from Walmart's 45 stores and 99 departments, applying these models at scale becomes inefficient. These models are time-consuming, complex, and require case-by-case analysis, making them impractical for forecasting in this context.

By utilizing machine learning models such as Random Forest Regressor and XGBoost Regressor, we can bypass the need for manually decomposing trends and seasonality. Instead, we can directly input relevant predictors or those we suspect to be influential into these models. They will then identify and highlight the factors that have the most significant impact on the predicted forecast. This approach allows us to easily scale up the forecast to include all stores and departments, resulting in a more efficient, convenient, and time-saving process.

Although the ARIMA model with the first-time series differencing yielded the lowest RMSE and MAE, it is not suitable for scaling up to multiple stores and departments. Therefore, our best model choice is the Random Forest Regressor with tuning. The RMSE decreased from 23k (baseline model) to 18k, and the MAE decreased from 18k (baseline model) to 13k. Even though these errors are still relatively high, it is the best performance we can achieve with the current data. To further improve the model's predictions, we need to feed more data into the model for a better learning process.

One important point to highlight is that both RMSE and MAE are used to evaluate the model's performance, but I strongly prefer MAE in this analysis as MAE reflects the absolute error between the actual and predicted sales, and it is less sensitive to large errors compared to RMSE.

## 5. Recommendation:

- Holiday: As per the current status, the yearly holiday calendar was not fully updated in the data and there was a simple classification of Yes/No for holidays. I would suggest incorporating a comprehensive collection of annual holidays and categorizing them into broader classifications, such as big, medium, and small, based on their duration.

- Sale events: Sale events were not present in the available data, but I would suggest incorporating them by including yearly sale events categorized into different levels such as mega, big, medium, small, flash, etc. Adding sale events as an additional predictor in the model can enhance the accuracy of the predictions.

- Error analysis: since the forecast model is not perfect, we should review the forecast every month/quarter to find out which factors impact the errors and add that factors into the models as predictors.

## 6. Limitation:

The available data is limited, covering less than 3 years, with only the year 2012 having complete data for the entire year. Additionally, there was missing markdown information until Nov-2011, and the holiday data is not fully provided.

