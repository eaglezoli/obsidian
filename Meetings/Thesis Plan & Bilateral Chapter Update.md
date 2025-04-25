```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
# Thesis Plan

| Week  | Date                      | Main Chapter                | Small Chapter       |
| :---: | :------------------------ | --------------------------- | ------------------- |
| **1** | 14<sup>th</sup> **April** | **10. Bilateral**           |                     |
| **2** | 21<sup>st</sup>           |                             |                     |
| **3** | 28<sup>th</sup>           |                             |                     |
| **4** | 5<sup>th</sup> **May**    | 5. Rig                      | 8. Vessels          |
| **5** | 12<sup>th</sup>           | 7. Proxy                    | 3. PPG              |
| **6** | 19<sup>th</sup>           | 11. Classification          | 2. CVD              |
| **7** | 26<sup>th</sup>           | 6. Thickness                | 4. Lit. Review      |
|   8   | 2<sup>nd</sup> **June**   | 12. Discussion & Conclusion | 1. Intro & Abstract |

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

# Bilateral Chapter – Data Analysis
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