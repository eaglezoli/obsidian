---
banner: https://images.unsplash.com/photo-1462642109801-4ac2971a3a51?q=80&w=1673&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
banner-inline-title-color: "#222222"
banner-x: 50
banner-y: 45
---
********

## Bilateral Setup
- Single patient
	- Left and right arm/leg
	- Peripheral arterial disease
- Multiple patients
	- One way valves
## Experiment
- FR 1–6 L/min (1, 2, 3, 4, 5)
- HR 60–180 bpm (60, 90, 120, 150, 180)
- Two vessel stiffnesses – healthy and unhealthy (need to determine elasticities)
## Data Analysis
- Mixed effects model has funnel shape
	- Tried log transform of AUC 
		- Helped, but still funnelled the other way
- Generalised Additive Model
	- 
- **Regression**
	- Continuous data
- **Prediction**
	- Discrete data
	- Decision Tree
	- XGBoost
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

- <span style="background:rgba(3, 135, 102, 0.2)">KEEP IT SIMPLE!</span> – Decide what the **aim** is?
	- Just focus on what I need to finish the chapter
	- Doesn't need to be a two-volume statistical study
	- Can always continue the research afterwards
![[Wiki#^gam-info]]

> [!todo]
> ### Aims
> 1. Find which features are most **strongly correlated** with FR and HR
> 2. **Interaction effect** of stiffness, FR and HR on select features
> 3. Highlight how **unhealthy** vessels **respond differently** to changing **flow dynamics**

### Improvements
- Feature naming/numbering system
- Remove collinear features
### Meeting James
- Double check
	- LOESS curve – should be more curved?
	- Boxplot – why are both channels the same?
		- Do with specific FR and HRs
### Meeting Juan
- Principal Component Analysis (PCA)
	- Order reduction
	- Reduce features
	- Find combination features – optimise
	- Scikit learn
- Steps
	1. Regression
	2. Confidence intervals probability distribution
	3. Gaussian process regression (for FR and HR, same model for both)
	4. Confidence interval plot – show overlap at low flow and gap at high