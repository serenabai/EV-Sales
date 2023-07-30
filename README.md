# Analyzing EV Sales and Predicting EV Sale Price

## Introduction

Returning to my birth city of Beijing for the first time in two years, I couldn't help but notice the massive increase in the amount of electric vehicles on the city streets. With their unmistakable green license plates and recognizable logos, EVs in China now make up more than half of the world's sales, with a quarter of cars manufactured in China being electric or hybrid vehicles as of 2022. Although Tesla has planted itself solidly at the top of the China EV industry, most of its closest competitors are actually Chinese car companies including BYD and Geely, who have yet to aggressively expand internationally. 

I began this project with the goal of gaining an understanding of the EV industry, especially the factors that go into pricing and the main drivers of sales. I am interested in using my findings to create a model that can predict how Chinese EVs could potentially be priced in the global market based on their technical characteristics. 

## Data Collection

In order to obtain the most up to date data on electric cars available internationally, I used BeautifulSoup to scrape 335 EVs from ev-database.org, a fairly comprehensive website cataloguing EVs available in Europe along with several key metrics, including Range, Efficiency, Body Type, Charger, and other important characteristics of electric vehicles. 

I also used EV sales data from US and Europe obtained from afdc.energy.gov/data and insideevs.com. 

## EDA

<img width="616" alt="Screen Shot 2023-07-30 at 7 25 25 PM" src="https://github.com/serenabai/EV-Sales/assets/78036684/439a5f95-07a2-4757-8539-a4cca0cde2d6">

The largest body type category in this dataset is SUV, which makes up 45.2% of the vehicles. Following SUVs, the most frequent body types in the data, in order, are SPV, Sedan, then Hatchback. 

<img width="534" alt="Screen Shot 2023-07-30 at 7 27 14 PM" src="https://github.com/serenabai/EV-Sales/assets/78036684/e70715e4-445d-4a8e-a6f7-7bed2ca9fb93">

There is a fairly even distribution amongst market segments, excluding sector C, which leads at 28.1%, and Sector A, which is the smallest at only 1.1%. Differences in distribution of market segments in different countries will be important to take into consideration.

<img width="602" alt="Screen Shot 2023-07-30 at 7 27 54 PM" src="https://github.com/serenabai/EV-Sales/assets/78036684/05554e70-49c7-459a-b509-209ff4237b88">

Unsurprisingly, the majority of EVs (66.5%) are five-seaters. 

<img width="990" alt="Screen Shot 2023-07-30 at 7 35 02 PM" src="https://github.com/serenabai/EV-Sales/assets/78036684/a1ac0d73-c4f9-43ac-bc04-a8b466a9c9f0">

I am most interested to see which variables have the highest correlation with price and sales. Within this sample of best selling cars, the price is more highly correlated with battery type, range, and fast charge, and in general has higher correlations with almost every metric than the entire dataset. Within this sample, sales are most highly correlated with top speed. 


<img width="452" alt="Screen Shot 2023-07-30 at 7 35 56 PM" src="https://github.com/serenabai/EV-Sales/assets/78036684/223d582b-4043-4cbb-b246-e6b74791a6fd">

In this visualization of acceleration speed vs price, we can see that most of the top sellers (red) are clustered together where price is closer to the minimum and acceleration speed is closer to the middle. This makes sense since more people can afford lower priced cars, and most people tend to buy cars with moderate performance. There is one outlier with very slow acceleration speed that is still a top selling car; it would be interesting to investigate this and figure out how this model has managed to perform so well despite its poor acceleration. 


## Linear Regression Model


I first ran the linear regression model simply using all numerical features (including one-hot encoded body type) as inputs. This gave me the following test and train scores:

train score: 0.7356124984151471
test score: 0.7166922951160326


<img width="1022" alt="Screen Shot 2023-07-30 at 7 47 00 PM" src="https://github.com/serenabai/EV-Sales/assets/78036684/e63b8c1a-8bf0-4f1f-8c2e-674dbb08d012">

<img width="384" alt="Screen Shot 2023-07-30 at 7 49 32 PM" src="https://github.com/serenabai/EV-Sales/assets/78036684/f09164ed-381f-4cb5-9b7d-2c962aa58520">

After examining scatterplots between price and other variables, I noticed that the relations appeared to be non-linear, and in fact, the distribution of price was right skewed not normal. To correct for this, I ran the regression again, this time using log(price) as the endogenous variable. This, combined with adjusting a few other features, allowed me to increase my test and train scores by around 10% each:

train score: 0.8280186615735312
test score: 0.827051138963188

<img width="748" alt="Screen Shot 2023-07-30 at 7 52 07 PM" src="https://github.com/serenabai/EV-Sales/assets/78036684/83d13735-d782-47d8-b715-e95c2441d288">



