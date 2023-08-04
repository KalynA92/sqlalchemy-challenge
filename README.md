# sqlalchemy-challenge

# Hawaii Climate Analysis

While planning a trip to Hawaii, you decide to do a climate analysis about the area. The following sections outline the steps that you need to take to accomplish this task.

## Part 1: Analyze and Explore the Climate Data

## Task

In this section, you’ll use Python and SQLAlchemy to do a basic climate analysis and data exploration of your climate database. Specifically, you’ll use SQLAlchemy ORM queries, Pandas, and Matplotlib. To do so, complete the following steps:

Perform a precipitation analysis and then a station analysis by completing the steps in the following two subsections.

## Precipitation Analysis

Find the most recent date in the dataset.

Using that date, get the previous 12 months of precipitation data by querying the previous 12 months of data.

Select only the "date" and "prcp" values.

Load the query results into a Pandas DataFrame. Explicitly set the column names.

Sort the DataFrame values by "date".

Plot the results by using the DataFrame plot method

Use Pandas to print the summary statistics for the precipitation data.

## Station Analysis

Design a query to calculate the total number of stations in the dataset.

Design a query to find the most-active stations (that is, the stations that have the most rows). To do so, complete the following steps:

List the stations and observation counts in descending order.

Answer the following question: which station id has the greatest number of observations?

Design a query that calculates the lowest, highest, and average temperatures that filters on the most-active station id found in the previous query.

Design a query to get the previous 12 months of temperature observation (TOBS) data. To do so, complete the following steps:

Filter by the station that has the greatest number of observations.

Query the previous 12 months of TOBS data for that station.

Plot the results as a histogram with bins=12

Close your session.

## Description

I started by importing all of the necessary dependencies. I created the engine to the hawaii.sqlite file provided. Reflected the database into a new model and displayed the tables. Checked the names of the tables in the database. Saved the refrences to each table. Created a session to link Python to the database. To find the most recentdate in the dataset, I queried the measurement table's date column and ordered by the same in a descending fashion and specified to display the first element of the column. Using the datetime package I calculated the date one year from the last date in the data set. I specified 366 days in order to include the specific day of the month of that year. Then performed a query to retreive the last 12 months of precipitation data using the measurement table's date and prcp columns. I filtered by the measurement table's date column, with the calculated date of the previous 12 months, and retreived all the data. I then saved the query results to Pandas DataFrame. I sorted the values indexing by the date as well as sorting by the values of the dates. Then plotted the dataframe using Pandas Plotting with Maplotlib. Using the .describe() function, I was able to calculate the summary statistics for the precipitation dataframe.

For the station analysis, I started by perfornming a query from the station table's station column using the .count() function to retrieve the total number of stations in the dataset. I used the .count() function again when querying the measurement table's station column to count the total number of times the stations appear in the dataset. I grouped by the station column and ordered by the total count of each station in a descending fashion. To calculate the lowest, highest, and average temperature I first grouped the necessary functions in a list, then performed a query using the measurement table's "tobs" or temperature column, grouping by the station, and specifically by the most active station based on the total number of times it appears in the dataset. To find the most recent date for the most active station in the dataset, I performed a query for both the measurement date and measurement tobs columns filtering by the most active station as determined in the previous query, and ordering by the date column in a descending fashion specifying the first element in the column. I then calculated the date one year from the last date in the dataset for the most active station specifying 366 days to include the correct dates. Then queried the measurement table's date and tobs columns, filtering by both the most active station and calculated date one year from the last date in the dataset. I saved the query to Pandas DataFrame and plotted a histogram using Pandas Plotting with Matplotlib specifying the bins to be 12. After getting all the results, I closed the session.  


# Part 2: Design Your Climate App

## Task

Now that you’ve completed your initial analysis, you’ll design a Flask API based on the queries that you just developed. To do so, use Flask to create your routes as follows:

1. /

Start at the homepage.

List all the available routes.

2. api/v1.0/precipitation

Convert the query results from your precipitation analysis (i.e. retrieve only the last 12 months of data) to a dictionary using date as the key and prcp as the value.

Return the JSON representation of your dictionary.

3. /api/v1.0/stations

Return a JSON list of stations from the dataset.

4. api/v1.0/tobs

Query the dates and temperature observations of the most-active station for the previous year of data.

Return a JSON list of temperature observations for the previous year.

5. api/v1.0/<start> and /api/v1.0/<start>/<end>

Return a JSON list of the minimum temperature, the average temperature, and the maximum temperature for a specified start or start-end range.

For a specified start, calculate TMIN, TAVG, and TMAX for all the dates greater than or equal to the start date.

For a specified start date and end date, calculate TMIN, TAVG, and TMAX for the dates from the start date to the end date, inclusive.

## Description

I started by importing all of the necessary dependencies. I created the engine to the hawaii.sqlite file provided. Reflected the database into a new model and displayed the tables. Checked the names of the tables in the database. Saved the refrences to each table. Created our session to link Python to the database. I then performed the flask setup. I started by creating the homepage displaying all of the available api routes. I then created the api route to the precipitation data. To return a list of the precipitation data for the last 12 months, I calculated the date one year from the last date in the dataset. I then performed a query for the measurement table's date and prcp columns and filtered by the date column being greater than or equal to the calculated year ago date. I closed the session. I created a dictionary from the precipitation data and appended it to a list with the corresponding date. Then specified to return the dictionary in jsonified format. I then created the api route to the station data. I started another session with the engine created. To return a list of the stations in the dataset, I queried the station table's station column, retrieved all of the stations, closed the session, using numpy library's .ravel() function over the results from the query I was able to then get the list of all stations. I then returned that list in jsonified format. I created a api route to the tobs or temperature data. I started another session. To return a list of the date and temperatures for the most active station in the data, I calculated the date one year from the last date in the data for the most active station specifying 366 days to include all the dates. I then queried the measurement table's date and tobs columns filtering by the date column being greater than or equal to the calculated year ago date, and also filtered by the most active station. I then closed the sesssion. I created a dictionary from the temperature data and appended it to a list for the most active station with the corresponding date. I then returned the disctionary in jsonified format. I created the api route for user inputted start date. I defined the start date an being the input. I started a session. To return a list of the minimum, maximum and average temperature for a specified start date, I created a list of the functions required. I started a query using the functions, filtering by the measurement tables date column being greater than or equal to the inputted start date. I closed the session. I created a dictoary for the temperature statistics and returned it in jsonified format. I the created a session for the user inputted start and end date range. To return a list of the minimum, maximum and average temperatures for a specfied start and end date, I used the same logic and coding as I did with the start route this time adding the user inputted end date as a filter.  


