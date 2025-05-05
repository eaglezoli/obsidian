## Data Visualisation
![[visualisation.png]]

## Data Analysis
### Mixed Effects Model
- Mixed models were developed to allow us to use all our data, even when we have low sample sizes, structured data and many covariates to fit
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