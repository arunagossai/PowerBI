# Creating a Table with the Modeling Tab
![](/images/OPEX3.png)

To create this visual I needed **one column** with the categories: 'AOP', 'Forecast', 'CY Actuals', and 'PY Actuals.' The current datatable had a **column for each**. I used the **modeling tab** in Power BI to **create a new table in DAX**. In the formula, I am able to code individual rows. This logic can be used to **append a 4 small tables together.** Each table correspoded to the categories I needed. The code is below:

    NewTable = 
    UNION (
        SUMMARIZECOLUMNS ( 'Query1'[Account Group]  , 'Query1'[Current Fiscal Year] , 'Query1'[Current Fiscal Quarter] , 'Query1'[Fiscal Month] , 
        'Query1'[Period] , 'Query1'[Flag] , 'Query1'[Fiscal Quarter], "Scenario" ,"AOP" , "Values" , [AOP]), <-- CATEGORY

        SUMMARIZECOLUMNS ( 'Query1'[Account Group]  , 'Query1'[Current Fiscal Year] , 'Query1'[Current Fiscal Quarter] , 'Query1'[Fiscal Month] , 
        'Query1'[Period] , 'Query1'[Flag] , 'Query1'[Fiscal Quarter]   , "Scenario" , "Fcst" , "Values", [Forecast]), <-- CATEGORY

        SUMMARIZECOLUMNS ( 'Query1'[Account Group] , 'Query1'[Current Fiscal Year] ,'Query1'[Current Fiscal Quarter] , 'Query1'[Fiscal Month] , 
        'Query1'[Period] , 'Query1'[Flag] , 'Query1'[Fiscal Quarter] , "Scenario" , "CY Actuals" , "Values" , [CY Actuals]), <-- CATEGORY

        SUMMARIZECOLUMNS ( 'Query1'[Account Group] , 'Query1'[Current Fiscal Year] , 'Query1'[Current Fiscal Quarter] , 'Query1'[Fiscal Month] , 
        'Query1'[Period] , 'Query1'[Flag],  'Query1'[Fiscal Quarter]  , "Scenario" , "PY Actuals" , "Values" , [PY Actuals] )) <-- CATEGORY
