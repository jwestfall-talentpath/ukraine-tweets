This will extract data from the Twitter API from #UkraineRussianWar and sort them by source url, full text of the tweet, and when the tweet was created using PySpark.

It will then filter out retweets then append to an existing data store.

Pipeline:

Extract from Twitter API using AWS Glue and a Cloudwatch Trigger (once a day collecting last 24 hours of tweets)

Store in S3 Staging Bucket

Use AWS Glue with a CloudWatch trigger to filter out retweets then put in S3 bucket with filtered data if Staging Bucket has data.  Once that is completed, it will delete data from the Staging Bucket

Use AWS Lambda to extract existing data from AWS RDS and the data in the Filtered Bucket.  It would push both data sets to the S3 combination bucket.  The trigger would be when data is in S3 Filtered Bucket.  

Use AWS Lambda to check for duplicate tweets in both datasets and remove duplicates from the filtered dataset.  Once removed, it would append the filtered data into the AWS RDS.  Both datasets would then be deleted from the S3 Combination Bucket.


Data:  1 table: Full_text of Tweet, source url, when created

File size: Around 212k for an hour of tweets, might be around 5M per day of filtered tweets
