# Amazon_Vine_Analysis

## Resources
- AWS RDS
- PGAdmin4
- PostgreSQL
- Google Collab
- Spark 3.2.1
- Java
- PySpark
- Data:  https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Video_Games_v1_00.tsv.gz 

## Project Overview

Analyzing Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

Picked a dataset containing gaming reviews and used PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Using PySpark determined whether a bias toward favorable reviews from Vine members existed in the dataset. 

Project consists of two technical analysis deliverables and a written report as follows:

Deliverable 1: Perform ETL on Amazon Product Reviews
Deliverable 2: Determine Bias of Vine Reviews
Deliverable 3: A Written Report on the Analysis 

## ETL on Amazon Product Reviews

Created an AWS RDS database with tables in pgAdmin, picking a dataset from the Amazon Review datasets (https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt), and extracted the dataset into a DataFrame. Transformed the DataFrame into four separate DataFrames that match the table schema in pgAdmin. Uploaded the transformed data into the appropriate tables and ran queries in pgAdmin to confirm that the data had been uploaded.

![review](https://github.com/PatriciaCB1/Amazon_Vine_Analysis/blob/main/Images/Review%20ID%20Table.png) 

![products](https://github.com/PatriciaCB1/Amazon_Vine_Analysis/blob/main/Images/Products%20table.png)

![customers](https://github.com/PatriciaCB1/Amazon_Vine_Analysis/blob/main/Images/Customers%20table.png)

![vine](https://github.com/PatriciaCB1/Amazon_Vine_Analysis/blob/main/Images/vine%20table.png)


## Determine Bias of Vine Reviews

Using knowledge of PySpark, etermined whether a bias toward favorable reviews from Vine members existed in the dataset. Determined if having a paid Vine review makes a difference in the percentage of 5-star reviews.

## Results

### Initial DataFrame
![initial dataframe](https://github.com/PatriciaCB1/Amazon_Vine_Analysis/blob/main/Images/Video%20Games%20Reviews%20DF.png)

How many Vine reviews and non-Vine reviews were there?

Cleaned / filtered the review data as follows:

- Filtered data to retrieve only rows where the total_votes count is equal to or greater than 20 to pick reviews that were more likely to be helpful and to avoid having division by zero errors

### Votes greater than or equal to 20

![Votes >= 20](https://github.com/PatriciaCB1/Amazon_Vine_Analysis/blob/main/Images/Votes%20%3E%3D%2020.png)

- Filtered data from the new DataFrame to create a further new DataFrame to retrieve all the rows where the number of helpful_votes divided by total_votes was equal to or greater than 50%.

### Helpful votes greater than or equal to 50%

![Helpful Votes >= 50%]

- Filtered the resulting DataFrame to create a third DataFrame hat retrieved all the rows where a review was written as part of the Vine program (paid), vine == 'Y'.

### Vine (paid)

![Vine YES]()

- Filtered the resulting DataFrame to create a third DataFrame hat retrieved all the rows where a review was written NOT as part of the Vine program (unpaid), vine == 'N'.

### Non-Vine (unpaid)

![Vine NO]()

Within the filtered DataFrame there were 40,565 reviews (94 paid + 40,471 unpaid)

![Paid V Non-paid Reviews]()

How many Vine reviews were 5 stars? - There were 48 Vine (paid) reviews that were 5 stars.

How many non-Vine reviews were 5 stars? - There were 15,663 non-Vine (unpaid reviews) that were 5 stars.

What percentage of Vine reviews were 5 stars? - 51% of Vine (paid) reviews were 5 stars.

What percentage of non-Vine reviews were 5 stars? - 39% of non-Vine reviews were 5 stars. 

## Summary

Given 51% of Vine (paid) reviews were 5 stars and only 39% of non-Vine reviews were 5 stars, there appears to be a bias of Vine having mor 5 start reviews.  


## Additional analysis recommended
- Would be best to look at how all rating levels compare instead of only 5 star
    - Top 2 box and Bottom 2 box would be interesting to understand 
