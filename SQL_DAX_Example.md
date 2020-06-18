# SQL and DAX with Power BI
![](/images/OPEX1.png)
In this project I visualized **operating expenses** which actualize at the end of the month. 
This required me to **changes the times frame** of the dashboard.
I used **SQL** to change the Quarter-to-Date and Year-to-date to reflect the period as if it was the month before.
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

