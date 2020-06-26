## Relational Databases and Mapping

![](images/BIOTECH.png)

This project primmarily dealt with creating a **unique key** build a relationship between an **Excel** spreadsheet and a **Redshift data pull via SQL**. Because the two datasets were from different data sources, consolidating them required cleaning and cross-functional collaboration. To make the unique key the following actions were performed in the **query editor**:
* deleting duplicate records
* deleting blanks 
* merging datasets
* unpivoting columns

Unpivoting the columns doupled/tripled all records in the merged dataset, incorrectly inflating revenue. As a result, I divided the acutals by 2 or 3 depending on if they were doubled or tripled. This was done with the code below:

    NewRevenue = 
    MergeData[Revenue]/ 
    CALCULATE ( DISTINCTCOUNT(MergeData[Attribute]) , ALLEXCEPT(MergeData , MergeData[Customer_Name]))

This measure was then used to create other measures such as quarter-to-date revenue and prior year growth.
