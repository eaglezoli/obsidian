```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

## Data Visualisation

![[visualisation.png]]

## Data Analysis
- **Regression** – *Continuous* data
- **Prediction** – *Discrete* data
- Algorithms
	- Decision Tree
	- XGBoost

^ml-methods

### Mixed Effects Model
- Mixed models were developed to allow us to use all our data, even when we have low sample sizes, structured data and many covariates to fit


![[linear-approach.png|Linear Approach]]

![[mixed-effect-model.png|Mixed Effects Model – Random Intercepts and Slopes]]

- **Fixed effects**
	- Variables that we expect will have an effect on the dependent/response variable
	- **Explanatory** variables in a standard linear regression
	- We are interested in making conclusions about how vessel stiffness impacts PPG features
	- Fixed effect: vessel stiffness
	- Dependent variable: PPG features

- **Random effects**
	- **Grouping factors** for which we are trying to control
	- Always **categorical**
		- You can't force R to treat a continuous variable as a random effect
	- A lot of the time we are not specifically interested in their impact on the response variable, but we know that they might be influencing the patterns we see
	- Golden rule: you generally want your random effect to have **at least five levels**
		- E.g. gender would be a fixed effect not random

### Generalized Additive Model (GAM)
- Nonlinear and multiple predictors
- With many variables, interactions can be missed

^gam