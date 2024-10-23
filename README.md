# Project3_Udacity
# Project: STEDI Human Balance Analytics
# Landing Zone
    Criteria	Submission Requirements
    Use Glue Studio to ingest data from an S3 bucket
    
    customer_landing_to_trusted.py, accelerometer_landing_to_trusted.py, and step_trainer_trusted.py Glue jobs have a node that connects to S3 bucket for customer, accelerometer, and step trainer landing zones.
    
    Manually create a Glue Table using Glue Console from JSON data
    
    SQL DDL scripts customer_landing.sql, accelerometer_landing.sql, and step_trainer_landing.sql include all of the JSON fields in the data input files and are appropriately typed (not everything is a string).

    Use Athena to query the Landing Zone.

    Include screenshots showing various queries run on Athena, along with their results:
    
    Count of customer_landing: 956 rows
    The customer_landing data contains multiple rows with a blank shareWithResearchAsOfDate.
    Count of accelerometer_landing: 81273 rows
    Count of step_trainer_landing: 28680 rows
# Trusted Zone
    Criteria	Submission Requirements
    Configure Glue Studio to dynamically update a Glue Table schema from JSON data
    
    Glue Job Python code shows that the option to dynamically infer and update schema is enabled.
    
    To do this, set the Create a table in the Data Catalog and, on subsequent runs, update the schema and add new partitions option to True.
    
    Use Athena to query Trusted Glue Tables
    
    Include screenshots showing various queries run on Athena, along with their results:
    
    Count of customer_trusted: 482 rows
    The resulting customer_trusted data has no rows where shareWithResearchAsOfDate is blank.
    Count of accelerometer_trusted: 40981 rows
    Count of step_trainer_trusted: 14460 rows
    Filter protected PII with Spark in Glue Jobs
    
    customer_landing_to_trusted.py has a node that drops rows that do not have data in the sharedWithResearchAsOfDate column.
    
    Hints:
    
    Transform - SQL Query node often gives more consistent outputs than other node types.
    Glue Jobs do not replace any file. Delete your S3 files and Athena table whenever you update your visual ETLs.
    Join Privacy tables with Glue Jobs
    
    accelerometer_landing_to_trusted.py has a node that inner joins the customer_trusted data with the accelerometer_landing data by emails. The produced table should have only columns from the accelerometer table.
    
# Curated Zone
    Criteria	Submission Requirements
    Write a Glue Job to join trusted data
    
    customer_trusted_to_curated.py has a node that inner joins the customer_trusted data with the accelerometer_trusted data by emails. The produced table should have only columns from the customer table.
    
    Write a Glue Job to create curated data
    
    step_trainer_trusted.py has a node that inner joins the step_trainer_landing data with the customer_curated data by serial numbers
    
    machine_learning_curated.py has a node that inner joins the step_trainer_trusted data with the accelerometer_trusted data by sensor reading time and timestamps
    
    Hints:
    
    Data Source - S3 bucket node sometimes extracted incomplete data. Use the Data Source - Data Catalog node when that's the case.
    Use the Data Preview feature with at least 500 rows to ensure the number of customer-curated rows is correct. Click "Start data preview session", then click the gear next to the "Filter" text box to update the number of rows
    As before, the Transform - SQL Query node often gives more consistent outputs than any other node type. Tip - replace the JOIN node with it.
    The step_trainer_trusted may take about 8 minutes to run.
    Use Athena to query Curated Glue Tables
    
    Include screenshots showing various queries run on Athena, along with their results:
    
    Count of customer_curated: 482 rows
    Count of machine_learning_curated: 43681 rows
    Hint: If you retrieve too many rows, consider dropping duplicates using the Transform - SQL Query node with the SELECT DISTINCT query.
