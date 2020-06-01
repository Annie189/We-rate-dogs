I. INTRODUCTION

Twitter user @dog_rates, also known as WeRateDogs. WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10. 
The datasets include three files:
•	Enhanced Twitter Archive
•	Image Predictions File
•	Data extraction from Twitter API

II. GATHER DATA
1.	Import necessary libraries
2.	Read datasets
Archive tweets
Image Predictions File
    Definition of the attributes:
•	p1 is the algorithm's #1 prediction for the image in the tweet
•	p1_conf is how confident the algorithm is in its #1 prediction
•	p1_dog is whether or not the #1 prediction is a breed of dog
•	p2 is the algorithm's second most likely prediction
•	p2_conf is how confident the algorithm is in its #2 prediction
•	p2_dog is whether or not the #2 prediction is a breed of dog etc


Data extraction from Twitter API
Data extraction from Twitter API provides data of retweet count and favorite count.

III. ASSESSING
Summary - Quality Issues
Archive tweet file
1.	Data is missing in the some columns: in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, etweeted_status_user_id, retweeted_status_timestamp, expanded_urls. 
2.	Duplicated data.This dataset includes retweets, which means there is duplicated data
3.	Wrong format. Source columns have HTML tags
4.	Wrong data type. Timestamp and retweeted_status_timestamp is an object instead of datetime
5.	Invalid Range: rating_numerator contains max value 1776 and rating_denominator contains max value of 17 rating_denominator is out of standard value of 10 
6.	Some of dogs have unnormal name such as 'None', or 'a', or 'an.' or 'O' or 'by' and some more lower case words as names
JSON file:
7.	Tweet ID is object instead of int64
Image file
8.	Inconsistent and wrong format of typing. Some are uppercase, some are lower case. Use "_" instead of  " ".
Summary - Tidiness Issues
df
1.	The variable for the dog's stage (dogoo, floofer, pupper, puppo) is spread in different columns
image_df
2.	This data set is part of the same observational unit as the data in the archive_df
df_tweet_json
3.	This data set is also part of the same observational unit as the data in the archive_df

IV. CLEAN DATA
Before cleaning data, the student would like to make a copy of dataset first.

Define- Code - Test
1. Remove unessentual attributes: in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id, and retweeted_status_timestamp
2. Removing HTML tags from source column
3. Delete retweets
4. Change the timestamp to correct datetime format
5. Dog ratings get standardized for denom of 10
6. Replace 'a', 'an', 'the', 'None' and other lower case words with NaN in name column
7. Convert the tweet_id in tweet_counts_clean into int64 type for merging
8. Create one column for the various dog types: doggo, floofer, pupper, puppo, 'doggo, puppo', 'doggo, pupper', 'doggo, floofer'
9 & 10. Merge the copied df_clean, image_df_clean, and tweet_json_clean dataframes

V. REPORT
There are 1969 rows and 24 columns in the dataset.
The student would like to investigate into the dataset regarding following questions:
-	Which are top frequent names?
-	How are average rating different among dog stages?
-	Which dog types are accurately predicted most?
-	What do people say in the review?

1.	Top frequent dog names

This is the top ten frequent dog names including: Charile, Lucy, Cooper, Tucker, Penny, Oliver, Sadie, Toby, Daisy and Winston. Among them, Charlie and Lucy are the two most popular names.

2.	Average Rating
Regarding average rating among dog stage, multiple stage (doggo, puppo) has the highest average rating (more than 12/10). Doggo and Floofer ranks second and third respectively.
3.	Dog Prediction
The student would like to investigate into dog prediction according to the first prediction. Step includes:
•	Identify top 10 most frequently predicted dog types
•	Among them, identify % correction prediction regarding prediction confidence > 0.5 and Prediction is True
Golden retriever, Laborador retriever and Pembroke are the top 3 most frequently predicted. Among top 10, Malmute is the least frequently predicted.
Among top 10 frequently predicted dog types, Golden retriever are the most frequently and correctly predicted. Pug this the name that ranks second regarding percent of correct prediction with 80% though there are only 55 times of predictions. Although Labrador retriever has high frequency of prediction, the percentage of accuracy is just around 68%.

4.	Text analysis
The student applied the NLP to identify top keywords are mentioned most in the review and which insights can be inferenced from. Reviews in general and those regarding pupper (the most popular dog stage in the dataset) are analyzed.
It seems that people always have a special feeling for dog and also take special care of them according to keyword analysis.
