# Twitter Dataframe Wrangling - WeRateDogs

## Introduction
In this project I will be analyzing and visualizing the `tweet_archive` dataset of a Twitter user `@dog_rates`, also known as WeRateDogs. WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dogs. These ratings almost always have a denominator of 10 and the numerators however are always greater than 10. WeRateDogs has over 4 million followers and has received international media coverage.

This archive contains basic tweet data (tweet ID, timestamp, text, rating_numerator, rating_denominator e.t.c) for all 5000+ of their tweets as they stood on August 1, 2017.

### Libraries used
The following Python packages were used in the project-:
* pandas
* NumPy
* requests
* tweepy
* json
* matplotlib

# Steps taken in completing the project
This project was completed in three major steps, namely-:
1. Gathering Data
1. Assessing data
1. Cleaning data
1. Visualization and Analysis

## Step 1: Gathering Data
The data was used in this project was gathered from three sources which are-:
1. The WeRateDogs Twitter Enhanced archive which was provided by Udacity and was
manually downloaded to the local environment.
1. The Image Predictions data which was downloaded from the cloud hosted by Udacity
using the Python module called request.
1. Lastly, we used the tweet_id in the first data frame to extract extra relevant tweets data.
To extract data from the Twitter API a developer account was needed, which I signed up
for. After getting the keys and tokens I initiliased them and together with the Python’s
Tweepy module I was able to fetch the necessary data.


## Step 2: Assessing data
After gathering all the data and storing it on the local environment, I read the data to
dataframes using Python’s pandas module. After that, I went on to assess the data using
various Python’s pandas methods like head(), info(), value_counts(), duplicated(), describe()
and many more.

By using these methods, I was able to detect some quality and tidiness issues that my data
frames had, such as incorrect datatypes, missing data, invalid data, duplicates, unnecessary
columns etc.

### Quality and Tidiness Issues Discovered
#### 1. Quality issues
##### a. The enhaced dataframe
* From the `.info()` method I discovered that `tweet_id`, `in_reply_to_status_id`, `in_reply_to_user_id`, `retweeted_status_id`, and `retweeted_status_user_id` are not of the same type,even though they are all IDs. Most of them are floats and one of them is of integer type. They should all be converted to strings instead because there are no arithmetical operations that can be performed on them.
* Moreover the `retweeted_status_timestamp`, `timestamp` should be `date_time` type instead of `string`, because they represent time.
* Also, there are some columns with null objects that are non-null because they have a value of `None`. This will distort the dataframe when we are looking for null values.

* From the `value_counts` I discovered that the `name` column have inappropriate names e.g. `a`, and 745 `None` values. 
* I also observed that a total of 20 ratings do not have the denominator value as 10, which the denominator for many entries.


##### b. The image predictions dataframe
* The dataframe has 2075 rows which means there is data that is missing since the enhanced dataset has 2356 rows.
* The `tweet_id` is of integer type, thus should all be converted to strings instead because there are no arithmetical operations that can be performed on them.
* The `duplicated()` method revealed that there are duplicated `jpg_url` values, which suggests that 66 tweets has the same dog picture.
* Inconsistent formating of the predicted dog names, some are in lowercase others are separated by an underscore.
##### c. The Twitter API dataframe
* The `df_enhanced` dataset has `2356` rows and the `twitter_api` dataframe has 2342 entries, which means that 14 tweets could not be retrieved, because either the tweets were deleted or the Ids were invalid.
* The `tweet_id` is of integer type, thus should all be converted to strings instead because there are no arithmetical operations that can be performed on them.

#### 2. Tidiness
* The various stages of dogs in the four columns namely `doggo`, `floofer`, `pupper` and `puppo` should be merged to form one column.
* All the three dataframes should be part of a single dataset.

NB : We could add a column called jpg_url_api contain the query of the api media_url_https it will have the same result as the images dataset
We may want to add a gender column from the text columns in archives dataset

### Step 3: Cleaning data
After I have assessed the data, I started cleaning the issues discovered in the Assessing data
process. Some of the main data cleaning process I performed were-:
a. Changing data type of timestamps to datetime and IDs to strings.
b. Melting columns
c. Dropping columns which I fount not useful to my project
d. Changed all the 'None' values to Numpy’s NaN values.
e. At last I combined the three data frames to one single data frame.

### Step 4: Visualization and Analysis
After I gather all the data, assessed it and cleaned it I went on to analyze and visualize it to gain some insights from the data.
First I used the describe() method and I discovered that-: 
1. 75% of the dogs received a rating of 12 and below, and 
1. The most favorited post received 165 031 likes.

Secondly I used the value_counts() method to find the most common dog name. The result came out with six dog names with 10 appearances each.

Next I visualized the favourite and retweet counts for each dog stage, and the chart shows that
`puppo` were favorited a lot. However this is because the total count of `puppo` is greater than any other dog stage. Another noticeable thing , is that favorites are always greater than retweets for any dog stage.

## References 
1. [Twitter API - get tweets with specific id](https://stackoverflow.com/questions/28384588/twitter-api-get-tweets-with-specific-id) accessed on 20 June 2022.
1. [Handling Exceptions](https://wiki.python.org/moin/HandlingExceptions) accessed on 20 June 2022.
1. [Reading and Writing JSON to a File in Python](https://stackabuse.com/reading-and-writing-json-to-a-file-in-python/) accessed on 20 June 2022.


