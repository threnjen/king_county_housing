
# King County Housing Price Predictor

By: Jen Wadkins

## Introduction

> This is an in-depth notebook which explores the King County Housing Dataset through several different models. The notebook includes a thorough EDA and cleaning section, numerous visualizations, exploration of different models, feature selection and engineering methods, and a model stack to create the final model.

> You can read my tutorial about simple model stacking on Medium: https://towardsdatascience.com/simple-model-stacking-explained-and-automated-1b54e4357916

## Skills Presented

* Data Cleaning
* Exploratory Data Analyis
* Data Visualization
* Feature Selection and Engineering
* Model Selection and Tuning
* Model Stacking

## Questions

* What are the primary factors influencing housing prices in the King County metro area?
* Can we effectively use a regression model based system for realtors to determine a proper list price?

## Methodology

We use the OSEMN for Data Science to organize the project.
* Obtain Data: Source data from King County
* Scrubbing/Cleaning Data: Clean and prepare data for model processing
* Exploring/Visualizing the Data: Perform EDA on data
* Model: Iteratively explore different models
* Analysis: Analyze and explain results


# Table of Contents

#### [king_county_streamlined.ipynb.ipynb](https://github.com/threnjen/king_county_housing/blob/main/king_county_streamlined.ipynb)

* **Project Overview**
    * Table of Contents
    * Objective
    * Package Imports
    * Notebook Functions

* **Obtaining our Data**

* **Scrubbing/Cleaning Data**
    * Checking Time Series
    * Duplicate Data
    * Outlier Detection
    * Binary Data

* **Exploring/Visualizing Data**
    * Study Target Variable
    * Create Holdout Set
    * Feature Engineering
    * Correlations and Multicollinearity
    * Polynomial Relationships
    * Visualize Categoricals
    * Visualize Continuous
    * Feature Interactions

* **Cleaning Final Data**
    * Standardize and Transform
    * Add Polynomial Features
    * Process Test Set
    * Create Train/Test Final Set

* **Modeling**
    * Spot Check Models
        * Feature Selectors
        * Spot Check Evaluation
    * Final Model Setup
        * Prepare Testing Assets
        * Get OOF Predictions
        * Run Stack Selector
        * Prepare Final Assets
    * Final Model Evaluation

* **Analysis**

* **APPENDIX**

## Analysis

> Our final model utilizes a combination of continuous variables and one-hot-encoded categoricals to produce a stacked model with R^2 of 89.78%, a mean absolute error of 47.2k, and a root mean squared error of 74k. I tried several different zip code transformations including polynomial features, mean target encoding, lower-granularity binning, and median rank as a continuous, and ALL of these efforts resulted in a lower R^2 and higher mean absolute error, leading to a final decision to one-hot encode all 70 zip codes individually. Similar efforts on other categoricals such as age and month sold also did not improve the model over one-hot encoding. This resulted in the greatest accuracy despite a model that is more "messy" with a large number of features.

### What are the primary factors influencing housing prices in the King County metro area?
> As square footage increases so does quality of materials. Most importantly you can see the upward price trend with both increased square footage and materials grade. I was intrigued that our lower bound of data points is very linear, but as our square footage increases, the upper bound gradually breaks away with higher variance. 
>![Total Price per Total Square Footage, by Grade](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/pr_grade.png)

>I ranked the 70 zip codes in King County by median home value, and used those ranks to color our data points.  Our low median zip codes have a low price per square footage, and price per square foot increases with zip code median, which makes sense, but also shows the importance of zip code to pricing. I found it interesting that while most zip codes exhibit a clear trend of price per square foot decreasing with increased total square footage, which is entirely normal, certain very high value zip codes seem to retain their high price per square foot regardless of total square footage. Certain zip codes seem immune to the usual price per square foot decay. 
>![Price per Square Foot per Total Square Footage, by Zip Code Median](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/pr_sf_zip.png)

> As they say, location is everything, and it is the primary influencing factor for a home price in the King County metro area. Our darkest areas, and therefore highest value sales, are clustered in and around Seattle to the west of Lake Washington and into the eastern lake cities of Bellevue and Redmond which are the technical employer hubs of the region. As we move away from Seattle and the tech hubs into the suburbs, our prices clearly go down.
>![Housing Sales in King County by Location](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/map_housing_dots_cropped.png)

> These three features alone explain 85% of the price variance.

### Can we effectively use a regression model based system for realtors to determine a proper list price?
> Our model, while explaining over 89.78% of the price variance with our features, was nonetheless far from accurate in absolute terms. A mean average error of 47.2k in either direction is a huge variance to a home price - one that is so large that it renders the prediction much less meaningful and useful. Other models need to be explored, better data needs to be sourced, or easy-to-use features that an average realtor is capable of evaluating/acquiring should be added to the model to improve its predictive quality. The model is providing at best a baseline starting point.


## Presentation
[Video - Data Science Module 2 Project](https://youtu.be/vsyFdHGtmqM)

[PDF of Presentation](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/mod_2_project.pdf)
