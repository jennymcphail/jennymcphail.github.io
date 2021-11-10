![royal_mile](https://github.com/jennymcphail/jennymcphail.github.io/blob/master/royal_mile.jfif?raw=true)
### Exploring Edinburgh through data!
## What can we learn from AirBnB data on the popular tourist destination of Edinburgh?

I have decided to look at Edinburgh AirBnB data as that is the city I was born in - I think it's a great place to visit, but do others agree?
You can see my code here: [project-1-blog-post](https://github.com/jennymcphail/project-1-blog-post)

I thought it would be useful to build a price prediction model so that new hosts could have a tool to help them decide how much to list their properties for. You can see the findings from my Exploratory Data Analysis and Model Build in this post.

# Top Level summary of listings

There are 6,634 unique listings belonging to 4,036 hosts - which is an average of 1.64 listings per host. Of course, no one has 1.64 listings so let's look at the distribution of listings per host:
![listings_per_host](https://github.com/jennymcphail/jennymcphail.github.io/blob/master/listings_per_host.JPG?raw=true)

About three quarters of hosts only have one listing but there are a chunk with 2 and some outliers with over 100! So it looks like most hosts are probably just listing their home when they aren't using it but there some who might have a whole business model around letting properties through AirBnB.

# Most and Least Popular Areas to List
## Top 10

| Neighbourhood                            | Listings  | 
|------------------------------------------|-----------|
|Old Town, Princes Street and Leith Street | 765       |
|Deans Village                             | 392       |
|Tollcross                                 | 334       |
|Hillside and Calton Hill                  | 247       |
|Dalry and Fountainbridge                  | 242       |
|Meadows and Southside                     | 228       |
|New Town West                             | 225       |
|Canongate, Southside and Dumbiedykes      | 224       |
|New Town East and Gayfield                | 174       |
|Stockbridge                               | 168       |

The top ten neighbourhoods are central and near tourist attractions.

## Bottom 10

| Neighbourhood                            | Listings  | 
|------------------------------------------|-----------|
|Clovenstone and Wester Hailes             | 8         |
|Colinton Mains and Firrhill               | 8         |
|Liberton East                             | 8         |
|East Craigs North                         | 8         |
|Hyvots and Gilmerton                      | 7         |
|Queensferry West                          | 6         |
|Currie East                               | 6         |
|Carrick Knowe                             | 6         |
|Barnton, Cammo and Cramond South          | 4         |
|Fairmilehead                              | 3         |

Some of the least popular areas to list are out of town, areas I would describe as satellite villages rather than part of Edinburgh proper.
Some are less attractive neighbourhoods - fine to live in but not what a tourist would imagine when they think of Edinburgh.

# Split of Room Types and Pricing by Room Type

- Entire Home/Apt makes up 65.9% of listings and has an average price of £158
- Private Room makes up 32.1% of listings and has an average price of £114
- Hotel Room makes up 1.5% of listings and has an average price of £259
- Shared Room makes up 0.4% of listings and has an average price of £33

Shared Room is the least popular listing type and also the cheapest.

# Is there Seasonality in Pricing?
![seasonal_pricing](https://github.com/jennymcphail/jennymcphail.github.io/blob/master/seasonal_pricing.JPG?raw=true)

At a top level, the seasonality doesn't follow what I expected - as the Fringe Festival runs in August I thought that would be the most expensive time of year. However room type also influences price (as we saw above) and I discovered some extreme outliers in price too which I decided to remove as part of the model build process.

# Model Build

I used the data in the listings file to build my model. As the target is continuous (price in £) I used a Regressor Decision Tree. I split the data 70/30 into training and test datasets and used the first to fit the model and the second to test how it performs on unseen data. I also converted any categorical variables into binary features.
1. **Model iteration 1** - baseline model - this had a very high error rate (Mean Absolute Percentage Error) on the test data (88%) and a very low one on the training data (0.06%), and also a big difference between the Mean Absolute Error (100.9) and Median Absolute Error (30.9) on the test data - overfitting to training data and outliers in price causing these issues
2. **Model iteration 2** - price outliers removed - this improved the performance of the model on the test data (MAPE - 69%) and also brought the Mean and Median Absolute Errors closer together (63.3 and 30.0) however it is still really overfitted to the training data.
3. **Model iteration 3** - reduced the number of features - this improved the performance of the model on the test data (MAPE - 65.6%) and also reduced the overfitting to the training data (MAPE - 22.8%) 

# Conclusion

Whilst I was able to improve the performance of the model, I don't think it is good enough for new hosts to use to price their listings. In order to make it really good, I think we need to know how many guests each listing can accommodate as I think this will be a key predictor of listing price.
