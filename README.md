
# Module 2 Final Project - Housing Price Predictor

For: Premiere Properties, LLC

By: Jenny Wadkins

## Introduction

>Premiere Properties, LLC has asked me to develop a housing predictor tool. The market recently has exploded with volatility and unpredictability, with houses going 30k, 50k or even 100k over asking. Realtors need a better tool to price and predict homes. The tool should be easy to both use and understand, and use features that a realtor can input.

## Questions

* What are the primary factors influencing housing prices in the King County metro area?
* Can we effectively use a regression model based system for realtors to determine a proper list price?
* Is a model-based system more accurate for determining list price than the traditional comps-based system?
* What easy-to-use features can we add to our model to increase its accuracy?

## Methodology
* Source data from King County
* Clean and prepare data for model processing
* Process data with a variety of models to find the most effective model
* Provide a "realtor simulator" model to compare with machine learning model
* Demonstrate ability of model to make new predictions

## Table of Contents

#### [student.ipynb](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/student.ipynb

> Notebook Preparation
* Recommended Extensions
* Importing our Modules

> Preprocessing
* Initial EDA
* Process Data for Modeling

> Model Explorations
* Basic Linear Regression Model
* Linear Regression with various Feature Selection Methods
* LAD Linear Regression
* Regularization Models - Lasso, Ridge, Elastic Net
* K-Nearest Neighbors
* Support Vector Regression
* Gradient Boosting Regressor
* Random Forest Regressor
* RFECV with Mean Encoded Categoricals

> Realtor Simulator - the Classic Comps Model
* Write realtor simulator functions and apply to test data

> Regression Results and Model Selection
* Evaluate results of all attempted models and choose best model

> Final Model
* Process and train final model on data
* Saving model assets for later use
* Evaluating final model stats

> Making Predictions with New Data
* Making new predictions on one entry and imported csv

> Visualizations
* Feature visualizations
* Geopandas geographical visualizations
* Comps model geographical visualization

> Analysis
* Statistical analysis and explanations

> Conclusions and Recommendations
* Answers to business questions

> Future Work

> Explanation of Attempts - Feature Engineering/Selection


## Analysis

> ![Statistical Model Summary](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/output.png)

> Our final model utilizes a combination of continuous variables and one-hot-encoded categoricals to produce a linear regression with R^2 of 88.2% and a mean absolute error of 56k. I tried several different transformations including polynomial features, mean target encoding, lower-granularity binning, and median rank as a continuous, and ALL of these efforts resulted in a lower R^2 and higher mean absolute error, leading to a final decision to one-hot encode all 70 zip codes individually. Similar efforts on other categoricals such as age and month sold also did not improve the model over one-hot encoding. This resulted in the greatest accuracy despite a model that is more "messy" with a large number of features.

> Features were selected using the sklean "Recursive Feature Elimination with Cross Validation" function, or RFECV. RFECV uses cross-validation and begins the model with all features, then eliminates the weakest feature and scores the model again, using cv with each iteration. At the end it returns the model with the feature set that produced the highest score on the cv. In the case of price predictions I used mean absolute error as my preferred scoring metric. Then, starting with the features recommended by RFECV, I ran the model again through a forward-backward feature selector, which starts with zero features and iteratively adds and subtracts features until all features have a p-value under the threshold (in this case .05). 

> Almost all included features had p-values so low that the probability that these features are influencing the price by random chance is near zero. Our highest included p-value, zipcode 98003, has only a .3% chance of having influenced prices by random chance.

> 88.2% of our variation in price can be explained by our model variables. Our equal R^2 and adjusted R^2 tells us that all of our features are contributing to our model. Adjusted R^2 penalizes the R^2 formula based on number of variables, so a same score tells us that our variables are all contributors.

> F-statistic and Prob(F-statistic) tell us if our variable group as a whole is statistically significant. The null hypothesis is a model with no variables (only intercept). Our prob(f-statistic) evaluates the chance that our null hypothesis is true and our variables have no effect. On our model this chance is so low that it's functionally 0. F-statistic is evaluating all of the coefficients used together, so p-value of individual coefficients is still important. So this number tells us that our MODEL is significant without telling us if any individual feature is significant.

> Omnibus and prob(omnibus) tell us that our residuals are not normally distributed. We want to see a value close to 0 for Omnibus, and a value close to 1 for Prob(Omnibus). Neither of these things is the case. We saw heteroscedasticity on the residuals for all of our model types that we tried. All of our models seem to perform well at lower prices and then variance increases as price increases. This was true on both linear and nonlinear approaches such as decision trees.
>![Residuals](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/residuals.png)

> Our data is skewed slightly left. Our data has high kurtosis which implies tighter grouping of our residuals around zero and fewer outliers, which implies a fitted model.

> Durbin Watson is a measure of homoscedasticity - an even distribution of errors. We are showing slight heteroscedasticity because we'd like to see this number between 1 and 2. We saw the heteroscedasticity in the residuals.

> Our low condition number implies no multicollinearity with our features.

> Overall our characteristics are mediocre. Our high omnibus and above 2 Durbin-Watson are problematic. But no better model was found to correct for the heteroscedasticity.

## Conclusion

#### What are the primary factors influencing housing prices in the King County metro area?
> As square footage increases so does quality of materials. Most importantly you can see the upward price trend with both increased square footage and materials grade. I was intrigued that our lower bound of data points is very linear, but as our square footage increases, the upper bound gradually breaks away with higher variance. 
>![Total Price per Total Square Footage, by Grade](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/pr_grade.png)

>Here we are showing our price per square foot compared to total square footage, colored by our zipcode median value rank. I ranked the 70 zip codes in King County by median home value, and used those ranks to color our data points.  Our low median zip codes have a low price per square footage, and you can see in the color bands how our price per square foot increases with zip code median, which makes sense, but also shows the importance of zip code to pricing. I found it interesting in this visual how while most zip codes exhibit a clear trend of price per square foot decreasing with increased total square footage, which is entirely normal,  certain very high value zip codes seem to retain their high price per square foot regardless of total square footage. These breakaway values correspond to the previous slide's upper bound with more variance. Certain zip codes seem immune to the usual price per square foot decay. 
>![Price per Square Foot per Total Square Footage, by Zip Code Median](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/pr_sf_zip.png)

> As they say, location is everything, and it is the primary influencing factor for a home price in the King County metro area. Our darkest areas, and therefore highest value sales, are clustered in and around Seattle to the west of Lake Washington and into the eastern lake cities of Bellevue and Redmond which are the technical employer hubs of the region. As we move away from Seattle and the tech hubs into the suburbs, our prices clearly go down.

>![Housing Sales in King County by Location](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/map_housing_dots_cropped.png)

> These three features alone - square footage, grade, and zip code - explain 85% of the price variance.

#### Can we effectively use a regression model based system for realtors to determine a proper list price?
> Our regression model, while explaining over 88% of the price variance with our features, was nonetheless far from accurate in absolute terms. A mean average error of 56k in either direction is a huge variance to a home price - one that is so large that it renders the prediction much less meaningful and useful. Other models need to be explored, better data needs to be sourced, or easy-to-use features that an average realtor is capable of evaluating/acquiring should be added to the model to improve its predictive quality. The model is providing at best a baseline starting point.

#### Is a model-based system more accurate for determining list price than the traditional comps-based system?
>At present, the regression model is only slightly more accurate than the comps-based system on our test data - and this is even with our comps-based simulator lacking a feature set as robust as our model. In fact our realtor simulator performed better on new data than our model. The model is lacking something - quality start data, predictive features, or something else - and we should identify and include them.
> The house in this image sold for 665k. The model predicted it at 784k, while the "realtor simulator" used comps to predict it at 663k. While this is a particularly egregious example of the disparity between our model and comps, it certainly highlights the problem - the model is currently only a baseline, and requires comp work regardless to produce a confident final answer.

>![Figure 1 - Housing Sales in King County by Location](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/images/comps_plat.png)

> With our model one major pro is it is a mathematical model and we can use it without housing data on hand. It would be benefited by up to date data, but it doesn't require it to function. This certainly results in less labor overhead as it only needs occasional updating. However the wide error range gives only a starting point, and it ultimately requires human intervention to determine final price, which is likely a comps-based manual pass anyway.

> The comps based system, on the other hand, is a familiar method for realtors. It somehow more accurately captures the location granularity that the model misses. And most importantly, it can still be accomplished programmatically, as I've demonstrated, which can provide a quicker starting point for a realtor instead of them identifying the comps manually. The downside here is cost of maintenance - the comps finder requires the entire data set to be present to function, and it must be updated frequently, preferably daily, for most accurate results. With that in mind the realtor simulator requires a lot more overhead to remain usable.

#### What easy-to-use features can we add to our model to increase its accuracy?

>I would consider two different models that separate urban and suburban areas, to better capture the non-decaying price per square foot in our high value zip codes that we saw back on our square footage visualization.

> I'd source better data for this project. Data that includes the type of sale would be incredibly important to weed out non-market sales which may be hurting our model.  When I searched out new data on which to test our completed model I saw a large proportion of non-standard sales on record, and this adds noise to our data.

> I want to use latitude and longitude as a more granular location identifier in place of zip code

> If we add features to the model, they need to be ones that an average realtor is capable of finding and utilizing with average Google skills. We could add frontend GUI features and backend web scraping that allows some of these things to be run by the model software. For example, using latititude and longitude, GreatSchools.org can tell a property's exact school assignments and ratings. A realtor doesn't know lat and long, but we can use under the hood web scraping that takes the address and uses a reverse address finder such as at https://www.latlong.net/Show-Latitude-Longitude.html to determine lat/long, then takes that result to GreatSchools.org to scrape for school information. Lat/long can also be utilized within the model in combination with the many GIS map tools available from King County about public services, parks, school districts, area income and more to obtain and enter data without the realtor needing to do any more than enter an address.


## Recommendations for Future Work

> For future work, I'd like to utilize lat and long to find things like school information and write an address lookup tool to easily obtain these lat/long values. We can integrate additional map information to get proximity of grocery stores and restaurants for a walkability score, distance to public services, parks, waterfront areas. It might also be worthwhile to use location to study larger non-discriminatory census metrics such as household income for an area. All of these additions are easily performed under the hood where all a realtor needs to enter is a property address

> King County in particular offers comprehensive map data which can be integrated into our work via geopandas. These maps include information on school district and average household income which I suspect would be strong predictors. We can also use the King County map information to determine other metrics such as parks and public services, distance to waterfront, and other proximity-based features. Using these in conjunction with retooling our model for higher lat/long granularity should improve our predictions.

>If all else fails, we can fall back to working on our realtor simulator. If we can develop multipliers for more binary elements such as if a property has a view, is on the waterfront etc we might be able to further refine the realtor simulator. Either way it could serve as a valuable tool to help agents find comparative properties quickly rather than manually.

> Regardless of what we choose, a front-end GUI that our agents can use would be the final goal


## Presentation
[Video - Data Science Module 2 Project](https://youtu.be/vsyFdHGtmqM)

[PDF of Presentation](https://github.com/threnjen/dsc-mod-2-project-v2-1-online-ds-sp-000/blob/master/mod_2_project.pdf)
