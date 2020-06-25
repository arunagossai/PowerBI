## Relational Databases and Mapping

![](images/BIOTECH.png)

This project primmarily dealt with creating a **key** build a relationship between an **Excel** spreadsheet and a data table pulled **via SQL**,
Because the two datasets were from different data sources, consolidating them required cleaning prior and cross-functional collaboration.
One feature utilized within the **query editor** in Power BI was unpivoting/pivoting columns. This doupled or tripled records which
incorrectly inflated revenue. As a result, I divided the acutals by the appropriate amount, shown in the code below:

    Revenue = 
    Merge1[Amount P$]/ 
    CALCULATE ( DISTINCTCOUNT(Merge1[Attribute]) , ALLEXCEPT(Merge1 , Merge1[NSGN Name]))

This measure was then used to create other measures such as quarter-to-date revenue and prior year growth. 
