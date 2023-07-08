# REGRESSION MODEL FOR HOUSING DATA.

## Introduction.
Housing projects consist of several different factors that determine the quality of the final product which is a house. Housing project can be managed by a real estate agency which is a business that arranges the selling, renting, or management of homes, land, and buildings for their owners. A real estate agency is a key player in the housing market, attracting both local and international investors who seek to capitalize on the lucrative opportunities presented by real property. With the advent of technology and availability of vast amounts of data, investors are increasingly turning to quantitative ananlysis and machine learning techniques to determine the factors that affect the sale price of houses in the real estate industry.


## Overview.
This project aims to determine the specific factors that increase or decrease the sale price of a housing unit by using a range of specific factors within the data provided. The target partners include; real estate agencies, construction companies, home owners who are interested in selling and potential home owners looking to buy. By determining the factors that affect the sale price of a house, I hope to provide them with valuable insights that can inform their investment decisions and enable them to optimize their investment returns. My aim is to use statistical analysis to identify the specific factors that affect the sale price of houses represented in the King County housing dataset.

## Problem statement.
Historical housing data exists in enormous quantities, but it is mostly comprised of reports compiled after the house has been sold. This makes it hard to deduce the specific factors that affected the sale price of the houses. Determining which factors have the most significant effect on the final selling price of a house is crucial in making informed decissions about whether to invest in specific aspects such as renovations, expansions or even the housing unit as a whole. I hope to provide an accurate linear regression model that helps real estate agencies, construction companies, home owners who are interested in selling and potential home owners looking to buy make informed decissions. This research will lead to a better understanding of the housing industry and increase returns on investments.


## The Data
This project uses the King County House Sales dataset, which can be found in  `kc_house_data.csv` in the data folder in this project's GitHub repository. The dataset contains 21597 rows and 21 columns, out of the 21 columns in the dataset, only 12 columns are used in the project process. The columns that are dropped are;
> - date<br>
> - sqft_above<br>
> - sqft_basement<br>
> - yr_renovated<br> 
> - zipcode<br> 
> - lat<br>
> - long<br>
> - sqft_living 15<br>
> - sqft_lot15<br>

These columns are dropped because some of them i.e. sqft_above and sqft_basement have almost the same data as sqft_living and sqft_lot. The date, zipcode, lat and long have litle to no bearing at all on the sale price of the houses. After cleaning the data, the next step was identifying any missing values and dropping the rows with missing values. This provided the best solution for dealing with missing values because the rows with missing values were few and not likely to affect the outcome of the regression model. Finally I checked for duplicated records and droped the duplicates.


## Data preparation.
The target variable in this project was the selling price of the houses. But before I could come up with a regression model detailing the specific metrics that affect my target varible, I first had to perform the following statistical analysis on the dataset.

> I) I checked to see how the price data was distributed and discovered that it was not normally distributed. The data had a high positive skew, meaning that there were longer tails in the higher price range. The data also happened to be leptokurtic, which meant that the data had heavy tails and that there were more outliers.<br>

> II) I then performed a statistical analysis to whether the price data obeyed the __Central Limit Theorem__. The data did obey the central limit theorem and this was an indication that this dataset is statistically significant.<br>

> III) Next, I used hypothesis testing to determine the effect of a waterfront on the price of a house and tested the hypotheses using a two sample t-test in order to obtain a p-value to compare to an alpha value of 0.05. The p-value(0.0) obtained was less than the alpha value(0.05) and so I rejected the null hypothesis and conclude that the presence of a waterfront has an effect on the selling price of a house. The following were the hypotheses I came up with and tested;<br>

    > __Null Hypothesis__<br>
    > H0 = The presence of a waterfront has no effect on the price of a house.

    > __Alternative Hypothesis__<br>
    > H1 = The presence of a water front has an effect on the price of a house.

### Modeling.
In order to create the regression model, I needed to use columns with numerical data types. The numerical columns were copied into a new variable that was be used to create the regression model. The numerical columns chosen for the modelling process were:
> - price<br>
> - sqft_living<br>
> - sqft_lot<br>
> - yr_built<br> 
> - bedrooms<br> 
> - bathrooms<br>
> - floors<br>

Since correlation is a measure related to regression modelling, I checked the correlation between price and these variables and discovered that they had a medium-to-strong correlation with the price. Since sqft_living had the strongest correlation with the price, I used it to create a simple regression model that would be evaluated against the multiple regression model.

> __Interpreting the simple model__<br>

The formula set-up was:<br>
   > price = 283.40(square-feet) - 48607.47<br>
    
* The model was statistically significant overall, with the f-statistic p-value well below 0.05.
* The model explained about 50% of the variance in price.
* The model coefficient (const and sqft_living) were both statistically significant, with t-statistic p-values well below 0.05.
* Given that a house had 0 square-feet of living area, the price of the house dropped by 48,607 dollars.
* For each increase in 1 square-foot of of the living area, we saw an associated increase of 283.40 dollars in the price of the house.

> __Multiple linear regrssion model.__<br>
Now that I had a simple model that would be used to evaluate the final model, I went on and create a multiple linear regression model that included all of the numerical datasets. 

#### One-Hot encoding categorical variables.
This step of the modelling process involved creating dummy variables from categorical columns, i.e bedrooms. Once the dummy variables had been created, I will dropped one of the dummy variables so as to avoid the __dummy variable trap.__ The dropped variable was then considered to be the refrence category.

#### Interpreting the multiple regression model.
    
* The model was overally statistically significant, with the f-statistic p-value well below 0.05.
* The model explained about 56% of the variance in price. Which was an improvement from the simple model.
* Not all the model coefficients were statistically significant. Two coeficients (bedrooms_4 and bedroom_5) were both not statistically significant, with t-statistic p-values above 0.05.
* Given that all other predictors were 0, the price of the house was 6,072,946 dollars. Which is obviously not a real world value considering that a house should atleast have one of the other factors available.
* The refrence category for the number of bedrooms was any other number of bedrooms aside from the ones used in the model.
    * When a house had 2 bedrooms as compared to any other number of bedrooms besides 2, 3, 4 and 5, we saw an associated increase of 191,849.5 dollars in the price of the house.
    * when a house had 3 bedrooms as compared to any other number of bedrooms besides 2, 3, 4 and 5, we saw an associated increase of 93,730.56 dollars in the price of the house.
* For each increase in 1 bathroom, we saw an associated increase of 61,256.36 dollars in the price of the house.
* For each increase in 1 square-foot of the living area, we saw an associated increase of 305.33 dollars in the price of the house.
* For each increase in 1 square-foot of the lot area, we saw an associated decrease of 0.31 dollars in the price of the house.
* for each increase of 1 floor, we saw an associated increase of 55,786.64 dollars in the price of the house.
* for each year newer the house is, we saw an associated decrease of 3,270.37 dollars in the price of the house.


#### Changes to the model.

In order to get a better model, I had to make a few iterations to the multiple linear regression model.<br> 
> * First of all, the sqft_living coeficient explained a lot about the change in the price of a house leaving very litle to be explained by the sqft_lot coeficient. Thus, I dropped the sqft_lot coeficient from the modelling dataset.<br>
> * Secondly, choosing the bedrooms_other dummy category as the refrence category made it harder to interpret the bedrooms coeficients. I instead made the bedrooms_2 dummy category the refrence category.

#### Interpreting the final model.
    
* The model was overally statistically significant, with the f-statistic p-value well below 0.05.
* The model explained about 56% of the variance in price. Which was the same as the first multiple regression model.
* All the model coefficients were statistically significant with t-statistic p-values well above 0.05. This was the difference between the first model and the final model, not all coeficients were statistically significant in the first model.
* Given that all other predictors were 0, the price of the house was 6,311,447 dollars. Which is obviously not a real world value considering that a house should atleast have one of the other factors available. This was not too far off from the intercept value of the first multiple model.
* The refrence category for the number of bedrooms was a 2 bedroomed house.
    * When a house had any other number bedrooms besided 3, 4 and 5, as compared to a 2 bedroomed house, we saw an associated decrease of 189,512.8 dollars in the price of the house. This was surprising because this category contains houses with 1 bedroom and any other number of bedrooms above 5. 
    * When a house had 3 bedrooms as compared to a 2 bedroomed house, we saw an associated decrease of 97,025.53 dollars in the price of the house.
    * When a house had 4 bedrooms as compared to a 2 bedroomed house, we saw an associated decrease of 176,290.3 dollars in the price of the house. This is an new addition to the model since it was not statistically significant in the first model.
    * When a house had 5 bedrooms as compared to a 2 bedroomed house, we saw an associated decrease of 197,334.1 dollars in the price of the house. This is also a new addition to the model since it was not statistically significant in the first model.
* For each increase in 1 bathroom, we saw an associated increase of 62,650.7 dollars in the price of the house. Which was almost the same effect on the price of the house by the bathroom coeficient as compared to the first model. 
* For each increase in 1 square-foot of the living area, we saw an associated increase of 301.2 dollars in the price of the house. Which was not a big difference in the effect on the price of the house by the square-feet of the living area coeficient as compared to the first model.
* For each increase of 1 floor, we saw an associated increase of 57,798.7 dollars in the price of the house. Which was not a big difference in the effect on the price of the house by the number of floors as compared to the first model.
* For each year newer the house is, we saw an associated decrease of 3,295.95 dollars in the price of the house. Which was not a big difference in the effect on the price of the house by the year it was built compared the first model.

## Conclusions.
> * Though few, houses with waterfronts fetch more money than houses without waterfronts.<br>
> * Houses with excellent views have the highest price average while houses without a view have the lowest price average.<br>
> * Houses that are in very good condition fetch the highest amount of money. The unexpected finding here is that houses that are in poor to fair condition almost have the same price average, with poor conditioned houses averaging slightly more money than fair conditioned houses.<br>
> * House prices are mostly influenced by the size of the living area.<br>
> * From the final model, I can conclude that the number of bathrooms and floors in a house have the highest positive effect on the price of the house.<br>


## Recommendations.
The recommendations have been tailored to each of the indivual target partners.

#### i) Real estate agencies.
> * The agency should consider listing more houses that have waterfronts and excellent views because these houses are guaranteed to have a higher value than houses without waterfronts or views.<br> 
> * The agency should also try to steer clear of houses that are in poor condition and houses that are of a lower grade than 7. These houses fetch litle money and are hard to sell.<br>
> * The price of a house that has 2 or more floors and 2 or more bathrooms is guaranteed to increase by over 200,000 dollars. Listing more houses like these will lead to increased revenue for the agency.<br>

#### ii) Construction companies.
> * When building houses for sale, a construction company should consider building more houses with spacious living areas. The square footage of the living area should be greater than the square footage of any other area of the house as this has a direct effect on the price of the house.<br>
> * The houses should also be fitted with more bathrooms and more floors. These two factors are positively related to the price of a house, which means that the more the number of bathrooms and floors, the higher the value of the house.<br>

#### iii) Home owners who are interested in selling.
> * Before putting up the house for sale, home owners should consider making some renovations to the house so as to improve the condition of the house. Putting up the house for sale when its condition is average might lower the value of the house, so it is better to invest in some renovations where needed.<br>

#### iv) Potential home owners who are looking to buy.
> * When looking for a house to buy, a potential home owner should focus on finding a house that has more bedrooms and fewr floors. This type of house is guaranteed to be cheaper as the model has shown that the more the number of bedrooms, the cheaper the house becomes but the more the number of floors, the higher the price of the house.<br>
> * Another factor to consider is that, houses with waterfronts and excellent views are very expensive. Potential home owners who have a tight budget should focus on houses without waterfronts and with fair views in order to minimise the cost.<br>
> * If one is trying to make a business out of buying and reselling houses, a good tactic would be to buy houses that are in poor conditions and renovate it so as to improve the condition of the house before selling it at a higher price. One thing to avoid though is buying low grade houses because it is harder to improve the grade of a house especially if it is tied to the grade of the neighbourhood.<br>
