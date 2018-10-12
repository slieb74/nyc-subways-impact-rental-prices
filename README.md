# Predicting NYC Rental Prices Based on Proximity and Access to Subways

## Goal
Measuring the impact proximity to subway stations has on rental prices in Manhattan and Brooklyn, and how future station openings and/or closures will impact neighborhood prices.

## ETL
We gathered data from four sources:
  - Location data for station entrances and line access from MTA's API
  - Apartment sales from the NYC Department of Finance
  - Median neighborhood rental prices and sale-to-rent ratios from Zillow
  - Apartment coordinates from GoogleMaps API

- Our apartment data consisted of sales instead of rentals, so we used the median neighborhood rental prices from Zillow to convert the apartment sale prices into a rent estimate that better suited our goal. We wanted to focus on rentals instead of sales because it is less static of a market and would therefore see a greater impact from changes in subway access.

- In order to get the distance from each apartment to the subway entrance, we used GoogleMaps API to convert addresses into coordinates, from which we could calculate the distance in miles using the Haversine formula.
- From there, we found for each apartment every station with unique subway access within 0.55 miles of the apartment (roughly a 10-minute walk)

## Mapping using GeoPandas
To get a sense of where our apartments were located, and to ensure that we were not focusing on a few neighborhoods, we used GeoPandas to map each neighborhood, apartment, and subway line. 

###### Each apartment plotted in its neighborhood using GeoPandas
<p align="center">
  <img src="https://github.com/slieb74/nyc-subways-impact-rental-prices/blob/master/images/Aparmtent%20sales%20.png" height="550" width="525"> 
</p>

###### Each subway station entrance plotted in using GeoPandas
<p align="center">
  <img src="https://github.com/slieb74/nyc-subways-impact-rental-prices/blob/master/images/Subway%20%20map.png" height="475" width="450">
</p>

## Machine Learning Models
We used 4 different classification models to predict whether an apartment's rental price would be above or below its neighborhood median, given its access and proximity to different lines. 

The four models we used were:
  - Logistic Regression
  - Random Forest
  - Gradient Boosting
  - AdaBoost
  
The best performing model was the Random Forest Classifier, which had an Accuracy of 74.52% and AUC of 81.57%.

###### Results
<img src="https://github.com/slieb74/nyc-subways-impact-rental-prices/blob/master/images/Screen%20Shot%202018-10-09%20at%201.59.45%20PM.png" height="100" width="150">

###### Confusion Matrix
<img src="https://github.com/slieb74/nyc-subways-impact-rental-prices/blob/master/images/Screen%20Shot%202018-10-09%20at%201.59.37%20PM.png" height="350" width="350"> 

###### ROC Curve
<p align="center">
  <img src="https://github.com/slieb74/nyc-subways-impact-rental-prices/blob/master/images/Screen%20Shot%202018-10-09%20at%202.01.24%20PM.png" height="450" width="550">
</p>

## Next Steps
Due to time constraints, we had to limit the scope of our project to Manhattan and Brooklyn, but in the future, I would love to explore both the Bronx and Queens as well. In addition, I want to try to predict how the upcoming L Train shutdown will affect rental prices in Williamsburg. I think it would also be great to add Citibike data to our project and measure the impact dock openings have had on rental prices. 
