---
title: "The Relationship Between Poverty and Insurance Rates"
date: 2019-01-09
categories: [data-science]
tags: [economics, statistical-analysis, multiple-linear-regression, project]
header:
    image: "/images/Xilofono.jpg"
excerpt: "This report explores the relationship between health insurance and poverty in the United States, and particularly, if there is a relationship between being economially disadvantaged and being uninsured." 
---

# Uninsured Americans and Poverty 

## Executive Overview

This report explores the relationship between health insurance and poverty in the United States, and particularly, if there is a relationship between being economially disadvantaged and being uninsured. I found that there is a significant relationship between uninsured rates and unemployment rates, per capita income, and number of households impoverished; however, there is little relationship between uninsured rates and poverty rates. 

## Problem Statement

I investigated the relationship between poverty and health insurance, particularly, is poverty associated with a lack of insurance. Though the United States offers impoverished Americans health insurance through Medicaid and offers affordable healthcare through the Affordable Care Act, yet, as of 2016, approximately 27.3 million Americans remain uninsured (U.S. Census). In a survey of uninsured Americans conducted in 2017, 45 percent said that they are uninsured because the cost of being insured is too high (KFF). This problem is critical because as of 2009, approximately 45,000 deaths annually are associated with lack of insurance. Furthermore, uninsured, working age Americans have a 40 percent higher risk of death than insured Americans of the same age range (Harvard). Knowing the underlying evidences of the problem, I investigated independent variables related to poverty. I collected and processed data pertaining to uninsured rates, the dependent variable, and unemployment rates, per capita household income, number of households impoverished, and poverty rates, the independent variables. I used unemployment rates, per capita household income, number of households impoverished, and poverty rates because they are both generalized and specified indicators of poverty, and shifts in these indicators may attribute to changes in uninsured rates.

## Results

The regression outcome indicates that there is a significant relationship between uninsured rates and per capita income, unemployment rates, and number of impoverished households and little relationship between uninsured rates and poverty rates. The p-value of the regression is .00009339, meaning that the null hypothesis, uninsured rates is not related to poverty, is not rejected. As seen in Table 1.1, the p-values of impoverished households, unemployment rates, and per capita income is 0.035188, 0.007984, and 0.001314 respectively. The p-values of these independent variables indicate that there is a correlation to the dependent variable, uninsured rates. The p-values of the three independent variables are significant and further support the underlying evidences presented in the problem statement above. In regard to unemployment rates, in 2013 70.8 percent of all workers between the ages of 18 and 64 received health insurance through their employers (CNBC). In short, if a worker is unemployed, they are less likely to have health insurance, therefore, suggesting the possibility of a relationship. Further, there is evidence to support a relationship between uninsured rates and per capita income and impoverished households. In 2016, 27.3 million people did not have health insurance, and of those 27.3 million, 28.6 percent did not graduate high school, and people with less education tend to be in a lower socio-economic bracket (U.S. Census). 

<img src="{{ site.url }}{{ site.baseurl }}/images/uninsured/intercept.png" alt="coefficients">

* Table 1.1: Coefficients of the regression

In the scope of the model as it directly pertains to the data, I examined the adjusted R-square, and constructed a residuals vs fitted plot. The adjusted R-squared is .3494, which states that 34.94 percent of the variation in the dependent variable, uninsured rates, is explained by the four independent variables. Upon further examination of the data, the residual vs fitted plot illustrates that the data are randomly distributed along the horizontal axis. This suggests that the data are a good fit for the linear model.


<img src="{{ site.url }}{{ site.baseurl }}/images/uninsured/residual_fitted.png" alt="residual plot">

* Graph 1.1: Plot of residual values vs. fitted values

## Conclusion

This project investigated the relationship between poverty and health insurance and after conducting this experiment, it clarified the relationship; there is a significant relationship between impoverished households, unemployment rates, and per capita income and their insured status. The data and prior evidence suggest that economically disadvantaged Americans are less likely to be insured; however, the data used in this project only explore a part of the reality of the uninsured in the United States. To further investigate this relationship, I recommend taking a more granular and methodical data collection approach by means of survey. The survey sample size ought to be sizable enough to faithfully represent the people within a region. I believe this approach would yield a more qualitative and representative picture of the relationship between poverty and insured status.  

## Appendix A: Data Dictionary

1. **Variable_name: state**
* Variable_description: A list of 50 states in the United States. It does not include DC or territories.	
* Data_source_org: Wikipedia
* Data_source_URL: https://en.wikipedia.org/wiki/Health_insurance_coverage_in_the_United_States
* Variable_measure_type: Nominal	
* Data_type: This data is nominal, stored as text.

2. **Variable_name: hc_uninsured_rate**
* Variable_description: The rate of uninsured people, as reported by Wikipedia and derived from the US Census Bureau.
* This variable measures the percentage of people without health insurance in 2014.	
* Data_source_org: Wikipedia, US Census Bureau	
* Data_source_URL: https://en.wikipedia.org/wiki/Health_insurance_coverage_in_the_United_States	
* Variable_measure_type: Ratio	
* Data_type: This data is a ratio, stored as a percent.

3. **Variable_name: pov_house_income_thousands**
* Variable_description: The amount of people in poverty by household income, measured in the thousands, as reported by Wikipedia and derived from the US Census Bureau. This variable measures the amount of people in poverty using the rate of poverty adjusted by household income in 2017.	
* Data_source_org: Wikipedia, US Census Bureau	
* Data_source_URL: https://en.wikipedia.org/wiki/List_of_U.S._states_and_territories_by_poverty_rate
* Variable_measure_type: Interval	
* Data_type: This data is an interval, stored as a number.

4. **Variable_name: pov_rate**	
* Variable_description: The rate of poverty in a given state, as reported by Wikipedia and derived from the US Census Bureau. This variable measures the percentage of a state's population that is in poverty in 2017.	
* Data_source_org: Wikipedia, US Census Bureau	
* Data_source_URL: https://en.wikipedia.org/wiki/List_of_U.S._states_and_territories_by_poverty_rate
* Variable_measure_type: Ratio	
* Data_type: This data is a ratio, stored as a percent.

5. **Variable_name: unemployment_rate**	
* Variable_description: The rate of unemployment in a given states, as reported by Wikipedia and derived from the Bureau of Labor Statistics.This variable measures the rate at which people are lack gainful employed in 2018. This is adjusted for seasonal work.	
* Data_source_org: Wikipedia, Bureau of Labor Statistics	
* Data_source_URL: https://en.wikipedia.org/wiki/List_of_U.S._states_and_territories_by_unemployment_rate
* Variable_measure_type: Ratio	
* Data_type: This data is a ratio, stored as a percent.

6.  **Variable_name: income_per_capita**
* Variable_description: The per capita household income, as reported by Wikipedia and derived from the US Census Bureau. 
This variable measures the amount of money a household earns on average in 2015.	
* Data_source_org: Wikipedia, US Census Bureau	
* Data_source_URL: https://en.wikipedia.org/wiki/List_of_U.S._states_and_territories_by_income
* Variable_measure_type: Interval	
* Data_type: This data is an interval, stored as money.

## Appendix B: Multiple Linear Regression in R

```r
# Reads the hc_uninsured_dataset and runs a multiple linear regression

# Attaches hc_uninsured_datset 
attach(hc_uninsured_dataset_xlsx)

# Display column names 
names(hc_uninsured_dataset_xlsx)

# Display the data
hc_uninsured_dataset_xlsx

# Assign the independent variable 
uninsured <- c(hc_uninsured_rate)

# Assign the dependent variables
pov_house <- c(pov_house_income_thousands)
pov_rate <- c(pov_rate)
unemployment <- c(unemployment_rate)
income <-c(income_per_capita)

# Runs a multiple linear regression
uninsured_regression <- lm(uninsured ~ pov_house + pov_rate 
                           + unemployment + income)

# Displays results of multiple linear regression
summary(uninsured_regression)

# Displays confidence interval
confint(uninsured_regression, level = 0.95)
plot(uninsured_regression)
```

## Appendix C: Residuals and Coefficients 

<img src="{{ site.url }}{{ site.baseurl }}/images/uninsured/intercept.png" alt="coefficients">

**Residual standard error:** 2.742 on 45 degrees of freedom
**Multiple R-squared:**  0.4025
**Adjusted R-squared:**  0.3494 
**F-statistic:** 7.578 on 4 and 45 DF
**p-value:** 9.339e-05

## Sources:

1. CNBC. The Number of People with Health Insurance via Jobs Remained Steady with Obamacare. https://www.cnbc.com/2016/07/13/number-of-people-with-health-insurance-via-jobs-remained-steady-with-obamacare.html

2. Harvard Gazette. New Study Finds 45,000 Deaths Annually Linked to Lack of Health Coverage. https://news.harvard.edu/gazette/story/2009/09/new-study-finds-45000-deaths-annually-linked-to-lack-of-health-coverage/

3. KFF. Key Facts about the Uninsured Population. https://www.kff.org/uninsured/fact-sheet/key-facts-about-the-uninsured-population/

4. U.S. Census. Who are the Uninsured. https://www.census.gov/newsroom/blogs/random-samplings/2017/09/who_are_the_uninsure.html

## Data

https://github.com/atAlexFM/uninsured-dataset/blob/master/hc_uninsured_dataset_xlsx.xlsx
