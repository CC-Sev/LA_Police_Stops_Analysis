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
!(kmeans!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/7cf8bb18b12376e2f3a8b1b6c719c9bda175adc3/images/kmeans_data_plot.png]

!(kmeans2!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/7cf8bb18b12376e2f3a8b1b6c719c9bda175adc3/README.md#L28]

From the data (with ‘Area ID’ on the x bar and ‘Stop Time’ on the y bar), we can see that stops are happening at regular intervals throughout the entire day.

KNN with Regressor Analysis:
Before starting the KNN Regressor function we must clean the data and convert it as floats. This will make the data columns usable for the following functions since the included data is given as STR and will not work. For other values we also must turn categorical values into numerical values, we grab the perceived Gender and replace the terms with numbers from 0-4.

We can use the elbow method to find a good K for the KNN regressor. We must use the X and Y train values and for them to be a temporary model. We can then predict, using the temporary model from Xtest. After this we can also calculate MSE in the for loop to see which resulting K is better.
!(knn regression1!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/elbow_code.png]
!(knn regression2!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/elbow_knn.png]

Asian (1), Black/African American (2), Hispanic/Latino(a) (3), Middle Eastern or South Asian (4), Native American (5), Pacific Islander (6), White (7)


After we determined the K which is N_Neighbors= 3, then we use that to define the grid of feature values. This graph shows the relationship between Race and Age, the 3, 7 are the most group that are stopped. We think that because they have the most population in U.S.
!(plot_race_age!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/plot_race_age.png]

For the following graph. Female(0), Male(1), Transgender woman/girl(2), Transgender man/boy(3), Nonconforming(4).

Do the same thing as above with N_Neighbors= 3, then we define the grid of feature values with Gender vs. Age. Female and Male are the majority to be stopped.
!(plot_gender_age!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/plot_age&gender.png]

Using the graph we can visualize the KNN regressor function for Perceived Gender and the Perceived age. We see that for 0-Female, the perceived age was around 35. 1-Male= 42, 2-Trans woman = 35, Trans Man = 40, 04-Non Conforming =40.

Extra KNN:
!(extra knn!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/mse_graph.png]
!(plot_area_race!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/plot_area&race.png]

We then do a extra KNN for Race vs. Area ID:
We are replacing the AGE with Area ID, then compare it with Race. For that, we are going to calculate the new MSE and make a new elbow graph.
Now we visualize relationship between Race and Area ID. 
As the graph shown above, we know of four areas where the largest number of people are stopped.
There are: Area ID: 10(West Valley),11(North East),12(77th street),13(Newton) 
!(cmap!)[https://github.com/CC-Sev/LA_Police_Stops_Analysis/blob/fa468649a2280e3aa63ad66cc6ab91d8bfe46cfe/images/cmap.png]

Finally, we visualize the relationship between Race and Gender determined by AGE by scatter plot. Also, use different colors to indicate how many of these dots have the same or close color according to the Perceived AGE. In this case, The same or similar color means people were stopped for the same/similar reason or feature.
