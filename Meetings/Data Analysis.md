# Previous Paper – Significance Testing
- Ranked features by significance
- Range of 5 stiffness levels
- **To Do**
	- Train/test model
	- Classification
	- Measurement of stiffness

![[image-1.png]]

![[image-2.png]]

![[image.png]]

# Bilateral Study
- [[#Normalising|Normalising]]
- [[#Visualising|Visualising]]
- [[#Analysing|Analysing]]
	- [[#Analysing#Mixed Effects Model|Mixed Effects Model]]
	- [[#Analysing#Results|Results]]
		- [[#Results#Check Assumptions|Check Assumptions]]
			- [[#Check Assumptions#Residuals|Residuals]]
			- [[#Check Assumptions#Q-Q Plots|Q-Q Plots]]
	- [[#Analysing#Generalized Additive Model (GAM)|Generalized Additive Model (GAM)]]

## Normalising
- Tried normalising the data
	- Good for comparing features on the same scale
	- Present original data

![[histograms_AUC.png]]

![[histograms_rise_times.png]]

![[histograms_pulse_width_50.png]]

## Visualising
![[scatter-FR-stiffness-linear.png|Linear. Example feature Area Under Curve (AUC) against Flow Rate (FR). ppgA (Red) is unhealthy/stiff, ppgB (green) is healthy/elastic.]]

![[scatter-FR-stiffness-loess.png|LOESS (curved)]]

![[scatter-fr-wavelength.png|Grouped by wavelength]]

![[scatter-fr-hr.png|Against HR]]

![[scatter-fr-hr-groups.png|Grouped by HR]]

![[boxplot-stiffness-fr.png|Stiffness boxplots]]

![[boxplot-wavelength-fr.png|Wavelength boxplots]]

![[boxplot-fr-stiffness-wavelength.png|Split boxplots]]

![[scatter-HR-stiffness.png|Against HR (linear)]]

![[scatter-HR-stiffness-loess.png|Against HR (LOESS)]]
## Analysing

### Mixed Effects Model
- Considers groups in data (e.g. HR and FR groups)
- Linear
	- Trying Generalised Additive Model (GAM) – nonlinear and multiple predictors

![[linear-approach.png|Linear Approach]]

![[mixed-effect-model.png|Mixed Effects Model – Random Intercepts and Slopes]]

### Results
#### Check Assumptions
##### Residuals
- Should be straight with no patterns
![[mixed-residuals.png|mixed-residuals]]
![[mixed-quad-residuals.png|mixed-quad-residuals]]

![[mixed-residuals-not-normalised.png|mixed-residuals-not-normalised]]

![[mixed-resiudals-log.png|mixed-resiudals-log]]

##### Q-Q Plots
- Should be close to the line
	- Some deviation at beginning and end in an S shape is normal
![[mixed-qqplot.png|mixed-qqplot]]

![[mixed-qqplot-not-normalised.png|mixed-qqplot-not-normalised]]

### Generalized Additive Model (GAM)
- Nonlinear and multiple predictors
- With many variables, interactions can be missed
![[gam.png|GAM]]

![[gam-normal.png|GAM with normalised data]]

### Next
- Just go with the mixed effects models as it is (with the funnel)
	- Currently just linear, try upgrade to non-linear
		- Generalised Additive Model (GAM) – nonlinear and multiple predictors (trying currently)
- Look at statistical methods of Thomas and other papers
- Maybe try ANOVA