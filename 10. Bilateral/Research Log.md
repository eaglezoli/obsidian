## Bilateral Setup
- Single patient
	- Left and right arm/leg
	- Peripheral arterial disease
- Multiple patients
	- One way valves
## Data Analysis
- Mixed effects model has funnel shape
	- Tried log transform of AUC 
		- Helped, but still funnelled the other way
### Next
- Just go with the mixed effects models as it is (with the funnel)
	- Currently just linear, try upgrade to non-linear
		- Generalised Additive Model (GAM)
			- Nonlinear and multiple predictors 'added'
			- With many variables, important interactions can be missed
- Look at statistical methods of other papers
	- Thomas – ANOVA, Pearson Correlation Coefficient
	- Elisa – Poincare Plots
- Maybe try ANOVA
- Do analysis for each feature
- KEEP IT SIMPLE!
	- Just focus on what I need to finish the chapter
	- Doesn't need to be a two-volume statistical study
	- Can always continue the research afterwards
- Decide what the goal is?
	- Regression
		- Continuous data
	- Prediction
		- Discrete data
		- Decision Tree
		- XGBoost
- **The Goal**
	- Which features increase with FR and HR
	- Interaction effect between FR and HR on features
	- Highlight the difference in the gap between healthy and unhealthy vessel at low flow and high flow
	- Highlight difference in response to changing flow dynamics between healthy and unhealthy vessels
### Meeting with James
- Double check
	- LOESS curve – should be more curved?
	- Boxplot – why are both channels the same?
### Meeting with Juan
- Principal Component Analysis (PCA)
	- Order reduction
	- Reduce features
	- Find combination features – optimise
	- Scikit learn
- Regression -> confidence intervals probability distribution -> gaussian process regression (for FR and HR, same model for both) -> confidence interval plot – show overlap at low flow and gap at high
