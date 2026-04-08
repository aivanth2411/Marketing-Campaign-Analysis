### 01. Base Measures
  These are core measures used for KPI calculations.

**Total number of clicks**
  ```DAX
  TotalClicks = SUM(fact_mkt[Clicks])
  ```
**Total number of conversions**
 ```DAX
 TotalConversions = SUM(fact_mkt[Conversions])
  ```
**Total number of engagements**
```DAX
TotalEngagements = SUM(fact_mkt[Engagements])
  ```
**Total number of impressions**
```DAX
TotalImpressions = SUM(fact_mkt[Impressions])
  ```
