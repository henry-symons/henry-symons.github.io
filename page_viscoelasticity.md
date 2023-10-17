## Automating viscoelastic indentation analysis

**Project description:** Mechanical properties of viscoelastic materials (which show both solid and liquid properties) are usually measured in large bulk samples.
Using indentation measurements (where a probe scans across the surface making many measurements) instead allows us to see how these properties vary across the surface of a material. 
However, data analysis for this technique is challenging and time-consuming as mapping mechanical properties involves many individual measurements.

In this project, I create a Python-based application to automate this process, and enable rapid analysis of indentation data.

### 1. Contact point determination

Individual indentation curves show the force required to compress a probe a specified distance into a material. One of the key challenges in analysing this type of data is accurately identifying the contact point - the transition between a linear baseline region where sample and probe are not touching, and a curved indentation region where the probe is in contact with the sample. The procedure is made more challenging by noise in the raw data, and the variable nature of the baseline region which may be flat or sloped.

We develop a 2-step method to achieve a compromise of accuracy and computational resources, in order to enable batch processing of thousands of indentation curves in a reasonable timescale.

Step 1. Approximation of contact point:

<img src="images/viscoelasticity/CP_approx.png?raw=true"/>

In this plot, we determine the contact point initially as the maximum in the 2nd derivative of force vs probe displacement (i.e. the point at which curvature is greatest). As data are typically noisy, data are smoothed by applying a Savitsky-Golay filter. However, the downside of this smoothing process is a loss of accuracy in the contact point.

Step 2. Optimisation: 

<img src="images/viscoelasticity/CP_precise.png?raw=true"/>

Using the estimated contact point, we then apply a piecewise fitting process to the raw (unfiltered) data to a linear region, and an exponential section. The transition between regimes is used as a fitting parameter, taking the approximate contact point as the initial value, and it's optimised value represents a more precise contact point.
This optimisation process utilises the [Symfit](https://symfit.readthedocs.io/en/stable/index.html#) module to carry out the piecewise fitting. Although this could be directly applied to the raw data, the initial approximation step saves a considerable amount of computation time, and gives more reliable results.

Finally, we can use the contact point to convert our raw data to modulus values, based on the indentation depth at maximum force:

<img src="images/viscoelasticity/depth.png?raw=true"/>

This calculation uses the [Hertz contact mechanics model](https://en.wikipedia.org/wiki/Contact_mechanics).


### 2. Fitting individual curves

To extract useful mechanical properties from the data, the time-dependent modulus from each measurement are fitted to a 3-term Prony series representing the [Generalised Maxwell Model](https://en.wikipedia.org/wiki/Generalized_Maxwell_model). 

<img src="images/viscoelasticity/fitting.png?raw=true"/>

This fitting yields a series of three characteristic decay times, and more importantly, corresponding modulus values for each indentation measurement made.


### 3. Visualising mechanical properties

By using a dataset containing a grid of indentation measurements, we are able to automate the batch analysis of all measurements to yield a map of various mechanical properties across the surface of a material:

<img src="images/viscoelasticity/3d.png?raw=true"/>

This kind of plot shows mechanical heterogeneity on the microscale - an important feature to understand for many applications of viscoelastic materials, particularly those involving interfacing with biological systems.


The same data may be further processed by applying a Fourier transform, to convert a time-dependent response to it's corresponding frequency domain:

<img src="images/viscoelasticity/fourier.png?raw=true"/>

In this plot we can see the expected response of the material across a broad range of frequencies, with the error bands corresponding to the standard deviation in moduli across the surface of the material. These values are useful for assessing the behaviour of a material subjected to stresses of varying frequencies, and can also be directly compared to values generated from typical viscoelastic measurement techniques.


### 4. Conclusions

Overall, the procedure outlined here is a reliable method to automate the complex analysis process for viscoelastic indentation measurements. This technique can rapidly provide a wide range of useful properties, and their distribution across a material. Furthermore, the complete code provides a graphic user interface, allowing this process to be carried out without programming knowledge.

Underlying code for this analysis process is not currently available but will be added to GitHub upon publication of the corresponding scientific study. However, a related project for purely elastic materials was published in 2022 and can be viewed [here](https://pubs.rsc.org/en/content/articlehtml/2022/sm/d2sm00857b).
