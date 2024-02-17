Project Description: The goal of our project is to analyze what characteristics are prominent within samples of the LAPD RIPA database from data.lacity.org. This includes race, gender, perceived age, and what type of stops are made. We utilize stratified random sampling to sample the database and utilize K-Means Clustering and KNN Regression.



Stratified Data Sampling: In our data we needed to perform a sampling method and decided to use stratified sampling. Had to take the Stop_Year column and copy it to a new column. Used a split and slice to parse and set the column to only have the year. Then used the groupby function on the Stop_Year with sampling 4000 per year. 2023 was a year with a low frequency of entries so that year was not included. Used the 1.3 gb approx file and the commented data below to sample from it. 
![stratified sampling!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/40bd9e9e87d858a8030e97c9425dd513af19c06c/images/clean.png)



Data Cleaning:
In order for data to be used within our project, we performed cleaning methods before we proceed to use analysis methods. After we initialize the data, we proceed to convert (yes,no) categories within the data into numerical (0,1) so that we can include it within our functions during analysis. After deciding what columns would be most beneficial to our analysis, we remove the unused columns by using the drop functions in Pandas and rewrite them to the CSV file. This makes it easier for us to analyze and helps by removing large amounts of data that creates issues when trying to view the data.
![data clean!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/README.md#L12)

![race encoding!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/races_numerical.png)

![race encoding2!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/encoding.png)

K-Means:
Using the cleaned data, we can identify clusters within our columns of data to see if there are any relationships or  groups that havent been labeled yet.
For this data we want to look at the data from the ‘Area ID’ and ‘Stop Time’ to identify any groups within the area of arrest or stoppage and the time.
We first convert the Area ID from the included str into an integer before we start to implement, and replace 99 with 22 for more data fluency. 
Similarly, we convert the Stop time by converting the values from STR to INT, we split the values from the middle colon that is in between it. We split the values into a right and left, converting the left into an integer and the right side as a float. To use this data, we then combine both the right and left into the new “Kmeans_Data [‘Stop Time’]” that we will use for this analysis.

To find the most optimal K for the data, we must perform the elbow method. We set our x as Area ID and y as Stop Time and we use the Zip function to map the values so we can use them to create the elbow. Using a for loop, the cluster gets fitted into the data and we append the inertia value into the empty array we created. This for loop iterates for 11 K’s and we plot the inertia for all the K’s to get our elbow method graph.
From the graph, we analyze and find the inflection point to get the optimal K. In this case we choose K=3. We perform K means using the K means function and setting to 3 clusters and we fit the Kmeans variable into the data. After this is done, both the scatter plot with the Kmeans labels is printed and we also print the regular scatterplot with from the sata to show a comparison of both graphs for better understanding.
![kmeans!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/7cf8bb18b12376e2f3a8b1b6c719c9bda175adc3/images/kmeans_data_plot.png)

![kmeans2!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/7cf8bb18b12376e2f3a8b1b6c719c9bda175adc3/README.md#L28)

From the data (with ‘Area ID’ on the x bar and ‘Stop Time’ on the y bar), we can see that stops are happening at regular intervals throughout the entire day.

KNN with Regressor Analysis:
Before starting the KNN Regressor function we must clean the data and convert it as floats. This will make the data columns usable for the following functions since the included data is given as STR and will not work. For other values we also must turn categorical values into numerical values, we grab the perceived Gender and replace the terms with numbers from 0-4.

We can use the elbow method to find a good K for the KNN regressor. We must use the X and Y train values and for them to be a temporary model. We can then predict, using the temporary model from Xtest. After this we can also calculate MSE in the for loop to see which resulting K is better.
![knn regression1!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/elbow_code.png)
![knn regression2!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/elbow_knn.png)

Asian (1), Black/African American (2), Hispanic/Latino(a) (3), Middle Eastern or South Asian (4), Native American (5), Pacific Islander (6), White (7)


After we determined the K which is N_Neighbors= 3, then we use that to define the grid of feature values. This graph shows the relationship between Race and Age, the 3, 7 are the most group that are stopped. We think that because they have the most population in U.S.
![plot_race_age!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/plot_race_age.png)

For the following graph. Female(0), Male(1), Transgender woman/girl(2), Transgender man/boy(3), Nonconforming(4).

Do the same thing as above with N_Neighbors= 3, then we define the grid of feature values with Gender vs. Age. Female and Male are the majority to be stopped.
![plot_gender_age!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/plot_age&gender.png)

Using the graph we can visualize the KNN regressor function for Perceived Gender and the Perceived age. We see that for 0-Female, the perceived age was around 35. 1-Male= 42, 2-Trans woman = 35, Trans Man = 40, 04-Non Conforming =40.

Extra KNN:
![extra knn!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/mse_graph.png)
![plot_area_race!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/plot_area&race.png)

We then do a extra KNN for Race vs. Area ID:
We are replacing the AGE with Area ID, then compare it with Race. For that, we are going to calculate the new MSE and make a new elbow graph.
Now we visualize relationship between Race and Area ID. 
As the graph shown above, we know of four areas where the largest number of people are stopped.
There are: Area ID: 10(West Valley),11(North East),12(77th street),13(Newton) 
![cmap!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/cmap.png)

Finally, we visualize the relationship between Race and Gender determined by AGE by scatter plot. Also, use different colors to indicate how many of these dots have the same or close color according to the Perceived AGE. In this case, The same or similar color means people were stopped for the same/similar reason or feature.

EDA:
From this Data, we had 3 Questions:
    1. What are the characteristics of the person that LAPD stops from their Profile?
    2. Is the LAPD violating RIPA and is the LAPD justified in stopping a “Person of interest”?
    3. Is there a bias? If so, How Prevalent is this bias within the LAPD


We start by creating a copy of DF and naming it mdf, using the replace function we can then replace the Area ID with their corresponding names such as 01 with Central. We do this for all of the area code up to 23 different values. Using a pivot table, with the Stop_year data that displays the year date of the arrest. We can create a table using the Area as the index and ‘count’ as the aggfunc. Using the year arrest in our function, we can tally the total arrests by their year instance in these areas. This can be used to show the total arrests by the area within our dataset. 
![bar_area!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/README.md#L73)


Because of our usage of count, our pivot table should display the amount of arrests within an area. We can then draw a conclusion from using a visualization to neatly display our findings.
Data: From this visualization , there are a few areas that stand out as having more arrests. The 2 top outliers seem to be 77th street and Newton. From this data we can see that there have been significantly more stoppages within the Newton area and 77th street area. Both contain dangerous areas in LA such as Slauson Avenue.
![77!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/README.md#L78)
![newton!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/README.md#L79)


Basis for Stop:
Similarly, to analyze the basis for a police stoppage encounter. We created another pivot table using Basis for stop as the index, Stop Time as the values, and count as aggfunc. This is done similarly to display the counts of the encounters by the basis of the stop. We create another visualization to analyze the results.
![basis_for_stop!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/README.md#L84)

Data:
From looking at the results, we can see that the largest reason for stoppages were from Officers Witnessing a commission of a branch. This was followed by a matched suspect description and reasonable suspicion of crime. 

Result of the Stop Clean:
The result of a stop is created by having many individual yes and no in the result of the stoppage. We must clean the multiple result of action into binary 0,1 results instead of yes and No. We can then proceed to remove unnecessary characters from the columns to further clean. Creating a result column with all the possible results, which we can then create a new Column “Result” with all the values of the stoppage results. To finalize the cleaning, we replace the results from the Result Column and assign them a number to turn them into numerical values. 
![result_clean1](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/images/result_stop_clean.png)

Result of Stop:
To analyze the results of the stoppage, we must create a pivot table using the Stop Time column as the value, Result column as the Index, and using count as the aggfunc. This will display the amount of occurrences of a specific result from the stoppage.
![result_of_stop!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/README.md#L95)


Analysis:
After creating the visualization, we can analyze the data to see the most common results from the police stoppages. We can conclude that Citations for infraction is the most common result of stoppages, followed by Warnings,  and lastly No Action. These results show that the often responses from the stoppages are very mild responses from the Police side unless action is needed.
Correlation
	To further analyze the data, we can perform correlation analysis using columns that are prevalent to our topic and questions. This can show if there are any significant correlations between columns and the reasons for stoppages.

Race and Basis for Stop:
To see the correlation between the Race column and the Basis of Stop column, we create a crosstab from those columns using True Normalize and True Margins. This creates a messy and long crosstab that is hard to read, to better understand it we can use a visualization. Using a heat map, we can see the correlation values without having to read long float values.
![heatmap1!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/images/heatmap_reason&race.png)

This heat map shows the correlations and shows very little correlation between Races and Basis of stop. The only noticeable results show Hispanics and Witnessing a crime but shows a result of .26 which is low to consider a strong correlation. This also shows total values for the Race stoppages and the basis for stop showing 0.5 for Hispanic stoppages and 0.51 for Officer Witnessing Crime.

Area ID and Race:
Similarly, we can create a crosstab between Area ID and Race to display the table of correlation. We can use this correlation table to see if there is a relationship between stoppages of a race in certain areas.
![heatmap2](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/README.md#L111)
![heatmap3](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/README.md#L112)


Looking at the heat map, we can see very little correlation between different races being stopped and the area they get stopped at. Similarly it shows about 0.49 correlation of Hispanics stoppages as the previous table.


Basis for Stop and Result:
Lastly, we create another correlation table using the Basis of Stop Column and The Result of Stop Column. This table can be used to identify if there is a relationship between cause and effect of a stoppage.
![heatmap3!](https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/a09900ffb5d7b5b12894a2700756bfcd240a9a50/README.md#L120)
From this heat map, we can visualize the correlations between the two columns and create conclusions from the observations. We can see that there is very little correlation from Basis and Result of stop. The highest values showing at 0.14 between Citation  and Officerwitnissing a crime. 0.14 is too low of a score to show correlation.