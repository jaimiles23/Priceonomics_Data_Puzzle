@modify date 2020-07-12 16:55:36

# Priceonomics Data Puzzle
Priceonomics provides data on treeforts for TreefortBnb, Airbnb's fictious rival. They challenges us to tell us the median price of booking a treefort in each of the top 100 cities. Full backstory and challenge available [here](https://priceonomics.com/the-priceonomics-data-puzzle-treefortbnb/).

- More specifically, send us back a table with a list of the median price in each city, ranked from most to least expensive.
- Restrict your analysis to just to the "top 100" cities that have the most units on the market.

## Directory
This repository contains solutions to the Priceonomics Treefortbnb challenge in R and Python. Python analysis in Jupyter Notebook and rendered to HTML for in-line analysis.
Solutions used the following steps.
1. Load libraries
2. Import data
3. Clean data
4. Stated analysis
5. Additional EDA

Additional analysis notes are contained in each script.


## Results
Median price for the top 100 cities in the dataset is available in the *solution.csv*. 
Below are the top 10 results:

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
I was surprised that Indianapolis, IN topped the list. As a state capital, I expected it to be high. However, it's curious that its median price is 2x that of the second highest city: Malibu, Ca. The median is a robust statistic that is not sensitive to outliers. I suspected that the data had a right skew and investigated.

I found the following statistics for Indianapolis, IN:
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

The mean price for a treefortBnb in Indianapolis is $915.40 with a standard deviation of 969.65. Even more, tree houses cost all the way to $5,500! The spirit of the median (and other measures of central tendency) is to get an understanding of _normal_ in the dataset. Although these are standard measures, something is definitely wrong here. I can't imagine many people paying $5,500 for a treehouse!

To better understand the data, I binned it and plotted a histogram of the USD price for all units.

![](https://user-images.githubusercontent.com/50056791/87259128-cedfd680-c45d-11ea-990a-8f054ab1e797.png)

There are _many_ treeforts above $2,000! There are even some units listed for $10,000!


| id |	city |	state |	price_usd |	num_reviews |
| :-- | :-- | :-- | --: | --: |
| 	26233 | 	Park City | 	UT | 	10000	| 0 |
|	8868 |	Park City |	UT |	10000 |	1 |
|	28627 |	Miami Beach |	FL |	10000 |	0 |
|	2820 |	San Francisco |	CA |	10000 |	31 |
|	8329 |	Chicago |	IL |	6500 |	1 |



The far right of this table shows the number of reviews on each unit. Below is a scatterplot plotting each Indianapolis unit price vs number of reviews.
![indianapolis_price_vs_num_reviews](https://user-images.githubusercontent.com/50056791/86996325-334e1d80-c160-11ea-851d-f29417e14f4d.png)

The graph shows that prices above $1,000 USD generally have 0 reviews. If we consider reviews to be a proxy measure for visits, we can assume that these units do not constitute normal treefortBnb experiences. I suspected that this same relationship is present in the larger database and graphed a scatterplot of Unit Price USD vs Number of Reviews for the original dataset.
![](https://user-images.githubusercontent.com/50056791/87259605-59760500-c461-11ea-8c22-59cd2c4e2248.png)

Bingo! Below is a table of the top median-price TreefortBnb bookings that have one or more reviews:
		
| city |	state | median_price_usd |	
| :-- | :-- | --: |
| Carmel |	CA |	300.0 |
| Malibu |	CA |	225.0 |
| Truckee |	NV |	200.0 |
| Laguna Beach |	CA |	200.0 |
| Incline Village |	NV |	200.0 |


Of course, it doesn't matter whether or not the listings had reviews --Treefort BnB is fictional and none of the records represent a "real" experience. However, this is a useful exercise to demonstrate how a single (robust) measure of central tendency can tell a misleading story and you should always be ready to dig deeper into the data (: