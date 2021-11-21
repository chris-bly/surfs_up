# surfs_up

## Challenge Overview
Aloha! In this module we have utilized Python (via Jupyter Notebook and VS Code), SQLAlchemy, and Flask to analyse and visualize meteoroliogical data from around the island of Oahu, Hawaii. We have done so to perform analyses to help understand the viability of giving up life in the Lower 48 and opening a surf shack/ice cream stand in paradise. We need to know if the weather will sustain business year-round to define the potential of this business endeavour.

Currently the weather data is stored in a SQLite database as a flat file, the befit of which is that the entire dataset can be stored locally. By developing a summary of the temperature data in both June and December, we can observe the hottest and coolest months to see if they match well with the consumption of ice cream and the catching of the gnarliest waves to make the most informed decisions possible.

## Results
### June Temperature Statistical Summary
![June Temperature Data](resources/June_tobs.png)

### December Temperature Statistical Summary
![December Temperature Data](resources/December_tobs.png)

The above images present the observed temperature data in Oahu for the months of June and December from 2010-2017, respectively. From the above data, we can see the following:
- The average temperature in June is 74.9 degrees fahrenheit and the average temperature in December is 71.0 degrees fahrenheit, nearly 4 degrees cooler.
- The maximum temperature observed in June was 85 degrees vs. 83 degrees in December. So, even if the days are cooler on average in December the peak temperatures remain similar in both months. The higher standard deviation observed in the December temperatures also indicates the greater variance in temperatures when compared to June.
- Most important to the ice cream business, a look at the mimimum observed temperatures indicates an obversved gap of 8 degrees between June (64 degrees) and December (56 degrees). This, coupled with the lower quartile data showing that 25% of days only reach 69 degrees in December vs. 73 degrees in June indicate that there are certainly going to be days where ice cream isn't a highly sought-after treat. It may be a good idea to ensure the surf shack has a well-stocked inventory of wetsuits and cooler weather surfing accessories as well.

## Summary
In summary, though the temperatures are a bit lower and more variable in December than they are in June, there should still be ample days to move volume in both the dairy and surfboard rentral markets. 

- Additional analysis that could be performed to bolster the decision-making would be to calculate the number of days in both June and December with precipitation. Days with precipitation above a certain threshold could possibly be detrimental to business.
```
results = session.query(Measurement.date, Measurement.prcp).filter(extract('month', Measurement.date) == 6).all()
dec_results = session.query(Measurement.date, Measurement.prcp).filter(extract('month', Measurement.date) == 12).all()
```
- Furthermore, some visual representation of the data that expands upon the number of days with preciptiation would be helpful to describe the days where business may be, ahem, _dampened_ by the presence of rain. 
```
# Save the query results as a Pandas DataFrame and set the index to the date column
precip_df = pd.DataFrame(results, columns=['date','precipitation'])
precip_df.set_index(df['date'], inplace=True)

# Sort the dataframe by date
precip_df = df.sort_index()
# Use Pandas Plotting with Matplotlib to plot the data
precip_df.plot()
```
- Finally, visualization could be applied to the temperature dataframe as well for each month presented as a histogram to better understand the distribution of temperatures as they apply to optimal ice cream/surfing weather.
```
temps_df.plot.hist(bins=12)
plt.tight_layout()
```
