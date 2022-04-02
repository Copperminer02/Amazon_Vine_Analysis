# Amazon_Vine_Analysis

## Overview

Amazon Vine's has requested analysis of member reviews for products purchased by Amazon Vine Members.  Particularly, Amazon Vine would like to know if reviews performed by Vine members are biased and are more favorable than non-member reviews.  

This analysis focusses on US reviews for the Musical Instruments category.

## Resources

### Data

  * **Amazon Data** - ***url = "https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Musical_Instruments_v1_00.tsv.gz"***

### Software/Programming Languages

  * Google Colab Notebooks
  * PostgresSQL/postgresADMIN
  * Spark/pySpark version 3.0.1
  * Jupyter Notebook/ python pandas
  * AWS database server

### Files

  * **Amazon_Reviews_ETL.ipynb** - google colab notebook.  Accesses Amazon Data, transforms and saves into dataframes, connects to postgresSQL, and saves dataframes into 4 tables into postgresSQL via AWS server.
  * **Images/ images postgresSQL tables**
    1. customer_table - contains customer id  versus count of customer reviews by that id
    
    ![customers_table](https://user-images.githubusercontent.com/91850824/161400611-58a9a52b-ffdc-46ad-98de-443d92723fac.png)

    2. products_table - product_id compared to product title
    ![products_table](https://user-images.githubusercontent.com/91850824/161400616-52fa4780-48a4-4722-acfc-e5693c5ffef2.png)

    
    3. review_id_table - review number, customer id, product id, product parent, review_date
    ![review_id_table](https://user-images.githubusercontent.com/91850824/161400619-5d049ef1-a799-43be-9149-1234b55daab1.png)

    
    4. vine_table - contains purchase review information with vine membership information
    ![vine_table](https://user-images.githubusercontent.com/91850824/161400624-5ea97155-f48a-4572-92ca-9e378598d1b3.png)

  * **Resources/vine_table.csv** - csv output from postgresSQL for vine_table
  * **Vine_Review_Analysis.ipynb** - jupyter notebook that transforms vine_table.csv creates and manipulates dataframs to calculate positive review and 5-star ratings by vine members and non-members

## Analysis

The prupose of this analysis is to analyze the chosen amazon review datasets and compare the favorible product results for vine members to non members.  Particularly, the 5 star reviews were sorted, counted and compared to all favorible reviews with over 20 votes, and whose helpful_votes made up at least 50% of all votes for the review.

The dataset for amazon musical intruments was chosen for review.  First, with via colab notebook **Amazon_Reviews_ETL.ipynb**, a spark session is started and the dataset was read into the notebook.
![image](https://user-images.githubusercontent.com/91850824/161400968-e6cd9dec-476d-4a14-a00d-6011d7cad51c.png)

From the main dataframe, 4 more dataframes were created, and saved to a AWS RDS database.
![image](https://user-images.githubusercontent.com/91850824/161401001-1765f742-c1d4-4672-8c58-8055fe361695.png)
![image](https://user-images.githubusercontent.com/91850824/161401007-dae5d467-ab5f-45be-b58d-0271c026b732.png)
![image](https://user-images.githubusercontent.com/91850824/161401014-82fb615e-68f2-44c2-a922-ea133bcd0051.png)
![image](https://user-images.githubusercontent.com/91850824/161401017-5a9cf4ed-9bce-4f56-bcf2-d07951dbe75f.png)

Using postgresADMIN, the 4 tables were imported into postgresSQL, and the **vines_table** was exported as a csv file for further analysis.  

In jupyter notebook, the vine_table.csv was imported as dataframe.
![image](https://user-images.githubusercontent.com/91850824/161401531-fab60877-1e76-400c-bafb-f280b9bf55dd.png)

The dataframe was paresed to show only reviews with 20 or more votes:
![image](https://user-images.githubusercontent.com/91850824/161401548-a8e31486-34a3-4175-8073-2f496e6ce124.png)

From the parsed dataframe, another dataframe was created.  The third dataframe kept reviews with a helpful_vote to total_vote ratio greater than 50%.  

![image](https://user-images.githubusercontent.com/91850824/161401659-e7498f92-9e9b-481f-aeb1-a3a2ac4540dd.png)

From this final dataframe and for member and non-member categories,  the total reviews were counted, the 5-Star reviews were counted, and the percent of 5 Star reviews to all reviews was caclulated.
![image](https://user-images.githubusercontent.com/91850824/161401741-536c6806-178d-4cdd-8e6d-10dd6614f4b2.png)
![image](https://user-images.githubusercontent.com/91850824/161401743-aa15c10c-945c-48fb-bf9c-09dc30e13633.png)

## Results

1.  There were 60 reviews from Vine Members compared to 14,477 Non-members.
2.  Vine Members had 34 5-star reviews compared to Non-Member 8,122.
3.  5-Star reviews made up 56.7% of all Vine Member reviews compared to 56.7% of all Non-Vine Member reviews.

## Summary









