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
This optimisation process utlises the [Symfit](https://symfit.readthedocs.io/en/stable/index.html#) module to carry out the fitting. Although this could be directly applied to the raw data, the initial approximation step saves a considerable amount of computation time, and gives more reliable results.

Finally, we can use the contact point to convert our raw data to modulus values, based on the maximum indentation depth:
<img src="images/viscoelasticity/depth.png?raw=true"/>

This calculation uses the [Hertz contact mechanics model](https://en.wikipedia.org/wiki/Contact_mechanics).


### 2. Spatial mapping of NO2 concentrations

To map the spatial distribution of NO2 levels, we introduce a third dataset containing coordinates of air quality measurement sites in Bristol, along with a polygon covering the coordinates of the CAZ. We firstly determine which locations lie within this region, and which belong to each dataset studied:
{% include measurement_sites_bristol.html %}


This enables the plotting of mean NO2 concentrations at each location by year of the dataset:
{% include no2_historic_bristol.html %}


We can further extend this analysis to the diffusion tube dataset for a more complete picture of NO2 levels since 2010 (however this data does not currently span past 2022 so is not useful for quantifying the effects of the CAZ):
{% include no2_diffusion_bristol.html %}


Broadly speaking, we can see NO2 concentrations have decreased year-on-year, however in several locations around the city centre they remain above the 40 μg/m3 limit.


### 3. Quantifying the effects of the CAZ

To quantify the effects of the CAZ, we consider data from 1 year prior to the introduction of the scheme onwards. Here the number and locations of measurement sites are consistent, and the influence of other factors (e.g. the effects of intermittent COVID-19 measures during 2020 and 2021) should be minimal.

Firstly, we examine a times-series of weekly-average NO2 concentrations, either averaged across all measurement sites, or plotted individually:

<img src="images/CAZ/timeseries.png?raw=true"/>

Looking at the averaged data, weekly concentrations fluctuate significantly making longer-term changes unclear, however, there appears to be slight long-term decrease in NO2 after the introduction of the CAZ. Looking at individual sites, we see that most remain unchanged, however, one site within the CAZ (site ID 501) shows a substantial decrease in NO2 measured after the scheme is introduced.

To see these changes more clearly, mean NO2 concentrations are plotted before and after the introduction of the CAZ for each site:

<img src="images/CAZ/barplot.png?raw=true"/>

In this plot we can clearly see that all locations within the CAZ have experienced a reduction in mean NO2 concentration, when compared with the year prior to its introduction. In particular, the site with highest NO2 concentrations (site ID 501) has shown a substantial drop and is now close to the target level of 40 µg/m3.

One final check in this exploratory analysis is to confirm that differences are not simply a result of seasonal variation in NO2, as a full year has not yet passed since the introduction of the CAZ.

<img src="images/CAZ/caz_bymonth.png?raw=true"/>

In these plots, we compare NO2 concentrations by month, averaged over sites either inside or outside the CAZ. We see that for almost all months, sites inside the CAZ have experienced a substantial decrease in NO2 concentration compared with the same months before the CAZ introduction.


### 4. Conclusions

Overall, this preliminary analysis appears to indicate that the introduction of the CAZ has been successful in improving air quality around Bristol city centre. All measurement locations within the CAZ have recorded lower NO2 concentrations since the introduction of the scheme. Significantly, the site with the highest concentration the year prior to CAZ introduction (around 64 μg/m3) has since recorded a number much closer to the legal limit (around 47 μg/m3). The observed decreases do no appear to be a result of seasonal changes in NO2 concentrations.

A more comprehensive dataset with a greater number of measurement sites, and additional time passing since the introduction of the scheme will enable more extensive analysis of the effects of the CAZ. For example, an updated diffusion tube dataset containing data for 2023 should allow further insight and quantification of the changes seen.

For more details see [GitHub Project](https://guides.github.com/features/mastering-markdown/).

