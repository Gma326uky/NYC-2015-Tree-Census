# NYC 2015 Tree Census
For this project, I looked into addressing some of the goals of the the NYC 2015 Tree Census project.

The NYC tree census has been done every 10 years since 1995, which records 
the location, size, species, and condition of all public street and park trees 
in New York City. 

For the park trees, it involves volunteers from NYC that are trained on-site, 
and for the street trees, it uses cars with mounted devices that collect 
information on the trees.

https://www.nycgovparks.org/reg/trees-count

Some of its goals are:

- Understand the characteristics of the Urban forest's population in NYC.
- Understand the change over time of the urban forest in NYC.
- Develop new management and operational plans for all trees across the city.
- Identify areas where there is room for more trees.

Since one of the goals of the study is to understand the characteristics of the
Urban forest's population in NYC, my goal was to create a plot that shows
some of these characteristics.


## How It's Made:

**Tech used:** R, Rstudio (tidyverse, ggplot2)

I imported the data from the last NYC Tree Census, done in 2015, which can be found here:

https://data.cityofnewyork.us/Environment/2015-Street-Tree-Census-Tree-Data/uvpi-gqnh/about_data

I previewed the data with the head() function, and after looking at the variables, I decided I wanted to find the difference in the average size of different tree species, and how the average size of different species of trees varied per location of NYC.

The DBH or Diameter at Breast Height is a measurement that is commonly used to measure the size of living trees, so I used the "tree_dbh" column in the data set for the size. 

For the species, since there were 133 species in the data, I decided to only analyze the 5 species of trees that had the most observations in the data. Using functions from the tidyverse package, I grouped that data by "spc_common" which is the name of the tree species. I counted the observations for each species, arranged he results in descending order so the ones with the highest counts would be at the top, and previewed only the first 5 rows of the data. After finding the 5 most common tree species, I created a vector with them ("London planetree", "honeylocust", "Callery pear", "pine oak", and "Norway maple"), and created a new data set by filtering the original data using this vector.

For the locations, I thought about using either the cities or the boroughs of NYC. I use the length() function on to count how many unique values were on the "zip_city" and "borough" columns. After seeing that there were 5 boroughs in the data compared to 47 cities, I thought boroughs would be a better choice. The 5 boroughs of NYC are Bronx, Brooklyn, Manhattan, Queens, and Staten Island. 

I created a bar chart using ggplot, where I grouped the data by the species and the borough. I used the summarise() function from the tidyverse to calculate the average DHB, which would be the variable on the y-axis of my plot. I used the species as the variable on my x-axis, and used colors in the bars to represent the 5 boroughs of NYC. 


## Optimizations

In order to make my data more manageable and my plot simpler, I filtered the data to include only the 5 most common species of trees in NYC.

I specified the "position" argument of my bar chart to "dodge" so that the bars would be next to each other, helping visualize the data better.

I also made sure to add descriptive labels and a theme to my plot to make it easier to understand and more visually appealing.



## Lessons Learned:

There does seem to be a significant relationship between size and location for all tree species, given that the average DBH changed in the same direction (increased or decreased) for all trees depending on the location.

However, proportion of the change in mean DBH does seem to differ according to the tree species, with the change in the "Callery pear" species being the most consistent, and the change in the "London planetree" having the most variation. Something to note is that at every location, the "Callery pear" always had the lowest average DBH of all 5 tree species, and the "London planetree" the highest, which may be related to the proportional change per location.
