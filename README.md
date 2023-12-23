# Data-Analysis-2 Final Project
--- 

## Introduction


In response to the COVID-19 crisis, the U.S. Federal Government, led by the Trump administration in 2020, initiated the Paycheck Protection Program (PPP). Designed to support a range of entities including businesses, self-employed workers, nonprofits, and smaller enterprises, this program offered low-interest loans. Its primary objective was to aid in covering essential expenses such as payroll, rent, interest, and utilities. Notably, businesses that maintained stable employee numbers and wages had the opportunity for partial or complete loan forgiveness. This report seeks to explore how these loans were distributed.


**My research question:**
How do business ownership characteristics, specifically ethnicity, gender, veteran status, and political affiliation of the state, along with the proportion of Black residents in a state, collectively influence the loan amounts received through the Paycheck Protection Program?


## Data


To run my analysis, I collected my data from the [Black Wealth Data Center website](https://blackwealthdata.org/explore/business), and I enriched my data with the political affiliation of the state, by looking at the governor of the state in 2020 and his/her political party. I gathered this information from the website of [Ballotpedia](https://ballotpedia.org/List_of_current_governors_in_the_United_States).


## Data Cleaning


The original dataset includes 1,206,970 observations as the geographical grouping of the data is broken down to state, county, and zip code level, resulting in the file taking up too much memory for me to push it to GitHub. To fix this, I have filtered down to only state-level observations. I also excluded those observations which were unanswered in certain categories. In the end, I overwrote the original file to save space.

This cleaning was done in `01_initial_cleaning_code_working.ipynb` which cannot be run again, as it overwrote the original file to save space. This file is located in the `work files` folder

## Descriptive Statistics

![image](https://github.com/szilvasipeter2000/Data-Analysis-2/assets/144559314/c858b816-9c47-458e-89c7-a12395b38b72)

The table summarizes the main characteristics of the dependent, explanatory, and control variables. For the regression analysis, I'll utilize the natural logarithm of the loan amount due to its skewed distribution. This logarithmic transformation aids in achieving a more symmetrical and normally distributed data. From the original dataset, I also created four binary variables, as shown in Table 2. For each measurement we have 807 observations and 0 missing values. White owned businesses are 25.28% of all businesses, while the remaining categories—male, non-veteran, and republican—each represent approximately half. This is a result of the structure of the dataset. Loan amounts are aggregated and grouped by state and different ownership characteristics. In the appendix I included detailed graphs about the distribution of each variable.

## Regression Models

![image](https://github.com/szilvasipeter2000/Data-Analysis-2/assets/144559314/2def8a5f-3c4e-4d1d-8a1e-ffe3792a54e4)

In Model (1), the constant indicates the average natural logarithm of loan amount for businesses not white-owned is 15.683. The "White Owned" coefficient suggests a 99% confidence that when the variable changes from 0 to 1, the ln loan amount rises by 2.697, equivalent to a 1383.31% increase. The R2 indicates 18.9% variability in the dependent variable is influenced by ownership status. However, the model’s Residual Error is considerably high, as we are looking at logarithmic values. To perfect the model, we can include controlling variables. In models, (2), (3), and (4), I included step-by-step one more variable to our model to see how each of them effect our dependent variable. All our controlling variables’ coefficients are statistically significant at 99% confidence level.  However, building on this model, I’ve further enhanced the regression to also include the Percentage of Black Population, and an interaction between White Owned and Male Owned. For Black Population Percentage, I incorporated a piecewise linear spline with a knot (or breakpoint) set at 12%. This decision is based on visual observations from Graph 1, specifically noting a change in direction of the loess smoothing line at 12%. Graph 1 also visualizes White Owned businesses, and it’s visible that there are almost no loans for these businesses below Ln Loan Amount of 15 and the highest values correspond to White Owned Observations.

Graph 1: Piecewise Linear Spline with knot at 12% for the Percentage of Black Population Variable 
![image](https://github.com/szilvasipeter2000/Data-Analysis-2/assets/144559314/f7abaf39-ecf6-49d1-a745-85e5ebe7b9c7)

![image](https://github.com/szilvasipeter2000/Data-Analysis-2/assets/144559314/6558736f-550c-4a42-982f-1909fa4581bb)

My final regression, Model 2, includes all previously discussed variables and shows key insights into how the loans were distributed. White, Male, Non-Veteran are in all positive correlation with the Loan Amounts. If we are looking at loans with the same characteristics, White Owned Businesses tend to get 1013.53%, Male 196.33%, and Non-Veteran Businesses 2581% more loans on average than those that are Non-white, female or veteran owned. Additionally White Male owned businesses got 94.20% more loans than those that are not White Male owned. Interestingly when looking at Republican and Democratic states, Republican ones got on average 35.37% less loans than Democratic states. As for Black Population, there was a positive correlation until 12% as anticipated. On average, in states where the percentage of black population is less than 12%, 1% more black people means an increase of loan amounts by 27.04%.  This trend changes above 12%, to -5.16%. Note that all these values are valid within a 99% confidence interval. The R-squared of the model is also quite high with 0.73 while our Residual Error is also lower than what we saw in Model 1 meaning that including splines and interaction was a good addition to the regression.

## Conclusion
To address the question of how different business ownership traits affect the distribution of Paycheck Protection Program (PPP) loans, Model 2 provided significant insights. White, Male, and Non-Veteran owned businesses stood out, receiving notably higher loan amounts under the Trump administration's PPP. This points to a clear inequality within the dataset. Even though all the coefficients are 99% statistically significant and we should be able generalize to the population our data represents, this is as far this dataset takes us. We do not have data about the percentage of white businesses, compared to other ethnic groups, just as we do not have information who applied for these loans and who got it. Nevertheless, the results show that grouped by states and ownership characteristics, White, Male, and Non-veteran businesses received an advantage in times of aid from the Trump Administration.



