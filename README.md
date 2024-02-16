Project Description: The goal of our project is to analyze what characteristics are prominent within samples of the LAPD RIPA database from data.lacity.org. This includes race, gender, perceived age, and what type of stops are made. We utilize stratified random sampling to sample the database and utilize K-Means Clustering and KNN Regression.



Stratified Data Sampling: In our data we needed to perform a sampling method and decided to use stratified sampling. Had to take the Stop_Year column and copy it to a new column. Used a split and slice to parse and set the column to only have the year. Then used the groupby function on the Stop_Year with sampling 4000 per year. 2023 was a year with a low frequency of entries so that year was not included. Used the 1.3 gb approx file and the commented data below to sample from it. 



Data Cleaning:
In order for data to be used within our project, we performed cleaning methods before we proceed to use analysis methods. After we initialize the data, we proceed to convert (yes,no) categories within the data into numerical (0,1) so that we can include it within our functions during analysis. After deciding what columns would be most beneficial to our analysis, we remove the unused columns by using the drop functions in Pandas and rewrite them to the CSV file. This makes it easier for us to analyze and helps by removing large amounts of data that creates issues when trying to view the data.


