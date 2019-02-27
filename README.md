# Yelp_FraudDetection

After a LocalDiner demo, I was asked if the spatial patterns of user activity that the app uses to differentiate locals from tourists could also be used to detect fraudulent Yelp reviews. I didn't have a good answer at the time but I was curious to see if it could work.


## What are fraudulent Yelp reviews like?
My first (failed) attempt to answer this question assumed fraudulent reviews on Yelp were like those on Amazon -- highly positive reviews left by the seller to artificially bump the product rating. In that case, reviews left by users with few or no other reviews might be suspicious.

While fake positive reviews might also be a problem on Yelp, a more common scenario seems to be a flood of negative reviews left in response to some offensive action by the business owner. For example, Yelp ratings for Masterpiece Cakeshop, the Denver, CO bakery that refused a wedding cake to an LGBT couple, plummeted after the SCOTUS decision in the bakery's favor ([Delish](https://www.delish.com/food-news/a21205908/yelp-reviews-have-plummeted-for-the-colorado-bakery-involved-in-same-sex-wedding-cake-case/)). It should be possible to detect this as a sudden spike in the frequency of reviews regardless of user location.


## The ongoing case of Amy's Baking Company
It's harder to distinguish between real and fake reviews when the fraudulent reviews are posted over time. One such case might be Amy's Baking Company, a bakery in Scottsdale, AZ that appeared on the show Kitchen Nightmares ([Huffpost](https://www.huffingtonpost.com/2013/05/14/amys-baking-company-kitchen-nightmares_n_3274345.html)). After the initial wave of fake Yelp reviews in response to this episode (and the owners' insane reactions), users have continued to leave reviews on Yelp that are a direct result of the show.

After looking through Yelp, I speculate that reviews for Amy's Baking Company can be split into four groups:

+ Type 0: Real reviews that are not influenced by the show
+ Type 1: Legitimate reviews by people who visited the business after hearing about it on the show
+ Type 2: Reviews by people who visited the business before watching the show but left reviews after, either in support or against it. While their initial impressions of the bakery might not have been influenced by the show, their review is in response to it.
+ Type 3: Fake reviews by people who have never been to the bakery

### Assumptions:
+ All reviews left before the first airing of the show (May 10, 2013) are legitimate (Type 0)
+ Yelp has already filtered out most fake reviews (Type 3)
+ Reviews by users who have reviewed other businesses near Amy's Baking Company are likely to be real (types 1 or 2)
+ Reviews from locals are not more likely to be real than those from non-locals (and vice versa)

### Other thoughts:
+ There is likely an uptick of fake reviews after the follow-up episode (April 11, 2014)
+ Reactive or fake reviews (types 2 or 3) might have extreme ratings (1 star or 5 stars)
+ Yelp might have preferentially removed 1 star ratings, assuming that they were fake. Remaining fake reviews might have more 1.5 or 2 star ratings than expected.


## Methods:
+ Scrape all Yelp reviews for Amy's Baking Company
+ For each user that left a review, scrape their other reviews
+ Geocode each business
+ For each user, use Kernel Density Estimation to create a heatmap of their reviews
+ Calculate the distance between the center of review activity for each user and Amy's Baking Company
+ ?

