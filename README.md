# Client Project
### Utilizing social media to alert about new disasters

Notebooks in order of workflow:

1) [1_train-cleaning-preprocessing.ipynb] (./1_train-cleaning-preprocessing.ipynb)
2) [2_Data_Gathering_Twitter_API.ipynb] (./2_Data_Gathering_Twitter_API.ipynb)
3) [3_train-modeling-evaluation.ipynb] (./3_train-modeling-evaluation.ipynb)
4) [4_Alert_Map_Bokeh_Final.ipynb] (./44_Alert_Map_Bokeh_Final.ipynb)

[Client_Project_Presentation.pdf] (./Client_Project_Presentation.pdf)

This project was developed by:

Sidd Nirmal and
Krista Johnson

**Problem Statement:**
FEMA has requested a demo of an emergency alert system for a large metropolitan area based on social media “reporting.” Twitter provides a live feed to what’s happening around the Greater New York region before many emergencies even get reported. We need to utilize this of-the-minute information to alert FEMA of a potential emergency as well as where it’s approximately located.

**Executive Summary**
*Gathering Data*
Using a dataset of over 10,000 disaster-related tweets marked as either "relevant" or "not relevant", we trained a model using NLP to classify tweets as such and get an initial benchmark. We also researched and took into a consideration, a lexicon of disaster terms to help classify tweets as it's better to cast a wider net and not miss an emergency that could potentially harm many people. These datasets were used to train our models while we worked on creating a developer account through Twitter to pull real-time tweets. 
While we had gone back and forth with Twitter to get the account approved we tried using TwitterScraper, which has been used by a number of groups in the past. However, due to Twitter's updated policies TwitterScraper is no longer able to scrape any tweets from the site. Once we received authorization from Twitter we were able to pull upwards of 4,800 real-time tweets based on a range of latitude and longitude. Due to users having geo tags turned on or off, Twitter only provides the tweets and not each individual tweet's exact location. Therefore, we had to write code that assigned a specific latitude and longitude to each tweet so it could be a point on our map. 

*EDA*
Since the initial training data was clean we had to focus on cleaning the real-time tweets that were pulled via the Twitter developer account. Every tweet that was pulled had a "b'" in front of it which we removed since it didn't have any significance. We also lemmatized the tweets to group together the inflected forms of each word so they can be analyzed as a single item. This way we could analyze the top "emergency" terms that signal a real emergency from a tweet that doesn't need to get FEMA's attention. 

*Modeling and Analysis*
As we modeled our initial training data, were were able to get upwards of 90% for both our logistic regression and random forest models. We used pipeline gridsearch for both models to make sure we were tuning and optimizing both models based on their parameters. Initially, we had limited features for random forest which gave us a score of around 54%, however when we revised this to barely limit the features the score raised significantly. 
We also revised our lexicon of emergency terms and created a list of stopwords. These stopwords aimed to help us differentiate between disasters or emergencies that are happening at that moment versus ones that are being reported on or that happened in the past. An example of this could be tweeting about the "anniversary" of an emergency or asking for "donations" for a disaster. 

**Conclusion**
After running our models we found that logistic regression consistently ran better than random forest so we would continue to tune that model if we were to move forward creating this alert system. We also found that because of the nature of social media and how it's an open source that anyone can post to, there's a lot of variance in how people talk about (or the type of language they use) to talk about potentially serious disasters. For example, one of our most frequent disaster terms after terms like "flood", "tornado" etc. was the word "lol". This is an interesting find since one would think all posts about serious disasters would reflect a serious tone. After even more research we found that the term "sharknado" when used as a stopword to take out any non-emergency tweets actually hurt our accuracy by 2%. When we researched this we found a large number of tweets where people used this term as a hashtag to post about real tornado warnings. 

**Next Steps and Recommendations**
Overall, even though we are confident with our scores that our model is able to classify a relevant emergency tweet, we do suggest that there is a necessary human-element needed to review the threat and make sure we don't waste any resources going after false claims. Again, social media is to be taken with a grain of salt since anyone can post whatever they want to their own profile. 
A way to help mitigate the need to go through every tweet that gets flagged would be to create a threshold, so that an alert would go off when 200 tweets (for example) are all flagged in a certain range of latitude and longitude it will be seen as more credible of a threat. 

**References**
Twitter data with permission by Twitter. [developer.twitter.com]
CrisisLex: dowloading a crisis term lexicon. [https://crisislex.org/crisis-lexicon.html]
ScienceAdvances (2016, March, 11). "Rapid assessment of disaster damage using social media activity'. [https://advances.sciencemag.org/content/2/3/e1500779.full]
Twitter. (2013, Sept 25). "Introducing Twitter Alerts". [https://blog.twitter.com/official/en_us/a/2013/introducing-twitter-alerts.html]
Streaming With Tweepy. [http://docs.tweepy.org/en/v3.4.0/streaming_how_to.html]