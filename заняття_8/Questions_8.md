# Lesson 8. AWS Certified Cloud Practitioner Practice Questions

### 1. Which AWS service is best suited to storing shopping carts when an application needs fast access to items by user ID?

- [ ] A. Amazon Athena
- [ ] B. Amazon DynamoDB
- [ ] C. Amazon Redshift
- [ ] D. Amazon QuickSight

### 2. Which components make up a composite primary key in a DynamoDB table?

- [ ] A. A partition key and a sort key
- [ ] B. A table name and an attribute name
- [ ] C. A primary key and a foreign key
- [ ] D. A Region and an Availability Zone

### 3. A DynamoDB table uses userId as its partition key and productId as its sort key. What can a Query operation return when you specify only the userId?

- [ ] A. All items in that user's shopping cart
- [ ] B. All users' items with a particular productId
- [ ] C. A SQL JOIN with the products table
- [ ] D. A new primary key for the table

### 4. Which DynamoDB capacity mode is suitable for a new application with unpredictable request volume when the team does not want to set read and write throughput in advance?

- [ ] A. Provisioned capacity without auto scaling
- [ ] B. On-demand capacity
- [ ] C. Amazon EC2 Spot Instances
- [ ] D. Amazon Redshift Serverless

### 5. CSV log files are already stored in an Amazon S3 bucket. An analyst wants to run an occasional SQL query against those files without creating a cluster. Which service should they choose?

- [ ] A. Amazon RDS
- [ ] B. Amazon DynamoDB
- [ ] C. Amazon Athena
- [ ] D. Amazon ElastiCache

### 6. Which statement about Amazon Athena is correct?

- [ ] A. It is a managed relational database for application transactions.
- [ ] B. It can run SQL queries against data in Amazon S3 without server management.
- [ ] C. It requires an EC2 cluster to be started before every query.
- [ ] D. It stores all data only in DynamoDB tables.

### 7. A company regularly analyzes large amounts of historical sales data with complex SQL queries and BI reports. Which service best fits this data warehousing workload?

- [ ] A. Amazon Redshift
- [ ] B. Amazon DynamoDB
- [ ] C. Amazon Route 53
- [ ] D. Amazon ElastiCache

### 8. What does Amazon Redshift Serverless allow you to do?

- [ ] A. Manage the nodes of a Redshift cluster yourself in every deployment.
- [ ] B. Run analytics without configuring and managing a provisioned data warehouse cluster.
- [ ] C. Convert Redshift into a key-value NoSQL database.
- [ ] D. Store all data automatically and exclusively in DynamoDB.

### 9. Which pairing of requirement and service is correct?

- [ ] A. Fast access to an item by key → DynamoDB; occasional SQL queries against S3 files → Athena
- [ ] B. Fast access to an item by key → Athena; occasional SQL queries against S3 files → DynamoDB
- [ ] C. Fast access to an item by key → Redshift; DNS → Athena
- [ ] D. BI reports on historical data → Route 53; shopping carts → Redshift

### 10. Which service should you choose to build a centralized analytics data warehouse for SQL queries across large datasets?

- [ ] A. Amazon Redshift
- [ ] B. Amazon SQS
- [ ] C. Amazon DynamoDB
- [ ] D. Amazon CloudFront

## Homework practice — 25 questions

### 11. What type of database is Amazon DynamoDB?

- [ ] A. A managed NoSQL database for key-value and document data
- [ ] B. A PostgreSQL-only relational database
- [ ] C. Object storage for files
- [ ] D. A managed DNS service

### 12. What is an item in a DynamoDB table made up of?

- [ ] A. Attributes
- [ ] B. EC2 instances
- [ ] C. S3 buckets
- [ ] D. Availability Zones

### 13. A DynamoDB table has only a partition key. Which statement is correct?

- [ ] A. Two items can have the same partition key value.
- [ ] B. The partition key value uniquely identifies an item in the table.
- [ ] C. A sort key is required for every table.
- [ ] D. A primary key is optional.

### 14. Which DynamoDB feature lets you efficiently query items using a key other than the table's primary key?

- [ ] A. A secondary index
- [ ] B. An Amazon CloudFront distribution
- [ ] C. An EC2 Auto Scaling group
- [ ] D. An S3 lifecycle rule

### 15. How does DynamoDB determine whether an item is unique in a table with a composite primary key?

- [ ] A. By the combination of its partition key and sort key values
- [ ] B. By its sort key value alone
- [ ] C. By its number of attributes
- [ ] D. By the table's creation time

### 16. A team wants DynamoDB to automatically delete session items after they expire. Which feature should it use?

- [ ] A. Time to Live (TTL)
- [ ] B. An Amazon Athena workgroup
- [ ] C. Amazon Redshift Spectrum
- [ ] D. S3 Transfer Acceleration

### 17. An application needs local reads and writes in several AWS Regions using replicated DynamoDB tables. Which feature fits this requirement?

- [ ] A. DynamoDB global tables
- [ ] B. A DynamoDB sort key
- [ ] C. Amazon Athena views
- [ ] D. Amazon Redshift snapshots

### 18. Which DynamoDB feature can capture changes to items for further processing?

- [ ] A. DynamoDB Streams
- [ ] B. Amazon Route 53 health checks
- [ ] C. Amazon Redshift Query Editor
- [ ] D. AWS Direct Connect

### 19. A team wants to specify the read and write throughput for a DynamoDB table in advance. Which capacity mode should it choose?

- [ ] A. Provisioned capacity
- [ ] B. On-demand capacity
- [ ] C. S3 Standard
- [ ] D. Redshift Serverless

### 20. Which statement best describes the data structure of a DynamoDB table?

- [ ] A. Every item must have all the same non-key attributes.
- [ ] B. Every item must have the primary key attributes, but other attributes can vary.
- [ ] C. A table has no primary key.
- [ ] D. Each item can contain only one attribute.

### 21. In a typical Athena use case, where are the files being analyzed with SQL stored?

- [ ] A. Amazon S3
- [ ] B. Amazon Route 53
- [ ] C. AWS IAM
- [ ] D. Amazon CloudFront

### 22. Which description best fits Amazon Athena?

- [ ] A. Interactive SQL queries against data without managing server infrastructure
- [ ] B. Persistent storage for shopping carts with key-based access
- [ ] C. Management of a domain's DNS records
- [ ] D. Caching web pages at edge locations

### 23. Which service is commonly used as a metadata catalog for Athena tables?

- [ ] A. AWS Glue Data Catalog
- [ ] B. Amazon Route 53
- [ ] C. Amazon ElastiCache
- [ ] D. Amazon EC2 Auto Scaling

### 24. Which TWO approaches can reduce the amount of data scanned by Athena queries? (Choose **TWO**.)

- [ ] A. Partition the data in S3 and filter queries by those partitions.
- [ ] B. Use a columnar format such as Parquet instead of raw CSV files.
- [ ] C. Add more DNS records in Route 53.
- [ ] D. Enable EC2 detailed monitoring for the bucket.
- [ ] E. Move table metadata into a security group.

### 25. An analyst runs infrequent queries against logs in S3. Why might Athena be a good fit for this specific workload?

- [ ] A. It can query the data directly in S3 without setting up a data warehouse.
- [ ] B. It is a transactional database for shopping cart operations.
- [ ] C. It automatically creates a DNS record for each file.
- [ ] D. It requires a dedicated cluster for every query.

### 26. Which workload is Amazon Redshift primarily designed for?

- [ ] A. Analytics queries and reports across large datasets
- [ ] B. Serving static website files
- [ ] C. Processing every DNS query for a domain
- [ ] D. Storing IAM users' passwords

### 27. Which Amazon Redshift characteristic helps it analyze selected columns in large tables?

- [ ] A. Columnar data storage
- [ ] B. Image-only storage
- [ ] C. No support for SQL
- [ ] D. Use of partition keys only

### 28. Which service is best suited to SQL aggregations over many years of sales history in a data warehouse?

- [ ] A. Amazon Redshift
- [ ] B. Amazon DynamoDB
- [ ] C. Amazon Route 53
- [ ] D. Amazon SQS

### 29. A company wants to analyze data in Redshift without configuring or maintaining provisioned clusters. Which option should it choose?

- [ ] A. Amazon Redshift Serverless
- [ ] B. DynamoDB Streams
- [ ] C. Amazon Athena Data Catalog
- [ ] D. An Amazon RDS read replica

### 30. Which TWO statements about choosing a service are correct? (Choose **TWO**.)

- [ ] A. DynamoDB is suitable for fast key-based operations on application data.
- [ ] B. Athena is suitable for SQL analysis of files in Amazon S3.
- [ ] C. Redshift is primarily designed for DNS routing.
- [ ] D. DynamoDB is file storage for a static website.
- [ ] E. Athena requires you to manage cluster nodes before every query.

### 31. Which of the following statements is TRUE about inserting data into a DynamoDB table?

- [ ] A. All items in a table must have the same number of attributes
- [ ] B. You can insert items with different attributes into the same table
- [ ] C. You must insert all attributes defined in the table's schema for each item
- [ ] D. You can only insert string data types into DynamoDB tables

### 32. What is the relationship between a Primary Key and a Sort Key in an Amazon DynamoDB table?

- [ ] A. They uniquely identify each item when used in combination
- [ ] B. The Sort Key replaces the Primary Key
- [ ] C. They must be of the same data type
- [ ] D. They are always required together

### 33. What should you consider before deleting a DynamoDB table?

- [ ] A. The need for a backup of the data
- [ ] B. The table's partition key
- [ ] C. The table's write capacity units
- [ ] D. The table's read capacity units

### 34. Which operation is used to retrieve data from a DynamoDB table based on specific criteria?

- [ ] A. Scan
- [ ] B. Query
- [ ] C. Get
- [ ] D. Fetch

### 35. Which statement BEST describes the flexibility of adding attributes to items in a DynamoDB table?

- [ ] A. Attributes can be added only if they are defined in the table schema
- [ ] B. Attributes can be added only after modifying the table structure
- [ ] C. All items must have the same attributes as defined during table creation
- [ ] D. New attributes can be added to some items without affecting others
