Data has been sourced from Kaggle. We have data related to fatal road accidents from 1989 to 2021. Rainfall data is data collected from BOM weather stations between 2007 to 2017.

My Jupyter notebook was initialised and had pandas, matplotlib.pyplot and scipy.stats libraries imported as to manipulate and visualise the dataset.

Prior to loading the "weatherAUS.csv" file into the notebook, I went through and manually changed each location from the Suburb it was represented as to it's corresponding State, I was unable to find an appropriate way in Python to do this within the allotted time.

The weather_df dataframe was then cut down to include just the Date, Location and Rainfall data and renamed as rainfall_df, as this is the data that we were concerned with.
As the date was written in a full Day/Month/Year format, I ran a splitting function to have each value ("Day","Month" and "Year") stored separately, the Month and Year were then recombined, as the Day of which the rainfall occurred was not relevant to the analysis we were going to perform.
After running a .count() function, you can notice that Date and Location have more rows than Rainfall, so I ran a .dropna() function and each column then returned the same number of values.
The DataFrame was then grouped by Date and the Rainfall was summed as the output to a new DataFrame.

As this data is numeric in nature, I wanted to ensure there were no outliers present (using the 1.5*IQR rule), so the .describe() function was run to find the 1st and 3rd quartile.
After finding the upper (6413.2mm) and lower (-430.8mm) bounds of the data, a bovplot was created to visualise any outliers, of which there was one.
This one value was dropped by creating a .loc() filter that checked that each value was less than the upper boundary.

Next we imported the accident data as crash_df. As the Date for the accidents is split into Month and Year already, we needed to concatenate them. However before this we needed to ensure that the date will match the Rainfall Date data we already were working with. To do that, we needed to map a 2 digit format to the Month column.
The data was then grouped by Date and each row was counted, as to find the amount of Fatal Accidents present in the dataset, and stored into a new DataFrame.
Similar to the Rainfall data, I ran an outlier check on the data, visualised with a boxplot and dropped any months that were outside the range.

Next our two final DataFrames were merged on their "Date" columns, to create a set for us to complete analysis on.
We performed the linear regression function (stats.lingress()) on the relationship between Number of Fatal Accidents and mm of Rainfall and the correlation coefficient was found to be -0.31.
The linear regression line and equation was plotted on a graph then a scatterplot showing the relationship between Number of Fatal Accidents and mm of Rainfall was also plotted on the same graph.
The table was finally tidied up with a title, and labels for the x and y axis.

With a correlation coefficient of -0.31, the results display a weak negative correlation between the Total Rainfall in the month and the Number of Fatal Road Accidents.
We can therefore concluded that the rate of fatal road accidents slightly decreases as rainfall increases.
This may be due to road users taking more care in wet conditions.
