
# Priceonomics Data Puzzle

This repository contains an R script to solve [The Priceonomics Data Puzzle: TreefortBnb](https://priceonomics.com/the-priceonomics-data-puzzle-treefortbnb/). 

## Challenge
> Tell us the median price of booking a room in each of the top 100 cities in this data set.


## Stated Considerations
- More specifically, send us back a table with a list of the median price in each city, ranked from most to least expensive.
- Restrict your analysis to just to the "top 100" cities that have the most units on the market.

## Extra Considerations
- There may be duplicate city names in different states. 
  - I will handle this by first grouping cities & states and then counting cities. NOTE: Some of these duplicates may be from data entry, e.g., Berkeley, CO is a city neighborhood.
- Don't assume that all data has uniform input.
  - After working with the data, I discovered case inconsistencies, e.g., New York, NY vs new york, NY. In analysis, I considered these the same cities.
- Some locations may be listed under different names. 
  - After grouping the data, I noticed that Miami and Miami beach are both listed.  With some research, I decided to group the two [separately](https://www.tripadvisor.com/ShowTopic-g34438-i92-k1409657-Whats_the_difference_between_miami_and_miami_beach-Miami_Florida.html).


## Analysis Steps:
1. Libraries and packages
   1. Install
   2. Load
2. Import & Clean Data
   1. Import
   2. Clean column names
   3. Check for missing values
   4. Check data types
   5. Clean string data
3. Analysis
   1. Find overlapping city names
   2. Find top 100 cities with most units on market
   3. Sort by price, units
   4. Format data (USD format, string case, remove units and state column)
4. Export Data
   1. Print pretty table to console
   2. Save as csv
5. Additional notes on:
   1. Top city performer
   2. Cities outside top 100

