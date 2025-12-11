---
layout: project
title: Feedback Control in the Windkessel Model
description: System Dynamics project on feedback control of the Windkessel model
technologies: [MATLAB]
image: /assets/images/3260_heartbeat.png
---

Our group studied arteries near the heart as low pass filters. The heartbeat can be modeled as a frequency input, with arterial compliance and resistance mediating the ultimate output blood pressure. Though the heart moves blood in beats, the arteries manage to supply the body with a constant flow because of their ability to act as low pass filters. Throughout this study, we created open and closed loop models and studied disturbance rejection. Additionally, we researched the function of a 3 and 4 element Windkessel model, which add impedance and inertance as components of the system. 


Context: The Two-Element Windkessel Arterial Model

The human heart is a complex biological system that affects all other parts of the body in one way or another. Its primary function is to pump blood to the rest of the body, sustaining life and keeping the body up and running. For the purposes of this project, we have simplified the overall model of the heart, and focused on the windkessel effect. The windkessel effect is a mechanism within the heart and the major arteries that control and level out the flow of blood from a pumping heart to the rest of the body. As a heart beats, it sends unequal amounts of blood during diastole vs systole. In order to give the body a constant, equal stream of flow, the arteries will expand and contract themselves to act as a reservoir when the heart is pumping more blood out in systole, and push the stored blood out when the heart is filling in diastole. This phenomenon is shown in the two diagrams below. [1]
![Diagram showing the movement in arteries due to the windkessel effect[1]]({{ "/assets/images/3260_arteries.png" | relative_url }}){:width="600px"}
Figure 1: Diagram showing the movement in arteries due to the windkessel effect during diastole (a) and systole (b) [1]


In this way, the body receives a constant amount of blood flow no matter what the heart is doing. The effectiveness of the windkessel is relative to parameters, not exclusive to, but including compliance and resistance. Compliance deals with the elasticity of the arteries in the heart, determining how well they will expand, and therefore how much blood can be stored within them before being pushed out. Compliance will often decrease with things like aging, smoking, or even diabetes which means the heart has to work harder and will result in an increase of blood pressure. Resistance relates to how easily the blood flows through the arteries, affected by use of drugs such as nicotine and cocaine, as well as being increased by stress and anxiety which makes it harder for the heart to pump the required amount of blood to the rest of the body. Using resistance and compliance within the arteries creates a 2-element system that can be analyzed in various ways. The actual heartbeat can be considered an input to the system, which controls overall blood flow. For this simplified model, it can be thought of as a sinusoidal input.


Open Loop Arterial System TF

Modeling the windkessel as a 2-element open loop system allows for the heart to be analyzed as a first order linear system. With the windkessel acting as a low-pass filter, the mean flow will produce pressure that is proportional to the resistance R, while the high-frequency pulses of the heart will impact the compliance, C. Starting with the basics, the governing equation for this system can be found using the bases of the conservation of flow and the definitions of compliance and resistance: 

<b>Half-bridge output equation:</b><br>
<sup>V<sub>out</sub></sup>/<sub>V<sub>in</sub></sub> = (k / 4)(ε<sub>1</sub> − ε<sub>2</sub>)<br><br>

<b>For a symmetric pair of gauges (ε₂ = −ε₁):</b><br>
<sup>V<sub>out</sub></sup>/<sub>V<sub>in</sub></sub> = (k / 4)(ε<sub>1</sub> − (−ε<sub>1</sub>)) = (k / 4)(2ε<sub>1</sub>)<br><br>

<b>With gauge factor k = 2:</b><br>
<sup>V<sub>out</sub></sup>/<sub>V<sub>in</sub></sub> = (2 / 4)(2ε<sub>1</sub>) = ε<sub>1</sub><br><br>

<b>Torque wrench sensitivity:</b><br>
Sensitivity = ε<sub>1</sub> = 1.0228 mV/V

One important thing to notice with these equations is that the heart does not provide a steady flow. 
During diastole, the inflow becomes 0, meaning:<br>
Q<sub>in</sub> = 0<br><br>

Substituting this into the governing equation gives:<br>
dP/dt = −P / (R C)<br><br>

Solving the differential equation:<br>
P(t) = P<sub>0</sub> e<sup>−t/(RC)</sup><br><br>

This exponential decay shows how arterial compliance and resistance work together — the 
<b>Windkessel effect</b> — to maintain smooth blood flow to the body even though the heart pumps in discrete beats.<br><br>

To represent both systole and diastole, the system can be modeled with a sinusoidal inflow:<br>
Q<sub>in</sub>(t) = Q<sub>0</sub> + A sin(ωt)<br><br>

This models the changing inflow from the heart and results in the pressure waveform shown below.
![Graphical model showcasing pressure and flow altering with heartbeat modeled as a sinusoidal input]({{ "/assets/images/3260_heartbeat.png" | relative_url }}){:width="600px"}
Figure 2: Graphical model showcasing pressure and flow altering with heartbeat modeled as a sinusoidal input


The oscillations represent the heartbeat or pulse rate, and the flowrate is constant whereas the pressure is changing. The constant flow represents the heart beating, and the changing pressure shows the windkessel in effect, eventually reaching steady periodic oscillations, or the system’s steady state showcasing a working windkessel effect.


Closed Loop Arterial System, TF 

Modeling the heart as an open loop is helpful because it allows for a simple and easy to analyze system. That being said, it can also be worth studying the heart as a closed loop system, since in the real world there are many factors that cause the heart to behave more like a closed system than an open one. One clear way the heart acts as a closed loop is the fact that our blood is circulatory [8]. The blood that exists in the heart is pumped through our body and eventually makes its way back into the heart again. Because of this, the amount of blood available to enter the heart is directly related to the amount of blood the heart is pumping out. In other words, the output of the system feeds back into its own input, meaning the heart isn’t operating as a purely open system. This feedback makes the closed-loop perspective more realistic and sometimes more useful, depending on what aspect of the heart’s behavior you’re trying to understand. 
![Blow Flow in Human Circulatory System]({{ "/assets/images/3260_blood_flow.png" | relative_url }}){:width="600px"}


Another way that our hearts act as closed loops rather than open loops is through the baroreflex [9]. The baroreflex is a built-in reflex our body uses to make sure we always maintain the right blood pressure. It works through biological sensors that can detect how much the artery walls are stretching at any given moment. If an artery wall isn’t stretching as much as usual, that implies there’s less stress on the artery and therefore less blood pressure pushing it outward. When this happens, the baroreflex recognizes that more pressure is needed and sends signals to the heart to pump harder or faster to raise the pressure back to where it should be. Likewise, if the arteries are stretching too much, the reflex can ease the heart’s output to bring the pressure down. This feedback loop means the heart is constantly adjusting based on the system’s own output, which is a clear sign that it behaves much more like a closed-loop system than an open one.
![Arteries with Baroflex]({{ "/assets/images/3260_heart.png" | relative_url }}){:width="600px"}
For these physical reasons we can see that in many ways the heart acts as a closed loop, so we can now try to model one to study. 

Since we want the heart to maintain a sinusoidal beat, the reference inflow is:<br>
Q<sub>ref</sub>(t) = Q<sub>0</sub> + A sin(ωt)<br><br>

The error signal is the difference between the reference and the actual outflow:<br>
e(t) = Q<sub>ref</sub>(t) − Q<sub>out</sub>(t)<br><br>

The controller generates the input flow based on this error:<br>
Q<sub>in</sub>(t) = K e(t)<br><br>

Combining this with the Windkessel dynamics:<br>
dP/dt = Q<sub>in</sub>/C − P/(R C)<br>
Q<sub>out</sub>(t) = P(t) / R<br><br>

Substituting terms gives:<br>
dP/dt = K C Q<sub>ref</sub>(t) − P/(R C)(K + 1)<br><br>

Taking the Laplace transform (assuming zero initial conditions):<br>
s P(s) = K C Q<sub>ref</sub>(s) − (K + 1)/(R C) · P(s)<br><br>

Rearranging for the transfer function G:<br>
G<sub>P</sub>(s) = P(s) / Q<sub>ref</sub>(s) = K C / (s + (K + 1)/(R C))<br><br>

Multiplying by resistance gives the flow transfer function:<br>
G<sub>Q</sub>(s) = G<sub>P</sub>(s) · R = K R C / (s + (K + 1)/(R C))<br><br>

From this expression, the pole of the closed-loop system is:<br>
<b>−(K + 1) / (R C)</b>

This pole is useful to know for the heart because the magnitude of it represents the heart’s “response time.” A larger magnitude means the system reacts more quickly, so the arteries and the pressure in them will adjust faster when the heart starts beating harder or faster.
Another helpful aspect of the pole is the fact that it is negative. This tells us that our model is stable, which means that the blood pressure will go to a steady state instead of continuing to change a lot without control. This makes sense in terms of actual physiology, it would be unideal if our blood pressure had unstable changes and reactions any time our heart rate moves up or down.


Three and Four-Element Modeling

So far in this report, we have considered a 2-element Windkessel model, with compliance and resistance as the parameters. This kind of  model works well for lower frequencies and slower pressure decay, but becomes insufficient when there are steep pressure changes, higher frequencies in the flow, wave propagation, and wave reflection. This happens in systole, when the heart contracts and pumps blood to the arteries. Once ventricular pressure is higher than aortic pressure, the semilunar valves open and blood is ejected. Research done by the VU University Medical Center in Amsterdam identifies a 3-element model and a 4-element model, both geared to address this problem. The 3-element model adds a characteristic impedance, and the 4-element model adds an inertance related to the energy needed to accelerate blood through the arteries. Characteristic impedance equals wave speed times blood density divided by aortic cross-sectional area [2].
![Bode Plot showing 2, 3, 4 element models, measured impedance and phase [2]]({{ "/assets/images/3260_bode_plots.png" | relative_url }}){:width="600px"}
Figure 3: Bode Plot showing 2, 3, 4 element models, measured impedance and phase [2]


When wave propagation and inertance are accounted for, the accuracy of our model increases by a lot, especially during systole, because arteries are transmission lines, not reservoirs. Depending on the frequency, the area of study for impedance changes. At high frequencies, it is possible to understand the system with a small area of study, near the aorta. Lower frequencies require analysis further down the arterial tree. 
When the heart suddenly ejects blood, that blood must be accelerated, and mass resists acceleration. Just as adding in an RLC circuit, considering acceleration makes the closed loop system now second order.
When a pressure wave is created from the heart, that wave propagates through the tree and reflects at branch points. In order to model waves, you need mass and elasticity, which is what inertance and compliance work to do in this case. The two work as a form of spring-mass system, which means that the four-element model also enables us to capture a “natural frequency” of the arterial tree [6]. In humans, that natural frequency is much higher than the operating heart frequency, so blood will never hit a resonant flow. Physiologically, the damping effect of arterial resistance and the frequency mismatch of our heart rates mean that the waves can propagate smoothly through the system. Even though resonance does not occur, reflections still strongly influence the shape of the arterial pressure waveform.
Therefore, three and four-element Windkessel models are more representative of blood transmission in the arteries, but with that, the modeling becomes more complex.


Disturbance Rejection of Closed Loop System

Using the two-element closed loop model, disturbance rejection in the Windkessel model can be analyzed. Disturbance in this system can arise from changes in peripheral resistance such as vasoconstriction and posture changes [4] or from changes in compliance from stress, hypertension strikes, or some medications [5]. The effectiveness of the disturbance rejection depends on the controller K. If K is too small, the system will be overdamped and the settling time and rise time will be slow and the flow may never fully recover back to steady state.
If K is too large, the system will be overdamped and overshoot the steady state. The system will then oscillate back to steady state depending on the decay envelope. If K is significantly too large, the system will be unstable and oscillate with increasing amplitude after the disturbance.
K needs to be balanced in the middle so there is fast and stable recovery to steady state without much overshoot.
Using the closed-loop model:<br>
dP/dt = K C Q<sub>ref</sub>(t) − P(t)/(R C)(K + 1)<br><br>

With Q<sub>ref</sub>(t) = Q<sub>0</sub> + A sin(2t):<br>
dP/dt + P(t)/(R C)(K + 1) = K C Q<sub>ref</sub>(t)<br><br>

Therefore, the closed-loop time constant is:<br>
<b>τ<sub>CL</sub> = (R C)/(K + 1)</b><br><br>

This shows that as K increases, the closed-loop time constant decreases, which results in faster disturbance rejection. 
This matches the well-known statement that “the two-element Windkessel predicts that in diastole, when the aortic valve is 
closed, pressure will decay exponentially with a characteristic decay time R C.”<br><br>

<hr>

The disturbance transfer function helps explain how disturbances affect arterial pressure and outflow.  
The outflow with an added disturbance d(t) is modeled as:<br>
Q<sub>out</sub>(t) = P(t)/R + d(t)<br><br>

Using Windkessel dynamics:<br>
dP/dt = Q<sub>in</sub>/C − P/(R C)<br><br>

Taking the Laplace transform:<br>
Q<sub>in</sub>(s) = K(Q<sub>ref</sub>(s) − Q<sub>out</sub>(s)) 
= K(Q<sub>ref</sub>(s) − P(s)/R − D(s))<br><br>

C s P(s) = Q<sub>in</sub>(s) − P(s)/R<br><br>

Substituting:<br>
C s P(s) = K Q<sub>ref</sub>(s) − K R P(s) − K D(s) − (1/R)P(s)<br><br>

Collecting terms:<br>
(C s + (K + 1)/R) P(s) = K Q<sub>ref</sub>(s) − K D(s)<br><br>

Thus:<br>
P(s) = [K / (C s + (K + 1)/R)] Q<sub>ref</sub>(s) − [K / (C s + (K + 1)/R)] D(s)<br><br>

Pressure disturbance transfer function:<br>
<b>G<sub>pressure</sub>(s) = P(s)/D(s) = − K / (C s + (K + 1)/R)</b><br><br>

<hr>

To find the outflow disturbance transfer function:<br>
Q<sub>out</sub>(t) = P(t)/R + d(t)<br>
Q<sub>out</sub>(s) = P(s)/R + D(s)<br><br>

Substituting P(s):<br>
Q<sub>out</sub>(s) = [1/R] · [−K/(C s + (K + 1)/R)] D(s) + D(s)<br><br>

Simplifying:<br>
Q<sub>out</sub>(s) = (1 − K R / (C s + (K + 1)/R)) D(s)<br><br>

Final flow disturbance transfer function:<br>
<b>G<sub>flow</sub>(s) = Q<sub>out</sub>(s)/D(s) = (C R s + 1)/(C R s + (K + 1))</b>

From the transfer functions describing output pressure and output flow in response to a disturbance, 
long-lasting disturbances — such as step inputs or slow changes in posture — correspond to the 
low-frequency limit where s → 0. In this case, the system response becomes:<br><br>

<b>Response = 1 / (K + 1)</b><br><br>

This shows that as K increases, the value of 1/(K + 1) decreases, meaning the effect of low-frequency 
disturbances is reduced. Therefore, increasing K directly improves disturbance rejection for 
slow or low-frequency disturbances.

Disturbances caused by rapid oscillations correlate to when s approaches infinity. And the controller in the system responds by 1. This shows the controller for the two-element system cannot suppress fast changing disturbances. This makes sense because the Windkessel is a lumped model because it describes the whole arterial system model, so “is not suitable for the assessment of spatially distributed phenomena and aspect of wave travel” [2]. It is a first-order low pass system, so high frequency disturbances that change rapidly like sudden fluctuations in heartbeat from pressure strikes and mechanical vibrations from noise in medical devices can not be modeled [3].


![Effect of controller gain K on disturbance rejection for both high and low frequency disturbance in the two-element, closed-loop Windkessel model [graphs generated using code from ChatGPT]]({{ "/assets/images/3260_disturbance.png" | relative_url }}){:width="600px"}
Figure 4: Effect of controller gain K on disturbance rejection for both high and low frequency disturbance in the two-element, closed-loop Windkessel model [graphs generated using code from ChatGPT]

From the graphs it is clear that the controller gain has significant impacts on the response for low-frequency disturbances, but little impact for high-frequency disturbances. For low frequency increasing K improves the disturbance rejection and the output stays closer to the reference while recovering faster. For high frequency disturbances, the disturbance passes through the system largely unaffected by the controller gain K. This once again demonstrates that the Windkessel model functions as a first-order low-pass system that is unstable to reject rapid oscillations.

Conclusion
We used the Windkessel model to analyze how the arterial system can be represented in both open and closed-loop configurations. The two-element Windkessel model, which incorporates arterial compliance and resistance, effectively illustrates how arteries act as low-pass filters that convert the heart’s pulsatile output into a steadier blood flow. Through transfer function analysis, we showed that the open-loop system behaves as a first-order system, while the closed-loop model more realistically captures feedback mechanisms such as the baroreflex.
Expanding the analysis to three-element and four-element models revealed limitations of the simpler two-element approach, especially during systole, when wave propagation and inertance play a significant role in the system’s accuracy. Disturbance rejection analysis of the two-element closed-loop system further highlighted these limitations because a first-order low-pass filter cannot effectively suppress high-frequency disturbances, which pass through the system largely unchanged. This analysis also demonstrated how the controller gain K influences the system’s sensitivity to disturbances.
Overall, by applying concepts such as transfer functions, frequency response, and open versus closed-loop behavior, our work shows how different Windkessel models provide insight into the arterial system. While simpler models capture the essential low-pass filtering characteristics, more complex models are required to accurately represent the frequency-dependent behavior of blood flow and pressure.

References

Journal Articles:

[1]	Kiuchi, Shunsuke & Hisatake, Shinji & Dobashi, Shintaro & Murakami, Yoshiki & Ikeda, Takanori. (2024). Role of Vascular Function in the Prognosis of Heart Failure Patients. Journal of Clinical Medicine. 13. 2719. 10.3390/jcm13092719. https://www.researchgate.net/publication/380384616_Role_of_Vascular_Function_in_the_Prognosis_of_Heart_Failure_Patients 


[2]	Westerhof, N., Lankhaar, JW. & Westerhof, B.E. The arterial Windkessel. Med Biol Eng Comput 47, 131–141 (2009). https://doi.org/10.1007/s11517-008-0359-2	


[3]  	Zhou, S., Xu, L., Hao, L. et al. A review on low-dimensional physics-based models of systemic arteries: application to estimation of central aortic pressure. BioMed Eng OnLine 18, 41 (2019). https://doi.org/10.1186/s12938-019-0660-3 


[4] 	Matthew A. Boegehold, Chapter 15 - Vascular Remodeling and Rarefaction in Hypertension,
Editor(s): Gregory Y.H. Lip, John E. Hall, Comprehensive Hypertension, Mosby, 157-166 (2007) https://doi.org/10.1016/B978-0-323-03961-1.50018-0  


[5] 	Simon AC, Levenson J, Chau NP, Pithois-Merli I. Role of arterial compliance in the physiopharmacological approach to human hypertension. J Cardiovasc Pharmacol. 1992;19 Suppl 5:S11-20. PMID: 1381785. https://pubmed.ncbi.nlm.nih.gov/1381785/ 


[6]	    Benkirane, S., Lam, S., Liu, A., Nguyen, L., & Sujan, N. (n.d.). 2- and 3-element Windkessel model analysis: The arterial system and its response to vasoactive drug impact. Department of Bioengineering, University of San Diego. https://isn.ucsd.edu/courses/beng122a/project/2023/reports/SB_SL_AL_LN_NS.pdf 


[7]     Behnam, V., Rong, J., Larson, M. G., Gotal, J. D., Benjamin, E. J., Hamburg, N. M., Vasan, R. S., & Mitchell, G. F. (2019). Waveform parameters derived from pressure-only Windkessel models are related to cardiovascular disease risk and could be useful for understanding arterial system function. Journal of the American Heart Association, 8(14), e012300 https://www.ahajournals.org/doi/10.1161/JAHA.119.012300 

Websites

[8]	    Cleveland Clinic, Circulatory System, 2024
https://my.clevelandclinic.org/health/body/circulatory-and-cardiovascular-system

[9]	    Cleveland Clinic, Baroreceptor Reflex, 2022 https://my.clevelandclinic.org/health/body/24556-baroreceptor-reflex


