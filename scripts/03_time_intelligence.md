### 03. Time Intelligence
  This script contains DAX measures used to analyze performance over time. It includes time-based calculations such as **Month-over-Month (MoM) changes in ROAS, Total Cost, and Total Revenue**, as well as logic for displaying **increase/decrease trend icons** in the dashboard.
  
- **Month-over-month ROAS**: This measure calculates the percentage change in ROAS compared to the previous month.
```SQL
ROAS_MoM = 
VAR current_month = MAX(dim_calendar[Date]) -- Get the latest date in the current filter context
VAR previous_month = EOMONTH(current_month, -1) -- Get the last date of the previous month
VAR roas_current = -- Calculate ROAS for the current month
    CALCULATE(
        [ROAS],
        FILTER(
            dim_calendar,
            dim_calendar[Year] = YEAR(current_month) &&
            dim_calendar[Month] = MONTH(current_month)
        )
    )
VAR roas_previous = -- Calculate ROAS for the previous month
    CALCULATE(
        [ROAS],
        FILTER(
            ALL(dim_calendar),
            dim_calendar[Year] = YEAR(previous_month) &&
            dim_calendar[Month] = MONTH(previous_month)
        )
    )
RETURN 
    IF(
        ISBLANK(roas_previous),
        0,
        (roas_current - roas_previous) / roas_previous
    )
-- Return percentage change
```

- **Month-over-Month ROAS Trend icon**: This measure creates a visual trend indicator for the Month-over-Month ROAS change. It displays an **upward arrow** when ROAS increases and a **downward arrow** when ROAS decreases, followed by the absolute percentage change formatted to one decimal place.
``` SQL
ROAS_MoM_Icon = 
VAR positive = UNICHAR(9650) -- Upward arrow symbol
VAR negative = UNICHAR(9660) -- Downward arrow symbol
VAR change_mom = [ROAS_MoM] -- Retrieve MoM percentage change
VAR icon = IF(change_mom >= 0, positive, negative) -- Assign icon based on trend direction
VAR result = icon & " " & FORMAT(ABS(change_mom), "0.0%") -- Format percentage with one decimal place
RETURN result
```
The same Month-over-Month logic is also applied to other key metrics, including:

- `TotalCost_MoM`
- `TotalRevenue_MoM`
