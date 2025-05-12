---
banner: https://images.unsplash.com/photo-1462642109801-4ac2971a3a51?q=80&w=1673&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
banner-inline-title-color: "#222222"
banner-x: 50
banner-y: 45
---
********

-  <span style="background:rgba(3, 135, 102, 0.2)">KEEP IT SIMPLE!</span> – Decide what the **aim** is?
	- Just focus on what I need to finish the chapter
	- Doesn't need to be a two-volume statistical study
	- Can always continue the research afterwards

> [!todo]
> ### Aims
> 1. Find which features are most **strongly correlated** with FR and HR
> 2. **Interaction effect** of stiffness, FR and HR on select features
> 3. Highlight how **unhealthy** vessels **respond differently** to changing **flow dynamics**

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
![[Wiki#^ml-methods]]

- **Visualisation**
	- To Do
	- Double check
		- LOESS curve – should be more curved?
		- Boxplot – why are both channels the same?
			- Do with specific FR and HRs

- **Cross Correlation**
	- Looks good on first look
	- To do
		- Correlation with *vessel health*
		- Correlation with FR & HR
			- Healthy vs unhealthy
			- Red vs infrared
		- Export as table

- **Mixed Effects Model**
	- Funnel shape residuals
		- Tried log transform of AUC 
			- Helped, but still funnelled the other way
	- **Next**
		- Just go with the mixed effects models as it is (with the funnel)
		- Currently just linear, try upgrade to non-linear
			- **Generalised Additive Model (GAM)** ![[Wiki#^gam]]
		- Look at statistical methods of other papers
			- Thomas – ANOVA, Pearson Correlation Coefficient
			- Elisa – Poincare Plots
		- Maybe try ANOVA
		- Do analysis for each feature

- **Generalised Additive Model (GAM)**
	- Textbook gam doesn't show both vessels in one graph, also graphics look dated
	- [This](https://stackoverflow.com/questions/75502600/visualize-generalized-additive-model-gam-in-r) shows both and looks better
		- Plotted fitted values with confidence intervals ✔️
		- Plotted difference bands with spot tests (chatGPT) ✔️
	- Filtering out HRs improved gap a little
	- **Next**
		- GAM for each feature
		- Rename y-axis with feature name and unit

- **MATLAB interaction** 
	- To Do
### Improvements
- Feature naming/numbering system
- Remove collinear features

### Juan Meeting
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