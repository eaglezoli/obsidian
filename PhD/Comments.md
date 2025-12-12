## Chapter 1 – Intro

- [ ] Motivation & novelty – add a paragraph about each
	- [ ] Motivation: In vitro allows for a controlled testing environment and compliments in vivo work
	- [ ] Novelty: First bilateral in vitro rig utilising PlatSil silicone gel for customising vessel stiffness
---
## Chapter 2 – CVD

- [ ] Add blood flow monitoring techniques (p29):
	- [ ] Blood pressure monitoring
	- [ ] Applanation tonometry
	- [ ] Impedance
---
## Chapter 3 – PPG
- No corrections! 🥳
---
## Chapter 4 – Lit. Review

- [ ] Computational modelling – Talk about computational model PPG investigation techniques (not just in vivo or in vitro, but in silico as well)
	- Allows for even more control than our in vitro studies as you can modify any parameter. A holistic approach would benefit from the advantages of all three pathways: in vivo, in vitro and in silico

- [ ] Images (p72 fig. 4-3) – Low resolution, update image

- [ ] Study review (p69, 2nd paragraph) – Highlight the hypothesis of the study, where they expecting to see same or different characteristics between PPGs from each side?

- [ ] In vitro (p77) – Discuss advantages & disadvantages of in vitro
	- [ ] Write about simulations
	- [ ] Explain why you decided on in vitro

- [ ] Table of papers – add a section for gaps in the literature
	- [ ] What gaps are there and why they would be desirable to address
	- [ ] Talk about the pros and cons of the literature
---
## Chapter 5 – In Vitro Bilateral Model
- [ ] Setup diagram (p92, fig. 5-1)
	- [ ] Show pump pulsatile input signal
	- [ ] Show pressure signals

- [ ] Literature gaps – What are the gaps with the literature which you address with your setup?
	- [ ] Add the contribution we discussed earlier to the end of the chapter

- [ ] Fluid – Highlight reasons for blood fluid choice and explain why you didn’t use blood
	- Methylene blue mimics blood absorption in the red-IR spectrum, which our sensor is based
	- Newtonian fluid, keeping viscosity and cell effects constant, to ensure only arterial stiffening is affecting the PPG signals and no other confounding factors
	- Provides a repeatable, tunable optical absorption without the difficulties of working with real blood

- [ ] Statistical analysis (p117) – You discussed your results in the discussion section but haven’t described them in the results section. Just add a basic visual description
---
## Chapter 6 – Custom Vessels

- [ ] Pressure signals (p147) – Explain these pressure signals
	- Why are there no pressure differences between vessels? Wouldn’t you expect a link between arterial stiffness and the pressure pulse?
		- In this study the pressure signals were used to confirm that we could see the expected pressure pulse wave, as a validation for the PPG signals, which were the primary focus, so the pressure signals were not analysed
		- I would expect a difference in the pressure signals with stiffness levels, but this was not seen
			- We attributed this to the location of the pressure sensor. Unlike the PPG sensor, which was placed directly on the vessel, showing volumetric changes, whereas the pressure sensor was placed downstream (after the vessel), so may not be enough to record pressure differences between vessels
			- This could be improved by recording pressure sensors from the vessel, but would require reworking the setup design, while ensuring not to affect the PPG signals
			- In vivo arterial stiffening and vascular ageing are systemic, and you would expect a change in the pressure pulse downstream, not just directly at the vessel. However this experiment was a localised investigation into a specific region, so the pressure differences did not appear downstream
				- The advantage of this is that we could confirm the trends in the extracted PPG features where directly related to arterial stiffening, with the absence of blood pressure changes

- [ ] Pressure sensor location (also p147?) – Add location info and explain reason
	- These were located downstream, but in the following chapter we analysed individual vessels in a single branch setup, where we recorded pressure signals before and after the vessel, however the analysis is based on the PPG signals

- [ ] Blank space (p154) – Don’t start next section on a new page if it leaves a large blank space on the previous page. At the end, zoom out and check for any large blank spaces

- [ ] Explain custom vessel fabrication challenges
	- What were the difficulties in the process?
	- How did you ensure that you could create multiple vessels consistently?
		- Ensuring consistency was challenging and demanded accurate measuring of silicone in grams, timing throughout the process, and finding the ideal draw speed (40 mm/min)
		- Once we figured out the rights amounts through experimentation, we recorded them and ensured to follow the same process each time
		- This ensured the properties were consistent and when we tested between vessels we confirmed that the results were reproducible
	- With the dip-coating method, wouldn’t the silicone collect more on one side due to gravity? How did you ensure the wall thickness on each side was the same?
		- Following the mixing and timing protocols I mentioned, we were able to reproduce vessels
		- We cut the cross-sections at middle and each end to compare and there were minimal thickness differences
		- This was acceptable naturally human arteries are not perfect straight tubes
	- Mention these difficulties and challenges, and how you overcame them. It sounds like a lot of work was put into this, but it doesn’t come across in the writing
---
## Chapter 7 – Arterial Stiffness Range
- No corrections! 🥳
---
## Chapter 8 – Bilateral Varying Flow

- [ ] Maybe take out correlation results on p180 if they do not match your previous findings and not as relevant
---
## Chapter 9 – Discussion
- No corrections! 🥳
---
