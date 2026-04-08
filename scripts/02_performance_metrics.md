### 02. Performance Metrics

This script includes DAX measures for evaluating campaign efficiency and return, such as **ROAS, Conversion Rate, Click-through Rate, CPA, CPC, CPM**. These metrics help measure the effectiveness of marketing spend and support performance comparison across campaigns, channels, and devices.

**Return on Ad spend (ROAS)**:
The revenue generated for each £1 spent on advertising.
  ```DAX
  ROAS = DIVIDE(SUM(fact_mkt[Total conversion value, GBP]),SUM(fact_mkt[Spend, GBP]))
  ```
**Click-through Rate**: The percentage of users who click on the ad after seeing it.
 ```DAX
  ConversionRate = DIVIDE(SUM(fact_mkt[Clicks]), SUM(fact_mkt[Impressions]))
  ```
or with the data provided: ```CTR = AVERAGE(fact_mkt[CTR, %])```

**Conversion Rate**:
The percentage of users who purchased products after clicking on the ads. 
 ```DAX
  ConversionRate = DIVIDE(SUM(fact_mkt[Conversions]),SUM(fact_mkt[Clicks]))
  ```
**Cost per Mile (CPM)**: Cost spent per 1,000 impressions.
```DAX
  CostperMile = DIVIDE(SUM(fact_mkt[Spend, GBP]),SUM(fact_mkt[Impressions]))*1000
  ```
**Cost per Click (CPC)**: Cost spent per click.
```DAX
  CostperClick = DIVIDE(SUM(fact_mkt[Spend, GBP]),SUM(fact_mkt[Clicks]))
  ```
**Cost per Action (CPA)**: Cost spent per action/ conversion.
```DAX
  CostperAction = DIVIDE(SUM(fact_mkt[Spend, GBP]),SUM(fact_mkt[Conversions]))
  ```
