
# Applied Data Analytics

## Wedge Project

The notorious Wedge Project certainly lives up to its reputation for being exceptionally challenging. As noted in the introduction, engineering the data into a usable format requires "a deep understanding of data pipelines and how raw data is transformed into consumable data" — an essential skill for a successful career, but also crucial for navigating this project. I’ve been thoroughly humbled by the process. To be honesst I have never felt entirely confident, let alone proud, of my abilities in this area. This experience has left me feeling a lot of respect for those who possess the expertise highlighted above.


### Task 1

* Files for this task: 
(task-1.ipynb)

Requirements of Task 1:  In this task, you’ll upload all Wedge transaction records to Google Big Query. You’ll want to make sure that the column data types are correctly specified and that you’ve properly handled the null values.

This file (at the 'B' level) defines the project and dataset details and sets up the cleaned files to be loaded to Big Query as 'wedge_B'. I was repeatedly getting errors from the 'memType' column, so I inspected the data types of the values in 'memType', and replaced NaN and empty strings with 'Unknown' which seemed to fix the issue. I also converted 'datetime' column to datetime type, and filled NaN values in numeric columns (if they existed). Additionally, I chose to drop unnecessary columns. After these steps, and the GBQ project and dataset details had been configured, the next steps were taken. 
1. Get all of the file names
1. Read in each file one at a time
1. Define table name
1. Upload data

(task-1A.ipynb)
This file was my attempt at Task 1 at the 'A' level. I did not succeed in getting the files uploaded to GBQ and ultimtaley ran out of time. It appeared to process the files, but the upload failed with errors like: 400 Error while reading data, error message: CSV table encountered too many errors, giving up. Rows: 100; errors: 100. Perhaps this is also an indication of file processing errors as well.  


### Task 2

* Files for this task: 
(task-2.ipynb)

Requirements: This task asks you to generate a file of owners where the file contains every record for each owner. There will be more than one owner in the file, and I do not want you to include card_no==3, which is the code for non-owners. The size of the sample is up to you, but I’d recommend shooting for a sample that’s around 250 MB.
Loads all data into GBQ data set.

What my code does:
1. Connect to BigQuery and Query Data:
The code connects to a Google BigQuery project using the bigquery.Client.
It runs a query to select all transaction data where card_no = 25220 from the transArchive_* table.
The result is loaded into a pandas dataframe, which is saved to a CSV file.
2. Filtering Data: The code filters out transactions with return or void statuses ('R' and 'V'). The filtered results are saved to a new CSV file. The size of this filtered CSV file is calculated and printed (0.21 MB).
3. Random Sample of Owners: It runs another query to select a random sample of 615 owners (card_no) who have less than or equal to 99,000 transactions, excluding non-owners (card_no = 3). This sample is stored in a dataframe and converted to a list of integers.
4. Querying Transactions for Sampled Owners: Using parameterized queries, the code fetches all transaction records for the sampled owners, excluding return and void transactions.
The query results are saved to a CSV file, and the number of records (1,249,151) is printed. The size of this CSV file is calculated and printed (284.22 MB).
I felt this was within a reasonable limit of 250 MB.

	

### Task 3

* Files for this task: 
(task-3.ipynb)
(sales_summary.db)

Requirements: Build a single SQLite database via Python (in a .db file) containing three tables.

My file script queries transaction data from Google BigQuery, processes it into three separate datasets, and then stores them into a local SQLite database for further analysis.

1. Sales by Date and Hour: The first query retrieves total sales, distinct transactions, and item counts (accounting for returns/voids) by date and hour, excluding certain departments and non-owner transactions. The results are stored in a pandas DataFrame (df_1).
2. Sales by Owner by Year by Month: The second query extracts sales data by owner, grouped by year and month, calculating total sales, distinct transactions, and items for each owner, while excluding non-owner transactions and certain departments. The result is saved in another DataFrame (df_2).
3. Sales by Product Description by Year by Month: The third query retrieves sales data for each product (by UPC), grouped by product description, department, year, and month, with the same exclusions. The result is stored in DataFrame (df_3).

The three DataFrames are inserted into an SQLite database as three separate tables: sales_by_date_by_hour, sales_by_owner_by_year_by_month, and sales_by_product_description_by_year_by_month. Each table is written to the database with a confirmation message printed upon successful insertion.


## Query Comparison Results

Fill in the following table with the results from the 
queries contained in `gbq_assessment_query.sql`. You only
need to fill in relative difference on the rows where it applies. 
When calculating relative difference, use the formula 
` (your_results - john_results)/john_results)`. 



|  Query  |  Your Results  |  John's Results | Difference | Rel. Diff | 
|---|---|---|---|---|
| Total Rows  |  85760139 |  85760139 | 0  |  0 |
| January 2012 Rows  | 988998  | 988998  |  0 |  0 |
| October 2012 Rows  | 1042287  | 1042287  |  0 |  0 |
| Month with Fewest  |  12 |  12 | Yes/No  | NA  |
| Num Rows in Month with Fewest  |  988998 |  988998 |  0 | 0  |
| Month with Most  | 4  |  4 | Yes/No  | NA  |
| Num Rows in Month with Most  |  1135000 |  1135000 | 0  |  0 |
| Null_TS  |  7123792 |  7123792 |  0 |  0 |
| Null_DT  |  0 | 0  | 0  | 0  |
| Null_Local  | 234843  | 234843  |  0 | 0  |
| Null_CN  |  0 | 0  |  0 |  0 |
| Num 5 on High Volume Cards  | 14987  |  14987 | Yes/No  | NA  |
| Num Rows for Number 5 | 460630  | 460630  | 0  |  0 |
| Num Rows for 18736  | 12153  |  12153 | 0  |  0 |
| Product with Most Rows  | banana organic  |  banana organic | Yes/No  | NA  |
| Num Rows for that Product  | 908639  | 908639  | 0  | 0  |
| Product with Fourth-Most Rows  | avocado hass organic  |  avocado hass organic | Yes/No  | NA  |
| Num Rows for that Product  |  456771 |  456771 | 0  | 0  |
| Num Single Record Products  | 2769 | 2769  | 0  | 0  |
| Year with Highest Portion of Owner Rows  | 2012 | 2012 | Yes/No  | NA |
| Fraction of Rows from Owners in that Year  | 0.7418  | 0.7418  | 0  |  0 |
| Year with Lowest Portion of Owner Rows  | 2017  | 2017  | Yes/No  | NA |
| Fraction of Rows from Owners in that Year  | 0.7513  |  0.7513 |  0 |  0 |


## Reflections

There was quite a bit of ambiguity with this project. I suspect this was intentional, as the real world often presents similar uncertainty, and part of the challenge is learning how to work through it. As suggested, I began with Task 3 before moving on to Tasks 2 and 1. However, this approach didn't offer as much clarity as I would have like, and in hindsight, I would have started with Task 1. I believe doing so would have given me a stronger foundation for understanding the dataset and tackling the later tasks more effectively.

While I contracted for an 'A' in this class, given the difficulties I faced during this project, I’ll be content with a 'C'. I gave it my best effort with the time I had available, which was limited due to several unforeseen challenges in my personal life.
