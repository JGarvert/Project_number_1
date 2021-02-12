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


### Inital Exploration
To get a handle on the data we were working with we created a few inital charts to see general trends. These charts are explained below.

##### Customer vs Subscriber
First we wanted to see a breakdown of riders by payment type to see how people were using the payment plans offerred. 


a. pie chart by user type (customer and susbscriber)
b. Most/least populer station both start and end stations.
    1. Outliers?  One station with the significantly the most usage?

Output should be a cleaned file that can be used for analysis

2. Analyizations:
b. average duration per ride (are trips shorter/longer based on time of year)
c. average duration by member/non member
d. was there any one bike (id) that had the longest or shortest duration (outlier)
=======
e. Add in map reflecting start of stop locations (as lat/log data is already included)

 # perhaps add in weather data as a comparison - is there a correlation between weather and duration, or number of trips?
