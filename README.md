World Wide Products Inc
==============================

World Wide Products Time Series Forecasting

Project Organization
------------


    ├── data
    │   └── raw   
    │        │── Product Data
    │
    ├── notebooks          
    │   └── src.ipynb               


Data
----
The data here is pretty well formatted. A row contains a Product_Code, Warehouse, Product_Category, Date
Order_Demand. There are 33 unique product categories and roughly 2100 different  product codes. The 
dates range from 2011 to 2017. The order volums vary widely and highly dependant on the product. The median 
of these numbers is 300, but there are some prodducts with order_demand in the millions. Among a specific
product, the distribution of orders is kind of similar. Lots of smallish orders with few very large orders
occasionally.

Feature Engineering
-------------------
I didn't do a lot with categories here besides the Order_Demand. The main thing necessary here to create 
data that is structured usefully is to have consistent intervals that are don't have too many missing 
values. This wasn't entirely obvious how to do at first because orders are spread in different intervals, 
and some products don't really have many orders at all. What I ended up doing is sorting the list of 
products by total number of orders and trying to make predictions on the most ordered products. I then 
grouped these products by monthly volume from 2012 to 2016 and used this data as my column to run the 
time series forecasting models on.

Time Series Algorithms
----------------------

The first model that I used was exponential smoothing. This looks at previous data and weights them 
by how recent they are. The idea behind this is that more recent data is predictive of the future 
moreso than old data. This approach does not do a good job of predicting cyclical nature of these 
products, but it does do a good job of weighting the importance of recent moves. I also used linear
regression. Again, this is a pretty simple model and I just ran linear regression on the time relationship
between time and order demand. This does a good job of catching overall shifts in product demand, however, 
it fails to catch cyclical movements and can be way off in some cases when the change in product demand is 
not really a linear thing.  s