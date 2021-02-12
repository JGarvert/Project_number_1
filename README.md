# NYC Citibike Exploration and Analysis

For this project, we analyzed data from New York City's Citibike bikeshare program across a variety of metrics. The secions below will explain our thought process, coding, and analyisis with the following sections:

* What is Citibike 
* Initial Dataset
* Questions for Analysis
* Data Cleaning Process
* Initial Exploration Charts
* Question Findings
* Additional Questions for Further Research

### What is Citibike?
Citibike is a bikesharing program in New York City. Stations with bike racks are located across the city. Riders can pick up a bike from any station, ride as much as they'd like, and return the bike to any other station.

Riders have two options for payment. They can either pay a flat subscription of $15/month for unlimited 45-minute rides, pay $15 for unlimited 30-minute rides in a single day, or $3 for a one time 30-minute trip. If a rider goes over the time limit, there is a small fee for each minute over the alloted time. 
(Source: https://www.citibikenyc.com/pricing)

### Initial Dataset
Citibike publishes its ridership data as a monthly csv file, which can be found here: https://www.citibikenyc.com/system-data.

Each csv includes the following columns of data:
* Trip duration
* Bike ID 
* Date/Time bike is checked out and time bike is returned 
* Latitude/Longitude of check out and check in station 
* Payment Method (subscriber or customer) 
* Rider Gender
* Rider Birth year 

### Question for Analysis

* How does the number of trips and their duration fluctuate over the course of the 6 months? 
* Do different age groups bike more or less than each other?
* Which stations are most popular?
* What are the average times a bike is checked out for, and are there any outliers? 

We chose these questions because we are curious about bikeshare programs in other cities. They are innovative programs for public health and the environment, and an alternative method of transportation that could grow more in the future. 
We were also curious about the demographics of the bikeshare population in New York City, which can provide insight on who is using the program and how it might be modified in other cities across the country.

### Data Cleaning
Overall, this was a relatively clean dataset. We modified some columns to fit our needs, and dropped those which did not, but it did not require extensive cleaning or supplementation from another sata source. Below are some of the steps we took to make the data more useable for our project:

First, we appended six months of csv's into on single dataframe. This allowed us to perform analysis on the whole dataset without managin six different data frames. 

Next we removed all rows with null values. We did this for two primary reasons: First, most of the null values were all in the same rows, meaning that we could drop those rows with no impact to the underlying data. Second, even where null values were embedded in otherwise full rows, we were looking at general trends, so dropping some data was unlikely to impact overall analysis.

After ensuring that we had cleaned up rows, we modifies several columns to fit our needs. First we split the date/time columns into one column for the data and one for the time. Since we were not looking at hour-by-hour trends, we dropped the time altogether and kept the data for our primary analysis. We also conversted the trip duration column units from seconds to minutes, which was a more usefull measurment. Finally, we took the birth year column and modified it to show age instead. 

Lastly, some of the columns containe ages that were between 100 and 150 years old. This may simply be a mistke in how Citibike catalogs age, but we dropped all rows where the rider was greater than 100 years old. 


### Initial Exploration
To get a handle on the data we were working with we created a few inital charts to see general trends. These charts are explained below.

##### Customer vs Subscriber
First we wanted to see a breakdown of riders by payment type to see how people were using the payment plans offerred. 

![UserType](https://raw.github.com/JGarvert/Project_number_1/main/charts/usertype.png)

This suggests that there are many more subscribers than customers, and that subscibers are likely riding more often. This would make sense if, for example, many poeple use the subscription as a commuting method rather than a recreational experience. 

##### Station Poularity
We also wanted to get a sense of the popularity of various stations

![Station Counts](https://raw.github.com/JGarvert/Project_number_1/main/charts/stations.png)

As seen here, no single station stands out significantly above the rest. 

##### Age of Ridership
Lastly, we wanted to see ridership by age. 

![Age Bins](https://raw.github.com/JGarvert/Project_number_1/main/charts/agebins.png)

By binning the ridership into age categories, we can see that younger people are taking more trips overall. However, if you look at a histogram by age, we see some anomolies

![Age Histogram](https://raw.github.com/JGarvert/Project_number_1/main/charts/agehist.png)

There is a clear spike at age 50. That spike cannot fully be explained by our data, but a few possibilities are that the default birth year if not provided is 1970 (giving age 50), that there is one person or group of people at age 50 that are biking significantly more than others, or that the Citibike data was skewed somehow before we began our analysis.

### Analysis Findings
As a reminder, our questions were: 
* How does the number of trips and their duration fluctuate over the course of the 6 months? 
* Do different age groups bike more or less than each other?
* Which stations are most popular?
* What are the average times a bike is checked out for, and are there any outliers? 

##### Trips Over Time
To examine our first question about ridership over time, we grouped the data by date and placed it into a line graph. Additionaly, we separated the subscriber and customer data for additional insights

![Ridership Graph](https://raw.github.com/JGarvert/Project_number_1/main/charts/ridershiplinegraph.png)

One trend that jumps off the graph is that ridership declined dramatically during the hight of New York City's COVID-19 lockdown. This drop was most pronounced among subscibers. 

In the following months, however, ridership incrreases back to pre-lockdown levels. That said, the make up of the user types changes from mostly subscribers to an even mix between customers and subscribers. This indicates that either people who were subscibers cancelled their subscription in March and did not bother to renew it when they started travling again, or that more people are using the program as a recreational tool while still in some form of stay at home order. 


##### Age vs Duration
For the second question, we wanted to see how age affected individual riders' trip length. To examine this visually, we used a scatterplot of those two variables. 

![Age vs Duration](https://raw.github.com/JGarvert/Project_number_1/main/charts/ageduration.png)

According to the scatterplot, most trips by all age groups are under 15 minutes, and duration seems to peak in the 30’s and then decrease with age.
That said, age 50 has many more data points (remember the age histogram) so the duration at that age is more spread out, explaining the vertical spike at age 50

##### Mapping Popular Locations
In the initial exploration, we determined the most popular stations. Because none of us live in New York City, that's not particularly useful, so we mapped out the station popularity. The heatmap incorporates all stations, while the pins represent the top ten.

![Full Map](https://raw.github.com/JGarvert/Project_number_1/main/charts/fullmap.png)

Based on the heatmap, and the fact that all the pins are located on Manhattan, that is clearly where the bulk of these trips take place. There are some stations out in Brooklyn, but they get significatly less traffic. 

One surprising finding is that we expacted more of the popular stations to be located around Central Park, since that seems like a nic open space to use a bike. It is clear in this map however, that the bulk over ridership is concentrated in mid and lower Manhattan. 

##### Average Checkout Time by Bike
To see the average checkout time, we grouped the data by bike ID and averaged the trip length. We then put it into a boxplot to easily visualize the measures of central tendency. 

![Average Bikes](https://raw.github.com/JGarvert/Project_number_1/main/charts/averagebox.png)

Clearly, however, the presence of dramatic outliers obscure the measures of central tendency. While determining outliers is important, we also wanted to see basic measures. By dropping the Matplotlib fliers, we were able to see those data.

![Age vs Duration](https://raw.github.com/JGarvert/Project_number_1/main/charts/averagedzoomed.png)

From this boxplot, we can see that the majority of checkout times are reasonable, coming in at a median of about 20 minutes, with an IQR of just below 10 minutes to just over 30 minutes. 

Given that we saw significant outliers, we then chose to look at those specifically. 

The bike that had the longest checkout time (about 20 hours) was checked out only once in our dataset. We hypothesize that the user damaged the bike and it was taken out of circulation after it was returned. With only one data ount, we could not create a boxplot for this bike. 

The second and third most used bikes are charted in boxplts below. Once again, outliers obscured the measures of central tendency, so we dropped the fliers to see those measures. 

![Bike2](https://raw.github.com/JGarvert/Project_number_1/main/charts/bike2full.png)
![Bike2](https://raw.github.com/JGarvert/Project_number_1/main/charts/bike2zoomed.png)
![Bike3](https://raw.github.com/JGarvert/Project_number_1/main/charts/bike3full.png)
![Bike2](https://raw.github.com/JGarvert/Project_number_1/main/charts/bike3zoomed.png)

After the flies are dropped, the median and IQR of these bikes is actually not far off of the average bike. This suggests that, except for single outlier incidents, bikes are generally used the same amount. 

### Challenges, Additional Questions, and Wrap Up

Most of the data was not very surprising, but there were unique circumstances where we found things that were unusual such as
* Impact of COVID-19 on ridership
We did not factor COVID-19 into our initial hypotheses, but it clearly impacted ridership over those six months
* Age, the spike at age 50. As discussed above, this may be the result of bad data or an anomoly, but it was facinating to discover and hypothesize reasons for that spike. 
* We thought there would be a larger amount of users vs subscribers, but it is clear that, at least initally, this program is used more for commuting than recration. 

##### Additional Questions/Areas to Explore:
* We would have liked to have a person ID, to open up our analyses further, although we understand why that is not available
* Explore the spike at the age of 50 years old
* Cost data may have been an interesting avenue to explore, if it was available
* What do they do with bikes that go missing or are damaged, and how does that factor into our analysis?

