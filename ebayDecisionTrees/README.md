# EbayDecisionTrees

## Problem Statement:

The task is to predict whether or not the auction
will be competitive.

## The Case:
1972 auctions that transacted on eBay.com during May–June 2004. The goal is to use
these data to build a model that will classify auctions as competitive or non-competitive.
A competitive auction is defined as an auction with at least two bids placed on the item
auctioned. The data include variables that describe the item (auction category), the
seller (their eBay rating), and the auction terms that the seller selected (auction
duration, opening price, currency, day-of-week of auction close). In addition, we have
the price at which the auction closed. 

## Preprocessing steps performed:

* Reduce number of categorical predictors by binning/grouping them
* Create dummy variables for categorical predictors
* Check for missing values
* Check for outliers
* Drop 'Close Price' predictor – impossible to know the close price before the auction ends, hence not useful in predicting outcome

## Interpreting Decision Tree Results

The blue color of the nodes indicates that the majority of the prediction is “Competitive” (y =1). The orange color of the nodes indicates that the prediction is “non-competitive” (y = 0). Denser color of the nodes indicates higher purity of the nodes. 

[DecisionTree2](/images/Tree2.png)

Duration, OpenPrice, SellerRating, the currency “EUR”, the “Music/Movie/Game” category, and the “Automotive” category are important predictors for partitioning the Competitive auctions from on-competitive auctions. Among them, Open Price is particularly important, since splits on this variable is recurrent at different levels of the tree. More specifically, lower Open Prices are associated with predictions of competitive auctions, and higher Open Prices are associated with predictions of non-competitive auctions. This result is expected because consumers more interested in bidding if the good is cheaper.

## Recommendations

* Lower Open Price, and not selling the product in Euro will increase the likelihood of competitive auction. 
    * The critical threshold for Open Price is 1.775, as indicated by the initial split at node #0. If possible, it is strongly recommended that the seller set the Open Price to less than 1.775. 
    * The seller is also encouraged to avoid selling the product in Euro for reasons mentioned already in this section. 

Few more specific recommendations are made based on the decision paths with the purist child nodes and leaves. Since prescriptions that include more details are more susceptible to inaccuracy, only the result of two purist partitions are included in this recommendation.



* Set the duration of the auction to less than 6 days
    * According to the decision path that ends at leaf node #3 and leaf node #4 (node #0 -> node #1 -> node #2 node -> node #3 and node #4):  Given that the seller set the open price to less than 1.775,  if the seller also sets the duration of the auction to less than 6 days, then the seller will very likely have a competitive auction. 



* If the open price is greater than 1.775 (node #0), and if the seller’s rating is greater than 570 (node #8), and if the open price is greater than 3.82 (node #14), and if the product of concern is under the category “Automotive” (node #18), then the seller will very likely have a non-competitive auction (node #32). 
    * According to the decision path that ends at node #32 (node #0 -> node #8 -> node #14 -> node #18 -> node #32), 



* If the seller is selling Automotive and cannot afford to or is unwilling to set the auction price to lower than 1.775, then the seller should expect the auction to be non-competitive and forgo their auction practice if non-competitive auctions are not acceptable to them.

