
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
  - After grouping the data, I noticed that Miami and Miami beach are both listed. With some research, I decided to group the two [separately](https://www.tripadvisor.com/ShowTopic-g34438-i92-k1409657-Whats_the_difference_between_miami_and_miami_beach-Miami_Florida.html).


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


## Results
Median price for the top 100 cities in the dataset is available in *Miles_Jai_Priceonomics_Puzzle_Solution*. Below are the top 10 results 

| Rank | city | state | median_price_USD
| :-- | :-- | :-- | --:
1 | Indianapolis | IN | 650
2 | Malibu | CA | 304
3 | Park City | UT | 299
4 | Truckee | NV | 275
5 | Healdsburg | CA | 275
6 | Laguna Beach | CA | 268.5
7 | Incline Village | NV | 259
8 | Manhattan Beach | CA | 209
9 | Charlotte | NC | 200
10 | Sonoma | CA | 200


## Additional analysis
I was surprised that Indianapolis, IN topped the list. As a state capital, I expected it to be high. However, it's curious that its median price is 2x that of the second highest city: Malibu, Ca. While the median is a robust statistics not sensitive to outliers, I find the result interesting enough to investigate. 

With a bit more digging, I found the following statistics for Indianapolis:
| Statistic | price_USD |
| :--       | --: |
| units   |  251   |
| mean   |  915.40 |
| st_dev | 969.65 |
| min | 33 |
| max | 5500 |
| Q1 | 162.5 |
| Q2 | 650 |
| Q3 | 1200 |

The mean price for a treefortBnb in Indianapolis is $915.40 with a standard deviation of 969.65. Even more, tree houses cost all the way to 5,500! The spirit of the median (and all measures central tendency) is to get an understanding of _normal_ in the dataset. Although these are standard measures, something is definitely wrong here. I can't imagine many people paying $5,500 for a treehouse!

Thankfully, priceonomics also included the number of reviews that each listing has. Below is a scatterplot of each Indianapolis unit price vs number of reviews.
![.](https://user-images.githubusercontent.com/50056791/86526191-7ac56880-be45-11ea-8a72-f72ae9a22816.png)

