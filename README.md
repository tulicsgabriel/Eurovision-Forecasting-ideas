# How would you forecast the winner of the next Eurovision song contest? Here are a few ideas

Here, I'm playing around with Eurovision data from 1975 to 2009 to forcast the winner of 2010.

Ideas:

### Forecast Method 1 - Based on data_mean_crosstable -> treated as a weight matrix

This is a non-machine learning approach.

The idea is to use the data_mean_crosstable dataframe as a weight matrix, with the in with information on how many points on average each country gives to which country. This reflects voting preferences between countries, which depends on political and minority relations within countries. This weight matrix can be constructed using all data (1975-2009 period) or even over the past period (for example, the last 20 or 10 years). 

Ideally, it would be time to test this method to see which weight matrix constructed from the time window gives the most accurate estimate. As there is no time to do this, I will use the weight matrix for the whole period.

The algorithm is in steps:
- Select the list of countries that will be finalists in 2010
- for loop through the list of countries voted for
        - for loop through the list of voting countries
            - for a country, to collect all the votes (in a list) for a country in a dictionary
- sum up the average votes for a country
- select the country with the highest average vote -> this will be the winner

### Forecast Method 2 - Forcast every country vote for every country

The idea is to treat every vote from every country to every country as an individual dataset that needs forecasting. The advantage of this approach is that it's independent of every other aspect and only looks at how a country votes for a country in time.

Ideally, we would be able to select the best algorithm for this kind of task, and we could test it beforehand how it works on this kind of data. It's not clear what kind of forecasting algorithm is best for eurovision data.

Also note: normally, we would do a hypothesis test if the time series data is stationary or not.

The algorithm is in steps:
- Select the list of countries that will be finalists in 2010
- for loop through the list of countries voted for
        - for loop through the list of voting countries
        - reframe the data we analyze: not every country participates in every year, so there are missing point values, fill these years with 0
        - fit an Arima model on the data, forecast for 2010, store it in a dictionary 
- sum up the average votes for a country
- select the country with the highest average vote -> this will be the winner

### Forecast Method 3 - Based on sum of all points given to a country so far

The idea here is to use the information of the sum of point by every year to forecast. We fit a model for every country individually. Store the predicted score for 2010 into a dictionary and then get the country with the maximum predicted points.   


# Requirements

numpy==1.22.3
pandas==1.4.2
pmdarima==1.8.5
statsmodels==0.13.2

# Other

The code snippets in the Notebook are for brainstorming purposes, the methods have not been validated or evaluated. Measurements of the accuracy of the methods are still needed. This is a hobby project, consider it a hobby project. 

Please feel free to share opinions, comments and/or other ideas.

## License
[MIT](https://choosealicense.com/licenses/mit/)
