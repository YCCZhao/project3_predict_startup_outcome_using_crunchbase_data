# Predict Startup Outcome Using Startup Categoryand Founder Education Info
For this project I used JSON files of company data and of person data from Crunchbase to predict if startups have successfully raised money, been acquired, launched IPO, or been deadpooled. The data I used is as of 12/11/2012, and obtained from (here)[http://www.cs.cmu.edu/~guangx/crunchbase.html#maprediction]
 
## Data Cleaning
* THe original dataset I obtained is nearly 1GB, therefore the early stage data cleaning and EDA were performed on AWS.

* Original data is in a very nested JSON format. For example: A JSON file of a company has not only basic company information, but also list of people that have relationship with, list of funding rounds, list of milestones, and etc. I had to extract and flatten the information, and transform them into tables and create relational database (normalized). At the end, I have tables of companies, persons, relationships between compnaies and persons, milestones, aquisitions, IPOs, education degrees.

* After I had the relational database, I didn't put them in a SQL server, simply because I ran out of time. I save them in pickle files and load them when analyzing.

* The relational "database" allowed me to join the tables to perform some EDA and extract features. After joining company, person, and relationship tables, I dropped all the companies that don't have founders associated with. Using agreggation I was also able to extract how many female/male/total founders a startup has and on average how many startups founders founded including this one. (Note that crunchbase doesn't provide the gender infomation, I extracted it from the person overview based on pronouns used.) Then I also added founder education data. From that I was able to extract the average education degree levels of founders, and what education background they are from. 


## EDA
* The data was extremely messy. For founder degree type alone, there are nearly 3000 unique values. Most of them refers the same degree type (ex: Bachelor’s Degree), however there are multiple spelling. Similar situation for founder education background. 

* There are more than 100k companies in the crunchbase database, however majority of them are missing information. At the end I had about 3800 companies for my classification models. 

* For this project I didn’t include startups that haven't been successfully raised money, because I couldn’t be sure if they haven’t indeed raised money or database hadn't been updated.


## Classification Models
* I used 10 fold cross validation to tune the hyper parameters of my KNN and logistic regress models. I also fitted them using following sets of features to see which sets of feature provide the best accuracy.

 1. Number of founders (cardinal) + Number of female founders (cardinal) + Number of male founder (cardinal) + Nth startup (cardinal)
 2. Founder Education Degrees (category)
 3. Education Degrees (ordinal)
 4. Founder Education Background (category)
 5. Categories (category)
 6. Number of founders (cardinal) + Number of female founders (cardinal) + Number of male founder (cardinal) + Nth startup (cardinal) + Founder Education Degrees (ordinal) + Founder Education Background (category)
 7. Categories (category) + Number of founders (cardinal) + Number of female founders (cardinal) + Number of male founder (cardinal) + Nth startup (cardinal)
 8. Categories (category) + Founder Education Degrees (ordinal) + Founder Education Background (category)
 9. Categories (category) + Number of founders (cardinal) + Number of female founders (cardinal) + Number of male founder (cardinal) + Nth startup (cardinal) + Founder Education Degrees (ordinal) + Founder Education Background (category)

## Results
* In general all features provide higher model accuracy and KNN provides higher model accuracy. The fact that KNN performs better hinted me that the features have some interaction, especially between founder education information. Unfortunately I didn’t have enough time to add more interaction terms.

* Final accuracy is 51%. At this point I realized I should have used precision to validate models. It's ok to miss companies, at the end there are only limited number of companied one can invest in, but it's optimal if we get our prediction right so we don't loss money on investments. 

* I also used decision tree to obtain feature importance. It’s interesting that it gave me different important features from logistic regression. I would like to look into the reason behind this in the future.
