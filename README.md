# Predict Startup Outcome Using Startup Categoryand Founder Education Info
For this project I used JSON files of company data and of person data from Crunchbase to predict if a startup has successfully raised money, been acquired, launched IPO, or been deadpooled. The data I used is as of 12/11/2012, and obtained from (here)[http://www.cs.cmu.edu/~guangx/crunchbase.html#maprediction]
 
## Data Cleaning
On AWS
JSON to SQL (DF in Pickel)
JOIN Data
Only Kept Founders
Extract Features
Categories (category)
Number of founders (cardinal)
Number of female founders (cardinal)
Number of male founder (cardinal)
Nth startup (cardinal)
Founder Education Degrees (category and ordinal)
Founder Education Background (category)


## EDA
100K to 1K
Imbalanced Dataset
6K don't have enough information (Excluded)
Only kept raised money, acquired, ipo, and dead


## Classification Models
Cross-validate KNN and Logistic Regression 

## Results
More features the better
KNN generally better
Using founder info only yields prettey good result.
Final model chosen is logistic over all features
