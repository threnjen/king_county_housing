
# King County Housing Price Predictor

By: Jen Wadkins

## Introduction

>This is an in-depth notebook which explores the King County Housing Dataset through several different models. The notebook includes a thorough EDA and cleaning section, study of different models using different categorical methods (one-hot encoding vs target encoding) with extensive parameter tuning, an exploration of different feature selection methods, an evaluation of the final model, and visualizations.

## Questions

* What are the primary factors influencing housing prices in the King County metro area?
* Can we effectively use a regression model based system for realtors to determine a proper list price?

## Methodology
* Source data from King County
* Clean and prepare data for model processing
* Perform EDA on data
* Process data with a variety of models to find the most effective model, also exploring different categorical methods and feature selection


# Table of Contents

#### [king_count_housing.ipynb](https://github.com/threnjen/king_county_housing/blob/main/king_county_housing.ipynb)

* **Business Objective**


* **Notebook Preparation**
    * Importing our Modules


* **Preprocessing**
    * EDA and Cleaning
        * Scaling Time Series
        * Duplicates
        * Outlier Detection
        * Missing Data
        * Binary Data
        * Visualize Cleaned Data
        * Studying our Target Variable
    * Create Holdout Set
    * Feature Engineering
    * Correlations and Multicollinearity
    * EDA & Process Train Set
        * Categoricals
        * Continuous
            * Find Interactions
            * Transform and Standardize Continuous Data
            * Add Polynomial Features
    * Process Test Set
        * Categoricals
        * Continuous
    * Create Train/Test Split


* **Model Explorations**
    * Picking our Base Features
    * Linear Regressions
        * Basic LR with Top Features One-Hot Encoded
        * Basic LR with Top Features Target Encoded
        * LR with ALL model features
        * Linear Regression with various Feature Selection Methods
            * Forward-Backward Selector
            * Permutation Importance
            * RFECV
    * K-Nearest Neighbors
    * Support Vector Regression
    * XGBoost Model
        * One Hot Encoded
        * Target Encoded


* **Model Selection and Analysis**

* **Additional Visualizations**

* **APPENDIX**

## Analysis

> Our final model utilizes a combination of continuous variables and one-hot-encoded categoricals to produce a support vector machine regression with R^2 of 89.3%, a mean absolute error of 52k, and a root mean squared error of 78k. I tried several different zip code transformations including polynomial features, mean target encoding, lower-granularity binning, and median rank as a continuous, and ALL of these efforts resulted in a lower R^2 and higher mean absolute error, leading to a final decision to one-hot encode all 70 zip codes individually. Similar efforts on other categoricals such as age and month sold also did not improve the model over one-hot encoding. This resulted in the greatest accuracy despite a model that is more "messy" with a large number of features.

### What are the primary factors influencing housing prices in the King County metro area?
> As square footage increases so does quality of materials. Most importantly you can see the upward price trend with both increased square footage and materials grade. I was intrigued that our lower bound of data points is very linear, but as our square footage increases, the upper bound gradually breaks away with higher variance. 
>![Total Price per Total Square Footage, by Grade](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/pr_grade.png)

>I ranked the 70 zip codes in King County by median home value, and used those ranks to color our data points.  Our low median zip codes have a low price per square footage, and price per square foot increases with zip code median, which makes sense, but also shows the importance of zip code to pricing. I found it interesting that while most zip codes exhibit a clear trend of price per square foot decreasing with increased total square footage, which is entirely normal, certain very high value zip codes seem to retain their high price per square foot regardless of total square footage. Certain zip codes seem immune to the usual price per square foot decay. 
>![Price per Square Foot per Total Square Footage, by Zip Code Median](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/pr_sf_zip.png)

> As they say, location is everything, and it is the primary influencing factor for a home price in the King County metro area. Our darkest areas, and therefore highest value sales, are clustered in and around Seattle to the west of Lake Washington and into the eastern lake cities of Bellevue and Redmond which are the technical employer hubs of the region. As we move away from Seattle and the tech hubs into the suburbs, our prices clearly go down.
>![Housing Sales in King County by Location](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/map_housing_dots_cropped.png)

> These three features alone explain 85% of the price variance.

### Can we effectively use a regression model based system for realtors to determine a proper list price?
> Our model, while explaining over 89.3% of the price variance with our features, was nonetheless far from accurate in absolute terms. A mean average error of 52k in either direction is a huge variance to a home price - one that is so large that it renders the prediction much less meaningful and useful. Other models need to be explored, better data needs to be sourced, or easy-to-use features that an average realtor is capable of evaluating/acquiring should be added to the model to improve its predictive quality. The model is providing at best a baseline starting point.


## Presentation
[Video - Data Science Module 2 Project](https://youtu.be/vsyFdHGtmqM)

[PDF of Presentation](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/mod_2_project.pdf)
