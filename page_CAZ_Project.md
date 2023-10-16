## Investigating the effectiveness of the CAZ at improving air quality in Bristol

**Project description:** Bristol City Council introduced a clean air zone (CAZ), where certain types of vehicles were charged a daily fee to enter a specified area around the city centre, in November 2022 to attempt to meet government guidance on air quality.

In this project I investigate the success of this scheme in achieving these aims.

To quantify air quality, we examine the concentration of NO2 from momnitoring sites across Bristol in data made publicly available by Bristol City Council. As a guideline, government policy states that the annual mean concentration cannot legally exceed 40 μg/m3.

### 1. Temporal trends in NO2 concentration

For this project, we examine two air quality datasets; one with data from 18 locations but spanning 1993 until present with high time resolution (continuous dataset), and one with yearly mean NO2 concentrations between 2010 and 2022 from 351 locations, collected using diffusion tubes (diffusion tubes dataset).

Firstly, we examine the decreasing long-term trend in NO2 concentration, and validate that the smaller subset of locations reflects the overall trend in NO2 levels:
<img src="images/CAZ/longterm_no2_trends.png?raw=true"/>

We can further investigate temporal trends over shorter time periods within the continuous air quality dataset:
<img src="images/CAZ/longterm_no2_trends.png?raw=true"/>

Here we can see several periodic trends in NO2 concentrations:
Firstly, we see a pretty substantial seasonal effect with levels highest during winter, but decreasing by approximately a quarter during the summer months. This behaviour is well documented and could indicate both a change in use (e.g. more heating or engine idling during colder months) and a seasonal difference in the pollutant lifetimes (which are shortest during summer months).
Secondly, we see a clear pattern associated with typical vehicle usage - a gradual build up during consecutive weekdays, with a substantial drop on weekends.
Looking on a shorter timescale, mean hourly concentrations peak at over 50 µg/m3 between 8-9 am and 5-6 pm, strongly coinciding with typical commuting times. Notably, overnight NO2 levels decrease to less than half the daytime maxima, showing the relatively short lifetime of this pollutant.


### 2. Spatial mapping of NO2 concentrations

To map the spatial distribution of NO2 levels, we introduce a third dataset containing coordinates of air quality measurement sites in Bristol, along with a polygon covering the coordinates of the CAZ. We firstly determine which locations lie within this region, and which belong to each dataset studied:
{% include no2_historic_bristol.html %}

This enables the plotting of mean NO2 concentrations at each location by year of the dataset:
{% include no2_historic_bristol.html %}

We can further extend this analysis to the diffusion tube dataset for a more complete picture of NO2 levels since 2010 (however this data does not currently span past 2022 so is not useful for quantifying the effects of the CAZ):
{% include no2_historic_bristol.html %}

Broadly speaking, we can see NO2 concentrations have decreased year-on-year, however in several locations around the city centre they remain above the 40 μg/m3 limit.


### 3. Quantifying the effectiveness of the CAZ

<img src="images/dummy_thumbnail.jpg?raw=true"/>

### 4. Conclusions

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
