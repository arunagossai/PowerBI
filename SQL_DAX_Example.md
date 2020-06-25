# SQL and DAX Example with Power BI
![](/images/OPEX1.png)

## SQL
In this project I visualized **operating expenses** which actualize at the end of the month. 
This required me to **change the timeframe** of the dashboard to show the prior month.
I used **SQL** to change the Quarter-to-Date (QTD) and Year-to-date (YTD) to reflect the period as if it was the month before.
The SQL code is below:

       CASE
     WHEN `Current Fiscal Month` = 1 AND `Fiscal Quarter` = 4 THEN 'Y'  
     WHEN `Current Fiscal Month` = 4 AND `Fiscal Quarter` = 1 THEN 'Y' 
     WHEN `Current Fiscal Month` = 7 AND `Fiscal Quarter` = 2 THEN 'Y' 
     WHEN `Current Fiscal Month` = 10 AND `Fiscal Quarter` = 3 THEN 'Y' 
     WHEN (`Current Fiscal Month` = `Fiscal Month` OR `QTD Flag` = 'N') THEN "N" ELSE "Y" END AS `QTD`,

       CASE
     WHEN `Current Fiscal Month` = 1 THEN 'Y'  
     WHEN (`Current Fiscal Month` = `Fiscal Month` OR `YTD Flag` = 'N') THEN 'N' ELSE 'Y' END AS `YTD`,

## DAX
Because of the shifted timeframe the **formulas in DAX** needed to be changed as well.
This was done for annual operating plan (AOP), forecast, and actuals.
The DAX formulas show the code for AOP, depending on if you wanted to see QTD or YTD amounts this code specifies the returned values.


     SUMX ( 'Query1' ,
          IF ( [Current Fiscal Month] = 1 && [Period] = "QTD" && [Prior Fiscal Year] = [Fiscal Year] && [Fiscal Quarter] = 4, [AOP P$],
          IF ( [Current Fiscal Month] = 1 && [Period] = "YTD" && [Prior Fiscal Year] = [Fiscal Year], [AOP P$],
          IF ( [Current Fiscal Month] > 1 && [Period] = "QTD" && [Current Fiscal Year] = [Fiscal Year] && ([Current Fiscal Month] = 4 || 7 || 10) && [Flag] = "Y", [AOP P$],
          IF ( [Current Fiscal Month] > 1 && [Period] = "QTD" && [Current Fiscal Year] = [Fiscal Year] && ([Current Fiscal Month] <> 4 && 7 && 10) && [Current Fiscal Quarter] = [Fiscal Quarter] , [AOP P$],
          IF ( [Current Fiscal Month] > 1 && [Period] = "YTD" && [Current Fiscal Year] = [Fiscal Year], [AOP P$], BLANK () ))))))

## Another Page in Dashboard
![](/images/OPEX2.png)
