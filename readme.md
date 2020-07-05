Wrangle Report
Problem Statement:
Twitter data regarding the twitter user dog_rates has to be wrangled, analysed and visualized to gain insights about the data. Data had to be gathered by multiple sources such as twitter archive given as a .csv file, twitter API and Image prediction file obtained by accessing a URL provided. Gathered data needs to be accessed and cleaned as it is both dirty and messy. Only after cleaning, the data becomes worthy enough for analysing and subsequent visualizing.
This documentation consists of data wrangling steps used for gathering, assessing and cleaning twitter data of dog_rates user.
Data was gathered by multiple sources such as:
1.	Twitter_archive_enhanced given as a .csv file by Udacity and downloaded manually. Read into twitter_enhanced dataframe.
2.	Image_predictions.tsv file obtained by programmatically downloading the URL using the Requests library.  Read into images dataframe.
3.	Used tweet_json.txt file by manually downloading as Twitter Developer account couldn’t be set. Otherwise must have queried twitter API for each tweet’s JSON data using python’s Tweepy library and each tweet’s entire set of JSON data should have been stored in tweet_json.txt file. Read into tweet_json dataframe.
Quality issues and tidiness issues were noticed in  twitter_enhanced dataframe and following steps were taken for assessing and cleaning it:
Rows containing non null value for 'in_reply_to_status_id'  were dropped, as we are interested in original tweets not replies.
'timestamp' is object, must be in datetime format
'Source' column consists of <a= href> value, only text needs to be retained.
 'retweeted_status_id','retweeted_status_user_id','retweeted_status_timestamp' represents retweets, as we are interested in original tweets, not retweets, only null values of these columns are relevant for the analysis.
Rows with missing values for 'expanded_urls' were dropped.
Few rows having rating denominators that are not 10, those rows were not ignored in the analysis.
'name' column of twitter_enhanced consisted of invalid values such as the,a,an,such. It was noted that correct names are represented by starting Capital letter. Non capital letter beginning names were replaced by None.
'retweeted_status_id','retweeted_status_user_id','retweeted_status_timestamp', ‘in_reply_to_status_id' columns were dropped as they all contained only null values after cleaning.
Dropped 'text' column as it's not used in my analysis
Dropped the rows where dog type is null in the merged dataset.
doggo, floofer, pupper, puppo are stored as different columns, were brought together and put into one column - dog_stage_name
Value of denominator was 10 for all rows after cleaning. Rating was represented by a single column using numerator and denominator rating columns. 
Images_df had predicted dog type and confidence level spread across multiple columns. All the predicted dog type columns were brought under single column name dog_type. Same way, Confidence levels were also brought under a common name conf. Additional columns are dropped.
All 3 cleaned data frames were merged into twitter_combined_df and this cleaned file is downloaded as Master.csv