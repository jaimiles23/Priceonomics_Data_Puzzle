![](https://user-images.githubusercontent.com/50056791/87258811-5e37ba80-c45b-11ea-95fe-b4d8b36f332a.png)

# Priceonomics Data Puzzle
Priceonomics provides a data set for TreefortBnb, Airbnb's fictious rival. They challenges us to tell us the median price of booking a treefort in each of the top 100 cities. Full description available [here](https://priceonomics.com/the-priceonomics-data-puzzle-treefortbnb/).

- More specifically, send us back a table with a list of the median price in each city, ranked from most to least expensive.
- Restrict your analysis to just to the "top 100" cities that have the most units on the market.

## Directory
This repository contains solutions to the Priceonomics Treefortbnb challenge in R and Python. Python solution was conducted in jupyter notebooks and rendered in HTML with in-line analysis.
Solutions comprised of the following steps.
1. Load libraries
2. Import data
3. Clean data
4. Stated analysis
5. Additional EDA

Additional analysis notes are contained in each script.


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
I was surprised that Indianapolis, IN topped the list. As a state capital, I expected it to be high. However, it's curious that its median price is 2x that of the second highest city: Malibu, Ca. The median is a robust statistic that is not sensitive to outliers and thus I found the result interesting enough to investigate. 

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

The mean price for a treefortBnb in Indianapolis is $915.40 with a standard deviation of 969.65. Even more, tree houses cost all the way to 5,500! The spirit of the median (and other measures of central tendency) is to get an understanding of _normal_ in the dataset. Although these are standard measures, something is definitely wrong here. I can't imagine many people paying $5,500 for a treehouse!

To better understand the data, I plotted a binned histogram of the USD price for all units.

![](https://user-images.githubusercontent.com/50056791/87259128-cedfd680-c45d-11ea-990a-8f054ab1e797.png)

!! There are _many_ units above $2,000! And there are even some listed for $10,000!


| id |	city |	state |	price_usd |	num_reviews |
| :-- | :-- | :-- | --: | --: |
| 	26233 | 	Park City | 	UT | 	10000	| 0 |
|	8868 |	Park City |	UT |	10000 |	1 |
|	28627 |	Miami Beach |	FL |	10000 |	0 |
|	2820 |	San Francisco |	CA |	10000 |	31 |
|	8329 |	Chicago |	IL |	6500 |	1 |


The far right of this table shows the number of reviews on each unit. Below is a scatterplot of each Indianapolis unit price vs number of reviews.
![indianapolis_price_vs_num_reviews](https://user-images.githubusercontent.com/50056791/86996325-334e1d80-c160-11ea-851d-f29417e14f4d.png)

The graph shows that prices above $1,000 USD generally have 0 reviews. If we consider reviews to be a proxy measure for visits, we can assume that these units do not constitute normal treefortBnb experiences. I filtered the dataset to only include unit lists with reviews and re-calculated the top median-price TreefortBnb bookings:
		
| city |	state | median_price_usd |	
| :-- | :-- | --: |
| Carmel |	CA |	300.0 |
| Malibu |	CA |	225.0 |
| Truckee |	NV |	200.0 |
| Laguna Beach |	CA |	200.0 |
| Incline Village |	NV |	200.0 |


Of course, Treefort BnB is fictional to begin with and none of the data is a "real" experience. However, this is a useful exercise to demonstrate how a single (robust) measure of central tendency can tell a misleading story and you should always be ready to dig deeper into the data (:
