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
> 1. Find which features are most **strongly correlated** with ~~FR and HR~~ ***stiffness***
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

[**Colour Palette**](https://pixelied.com/colors/palette-editor/edb120-d95319-4dbeee-0072bd-60c899-d681d2)
![[palette.png]]

1. Visualisation
	- To Do
		- Split line plots & box plots for healthy/unhealthy red/IR like Matlab
		- Multi-coloured scatter plots
	- Double check
		- LOESS curve – should be more curved?
		- Boxplot – why are both channels the same?
			- Filtering with specific FR and HRs, and one wavelength helped!

2. Cross Correlation
	- Looks good on first look
	- Correlation with *vessel health*
		- Only two levels (healthy/unhealthy), but still did correlation with corrr_var
			- Categorical gives same results as with elasticity values (as there are only two)
	- Updated colour palette
	- Correlation with FR & HR
		- Healthy vs unhealthy
		- Red vs infrared
	- Export as table
		- Following original order of features list
		- Stacked horizontally to fit together with only one features column
		- Values and signs matching graphs
	- **Observations**
		- IR features are more correlated with stiffness than red
			- IR mostly negative correlations
				- Red mixed
		- FR and HR are much more influential on PPG features (both wavelengths), as expected
			- They have opposite effects
				- FR more positive (larger waveform)
					- HR more negative (smaller waveform)
				- Can use heart rate to adjust flow rate predictions from PPG-based algorithms
					- Maybe link to BP?
	- **To do**
		- Redo graphs
			- Remove 'file' variable
			- Correct 'upslope' and 'onset' typos
			- Make IR graph taller and lighter to show .9
		- Captions for graphs and table

3. Mixed Effects Model
	- Funnel shape residuals
		- Log transform of AUC helped, but still funnelled the other way
	- Next
		- Just go with the mixed effects models as it is (with the funnel)
		- Currently just linear, try upgrade to non-linear
			- Generalised Additive Model (GAM) ![[Wiki#^gam]]
		- Look at statistical methods of other papers
			- Thomas – ANOVA, Pearson Correlation Coefficient
			- Elisa – Poincare Plots
		- Maybe try ANOVA
		- Do analysis for each feature

4. **Generalised Additive Model (GAM)**
	- Textbook gam doesn't show both vessels in one graph, also graphics look dated
	- [This](https://stackoverflow.com/questions/75502600/visualize-generalized-additive-model-gam-in-r) shows both and looks better
		- Plotted fitted values with confidence intervals
		- Plotted difference bands with spot tests (chatGPT)
	- Filtering out HRs improved gap a little
	- Separate analysis for Red/IR
		- Matches cross correlation results!
	- Function loop for all features
	- **Observations**
		- GAM matches cross correlation results
		- FR
			- *Red*: [[correlation-stiffness-red.png|length-height ratio]] is the highest correlated feature, *double* the 2nd
				- Shows potential for [[gam-red-stiffness-length_height_ratio.png|geometry ratios]]
					- May be linked to 2nd derivative ratios e.g. a/b
				- Need to look at example waveforms and geometrical measurements
				- But why is it not present on IR?
					- It is higher than IRs most correlated feature
					- Need to compare red and IR waveforms
			- *IR*: Upslope (-ve) and downslope (+ve) have different correlation signs
				- As does start (-ve) and end (+ve) datum areas, which also matches the upslope downslope signs
				- Shows that stiffness affects systolic and diastolic segments of the PPG differently 
				- Again need to look at example waveforms
			- SNR is higher in healthier, as expected
				- Flow rate doesn't seem to effect, so it's constant difference (offset)
					- For both wavelengths
		- HR
			- Shows a line with multiple curves
	- **To do**
		- Show example waveforms and geometrical measurements
		- Difference confidence bands
		- Against HR
		- y-axis feature name and unit

5. Interaction 
	- **Observations**
		- FR and HR have opposite effects on features
			- FR more positive (larger waveform)
				- HR more negative (smaller waveform)
			- Can use heart rate to adjust flow rate predictions from PPG-based algorithms
				- Maybe link to BP?
	- **To do:** MATLAB function
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