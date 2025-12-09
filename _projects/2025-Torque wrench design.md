---
layout: project
title: Torque Wrench design and Analysis
description: Ansys Analysis
technologies: [Autodesk Fusion]
image: /assets/images/torque_wrench_Normal_stress_close.png
---

For Mechanics of Materials I worked with a classmate, Alex Weng, to design and analyze a torque wrench. We were provided a list of design requirement including safety factors for yield, fatigue, and crack growth and a minumum strain along the direction of the handle at the strain gauge location for the rated torque of 600in-lbf. We start out by researching various materials that were typically used for torque wrenches and picked 7075-T6 Aluminum Alloy. Then, using MATLAB we created a code with the material and geometric properties of the torque wrench to calculate our safety factors and strain. After modifying some of the dimensions of he torque we successfully met the requirements

1. We used Fusion360 to CAD a model of the wrench with the dimensions shown in the images below:
![CAD image of torque wrench dimensions]({{ "/assets/images/torque_wrench_dim1.png" | relative_url }}){:width="600px"}
![CAD image of torque wrench dimensions]({{ "/assets/images/torque_wrench_dim2.png" | relative_url }}){:width="600px"}
![CAD image of torque wrench dimensions]({{ "/assets/images/torque_wrench_dim3.png" | relative_url }}){:width="600px"}
![CAD image of torque wrench dimensions]({{ "/assets/images/torque_wrench_dim4.png" | relative_url }}){:width="600px"}

2. The material we used for the torque wrench was 7075-T6 Aluminum Alloy. The elastic modulus of this material is around 10,000 ksi. This is significantly less stiff than steel, which allows the torque wrench to reach its required strain of 1.0 mV/V. The tensile strength is 67 ksi and the fatigue strength is 22ksi. This created a strength factor of safety of 6.3 and a fatigue factor of safety of 2.1. The 7075-T6 Aluminum Alloy also has a fracture toughness of 25,000 psi-sqrt(in), which gives a factor of safety for crack growth of 5.9.  

3. Then we put the model into Ansys. There is a fixed boundary condition at the drive. There is a 33.33 lbf load in the x-direction at the end of the handle (18 in. away from the drive) which corresponds to a 600 in-lbf torque at the drive. The diagram below shows the boundary and loading conditions.
![Image of Boundary and Loading Conitions]({{ "/assets/images/torque_wrench_BCs.png" | relative_url }}){:width="600px"}

4. We made a contour plot of normal strain in the strain gauge direction from FEM
![Image of Strain Contour Plot]({{ "/assets/images/torque_wrench_strain.png" | relative_url }}){:width="600px"}

5. We made a contour plot of the maximum principle stress from FEM
![Image of Principle Stresses Contour Plot]({{ "/assets/images/torque_wrench_principle_stress.png" | relative_url }}){:width="600px"}
![Image of Principle Stresses Contour Plot]({{ "/assets/images/torque_wrench_principle_stress2.png" | relative_url }}){:width="600px"}

6. This is a summary of the FEM results showing maximum normal stress (anywhere), load point deflection,  and strains at the strain gauge locations. The maximum normal stress on the torque wrench in the FEM is 27255 psi. However, this is at a stress concentration at the base of the drive. Along the torque wrench handle, the largest normal stress is 10581 psi. This is very close to our hand calculation, which was 10666.7 psi. 
The load point deflection in the FEM was 0.46186 inches. Our hand calculation load point deflection was 0.3072. These are on the same order of magnitude, but just like in the baseline design, the FEM had a higher deflection due to fillets along the handle in the CAD file. 
The strain at the strain gauge location was 1022.8 microstrain according to Ansys and 1007.4 microstrain according to our hand calculations. This is about a 1.5% percent difference, which is very small. 

![Image of Normal Stress]({{ "/assets/images/torque_wrench_Normal_far.png" | relative_url }}){:width="600px"}
![Image of Normal Stress]({{ "/assets/images/torque_wrench_Normal_stress_close.png" | relative_url }}){:width="600px"}
![Image of deflection plot]({{ "/assets/images/torque_wrench_principle_deflection.png" | relative_url }}){:width="600px"}
![Strain Gauge Image]({{ "/assets/images/torque_wrench_strain_gauge.png" | relative_url }}){:width="600px"}

7.We did calculations on torque wrench sensitivity in mV/V using strains from the FEM analysis.
ε<sub>1</sub> = 1022.8 microstrain<br>
    <i>change in gauge resistance</i> = k ε<sub>gauge</sub><br>
    <b>From half-bridge:</b>
    <sup>V<sub>out</sub></sup>/<sub>V<sub>in</sub></sub> = (k / 4)(ε<sub>1</sub> − ε<sub>2</sub>)<br>
    <b>With a gauge factor k = 2:</b>
    <sup>V<sub>out</sub></sup>/<sub>V<sub>in</sub></sub> = (2k / 4)(2ε<sub>1</sub>) = ε<sub>1</sub><br>
    Therefore the torque wrench sensitivity = <b>1.0228 mV/V</b>

8.We did research on the strain gauge to select. The Omega 1-LM11-1.5/350GE strain gauge fits our design. Its dimensions are 0.35 x 0.17 inches. It is a linear strain gauge measuring strain in one direction, so we can orient it along the handle to measure strain during bending. Also it has a gauge factor of about 2. Its maximum elongation is 10,000 microstrain, and our torque wrench has a max strain of a little over 1,000 microstrain, so this gauge is appropriate. 
