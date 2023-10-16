## Investigating the effectiveness of the CAZ at improving air quality in Bristol

**Project description:** Bristol City Council introduced a clean air zone (CAZ), where certain types of vehicles were charged a daily fee to enter a specified area around the city centre, in November 2022 to attempt to meet government guidance on air quality.

In this project I investigate the success of this scheme in achieving these aims.

To quantify air quality, we examine the concentration of NO2 from momnitoring sites across Bristol in data made publicly available by Bristol City Council. As a guideline, government policy states that the annual mean concentration cannot legally exceed 40 μg/m3.

### 1. Temporal trends in NO2 concentration

For this project, we examine two air quality datasets; one with data from 18 locations but spanning 1993 until present with high time resolution (continuous dataset), and one with yearly mean NO2 concentrations between 2010 and 2022 from 351 locations, collected using diffusion tubes (diffusion tubes dataset).

Firstly, we examine the decreasing long-term trend in NO2 concentration, and validate that the smaller subset of locations (continuous dataset) reflects the overall trend in NO2 levels in the larger set of locations (diffusion tubes dataset):
<img src="images/CAZ/longterm_no2_trends.png?raw=true"/>

We can further investigate temporal trends over shorter time periods within the continuous air quality dataset:
<img src="images/CAZ/periodic_no2_trends.png?raw=true"/>

Here we can see several periodic trends in NO2 concentrations:
Firstly, we see a substantial seasonal effect with levels highest during winter, but decreasing by approximately a quarter during the summer months. This behaviour is well documented and could indicate both a change in use (e.g. more heating or engine idling during colder months) and a seasonal difference in the pollutant lifetimes (which are shortest during summer months).
Secondly, we see a clear pattern associated with typical vehicle usage - a gradual build up during consecutive weekdays, with a substantial drop on weekends.
Looking on a shorter timescale, mean hourly concentrations peak at over 50 µg/m3 between 8-9 am and 5-6 pm, strongly coinciding with typical commuting times. Notably, overnight NO2 levels decrease to less than half the daytime maxima, showing the relatively short lifetime of this pollutant.


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
