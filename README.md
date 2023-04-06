# Unit 22 Homework: Home_Sales
 I used SparkSQL to analyze home sales data. I used Spark to create temporary views, partition the data, cache and uncache tables.

## The Process
1. First, I initialized findspark to import pyspark. I created a `SparkSession` with pyspark, saved the url `https://2u-data-curriculum-team.s3.amazonaws.com/dataviz-classroom/v1.1.2/22-big-data/home_sales_revised.csv` with the data to a constant, and used SparkFiles to pull the csv in order to read it into a dataframe.

![alt text](https://github.com/glongo001/Home_Sales/blob/main/Images/1_home_sales_df.png)


2. I used `createOrReplaceTempView()` to create a temporary table called `home_sales`.

3. What is the average price for a four-bedroom house sold for each year? Round off your answer to two decimal places.
    - I extracted only the year from the `date` column with YEAR(`date`).
    - I calculated the average price of homes with 4 bedrooms grouped by year sold, and rounded to two decimal places with ROUND(AVG(`price`),2).
    - The results showed that the average price for 4 bedroom homes sold in 2019, 2020, 2021, and 2022 was about $300,000.

![alt text](https://github.com/glongo001/Home_Sales/blob/main/Images/3_datesold_4beds.png)

4. What is the average price of a home for each year it was built that has three bedrooms and three bathrooms? Round off your answer to two decimal places.
    - I calculated the average price of homes with 3 bedrooms and 3 bathrooms grouped by year built, and rounded to two decimal places with ROUND(AVG(`price`),2).
    - The results showed that the average price for a 3 bedroom and 3 bathroom house was the lowest for houses built in 2015 where the average was $288,770.3, and the highest was for houses built in 2013 with an average of $295,962.27. The average price did not change much based on year built.

![alt text](https://github.com/glongo001/Home_Sales/blob/main/Images/4_datebuilt_3beds_3baths.png)

5. What is the average price of a home for each year that has three bedrooms, three bathrooms, two floors, and is greater than or equal to 2,000 square feet? Round off your answer to two decimal places.
    - I calculated the average price of homes with 3 bedrooms, 3 bathrooms, 2 floors and 2,000 square feet or more, grouped by year built, and rounded to two decimal places with ROUND(AVG(`price`),2).
    - The results showed that the average price was the lowest for houses built in 2011 where the average was $276,553.81, and the highest was for houses built in 2012 with an average of $307,539.97. Overall, the average price did not change much based on year built.
    - The additional parameters, 2 floors and square feet of 2,000 or more, did not change the prices much but they increased the differences in prices of houses built each year. In the previous table the averages ranged from $288k-$296k and in the current table the averages ranged from $276k-$308k.

![alt text](https://github.com/glongo001/Home_Sales/blob/main/Images/5_datebuilt_3beds_3baths_2floors_2000sqft.png)

6. What is the "view" rating for homes costing more than or equal to $350,000? Determine the run time for this query, and round off your answer to two decimal places.
    - I calculated the average price of homes with a value of $350,000 or more, grouped by view rating, and rounded to two decimal places with ROUND(AVG(`price`),2).
    - The results showed that for the houses with less than 20 view ratings the price average was about $400,000.
    - The results showed that for the houses with more than 20 view ratings the price average was about $1,000,000.

![alt text](https://github.com/glongo001/Home_Sales/blob/main/Images/6_view_350000price.png)
![alt text](https://github.com/glongo001/Home_Sales/blob/main/Images/6_2_view_350000price.png)

7. I cached the temporary table `home_sales` and used `isCached()` to check that the table was cached.

8. Using the cached data, run the query that filters out the view ratings with an average price of greater than or equal to $350,000. Determine the runtime and compare it to uncached runtime.
    - The results showed that the cached runtime was significatly lower than uncached runtime. Cached runtime was about 0.52 seconds while uncached runtime was about 0.70 seconds

![alt text](https://github.com/glongo001/Home_Sales/blob/main/Images/9_view_350000price_cached.png)

9. I used `partitionBy()` to partition the data based on `date_built` and saved as parquet data. I created a temporary view for the parquet data.

10. Run the query that filters out the view ratings with an average price of greater than or equal to $350,000. Determine the runtime and compare it to uncached runtime.
    - The results showed that the uncached runtime was significatly lower than partitioned data runtime. Uncached runtime was about 0.70 seconds while partitioned data runtime was about 1.17 seconds

![alt text](https://github.com/glongo001/Home_Sales/blob/main/Images/13_view_350000price_parquet.png)

11. I uncached the `home_sales` table and used `isCached()` to verify that the table was uncached.

Source: Used https://sparkbyexamples.com/, and previous class assignments for reference.
