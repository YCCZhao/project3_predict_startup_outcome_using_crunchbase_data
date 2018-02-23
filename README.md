# Predict Startup Outcome Using Startup Categoryand Founder Education Info
For this project I used JSON files of company data and of person data from Crunchbase to predict if a startup has successfully raised money, been acquired, launched IPO, or been deadpooled. The data I used is as of 12/11/2012, and obtained from (here)[http://www.cs.cmu.edu/~guangx/crunchbase.html#maprediction]
 
## Data Cleaning
* THe original dataset I obtained is nearly 1GB, therefore the early stage data cleaning and EDA were performed on AWS.

* Original data is in a very nested JSON format. For example: A JSON file of a compnay  has basic company information, list of people that have relationship with, list of funding rounds, list of milestones, and etc. I had to extract and flatten the information to transform them into tables and created relational database (normalized). At the end, I have tables of companies, persons, relationships between compnaies and persons, milestones, aquisitions, IPOs, education degrees.

* After I have the relational database, I didn't put them in a SQL server, simply because I ran out of time. I save them in pickle files and load them when analyzing.

* The relational "database" allowed me to join the tables to perform some EDA and extract features. After joining company, person, and relationship tables, I dropped all the companies that don't have founders associated with. Using agreggation I was also able to extract how many female/male/total founders a startup has and on average how many startups founders founded including this one. (Note that crunchbase doesn't provide the gender infomation, I extracted it from the person overview based on pronouns used.) Then I also added education information. From that I was able to extract the average education degree levels of founders, and what education background they are from. 


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
