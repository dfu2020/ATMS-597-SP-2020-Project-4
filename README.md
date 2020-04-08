# ATMS-597-SP-2020-Project-4
Group members: Dongwei Fu, Joyce Yang, Jun Zhang

This repository contains the csv files and code necessary to train and test two types of weather models. The project emulates a weather forecast challenge, where participants are given weather model data and observational data for a given time period, and asked to develop a weather model to predict forecast variables. 

    Model types: 
        Multiple linear regression 
        Random Forest 
    Forecast variables: 
        Maximum temperature (C)
        Minimum Temperature (C)
        Maximum Wind Speed (m/s)
        Daily Accumulated Precipitation (mm)
    
This code includes the following parts:

    KCMI Data Processing:
        KCMI Daily (target forecast variables are contained in this file)
        KCMI Hourly (feature variables) 
            In real-world weather forecasting/challenges, hourly observational data for the target day would not be available yet, so this data was shifted forward one day to better represent real-world situations. 

    GFS Data Processing:
        GFS Surface Data (feature variables)
        GFS Profile Data (feature variables)
        GFS Daily Data (feature variables)
        
All the variables were combined into one master table and split into training (2010-2018) and test data (2019). Next, they were used to create the two types of models, using sklearn modules. Model performance was evaluated using metrics such as mean absolute error, median absolute error, explained variance (coefficient of determination) and root mean square error. 

    Multiple Linear Regression: 
    Feature variables were ranked by their correlation with the target variable, and were all used as predictors for the target variable. Observed and predicted target variables were then plotted for the 2019 test data. For TMIN and TMAX predictions, the more number of predictors lead to smaller rmse, while this is not true for WMAX and RTOT predictions. 

    Random Forest: 
    Similar to the multiple linear regression, feature variables were first ranked by their correlation with the target variable. The most highly correlated variables were selected to be feature variables. Next, each feature variable was individually taken out before running the model again. This revealed which variables were redundant, or reduced the model performance. This process was used to narrow down to the final set of predictor features. Finally, different           combinations of hyperparameters (number of estimators and maximum number of features) were tested to find the combination leading to optimal performance. 

Future Improvements: 
The accuracy of the model could be improved by backfilling empty data, and performing some tests to quantify overfitting of the data. Additionally, a better understanding of the drivers of each of the target variables could guide future feature selection. 

Additional Observations: 
Compared to the other variables, precipitation was less correlated with the feature variables. This could be due to greater inherent variability/randomness in precipitation, or just that the input data variables did not cover weather variables most correlated with precipitation. Additionally, we noticed that our precipitation model was able to relatively accurately predict most precipitation amounts, but not extreme precipitation events. 

We also noticed that the different target variables responded differently to hyperparameter tuning. For example, precipitation was much more sensitive to the maximum number of features, and its model performed better with the lowest number of max features. The other variables performed the best with max features of 3-5, with performance declining outside of that range. They were also less sensitive. 

Overall, this project provides a relatively accurate process for creating models to predict weather variables using a combination of observational/model data. 
