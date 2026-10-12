GridSense Energy Services — Electricity Consumption Insight
PRACTICE DATASET (synthetic; not official company data)

Coverage: hourly readings from 2025-01-01 to 2025-03-01 (60 days).
Files:
- meter_readings.csv: timestamp, customer, consumption
- customers.csv: customer, segment, area, connection_type
- weather.csv: timestamp, temperature, humidity, rain
- calendar.csv: timestamp, weekday, holiday, season
- tariff.csv: timestamp, tariff_category, peak_period, tariff_rate_band

Data-quality issues intentionally included:
- Some missing consumption readings
- Duplicate meter records
- A few negative consumption values
- One inconsistent customer segment label ("residential")
- Missing temperature/humidity values in weather.csv

Suggested join plan:
1. Normalize customers.segment values (e.g. title case).
2. Merge meter_readings with customers on customer.
3. Merge with weather and calendar on timestamp.
4. Merge tariff on timestamp and normalized segment = tariff_category.
   tariff.csv has one row per timestamp per tariff category, so this join gives the matching tariff period for each customer record.

Peak definition in this practice dataset:
Peak = hours 07:00–10:59 or 17:00–21:59; otherwise Off-Peak.
This is a teaching assumption, not a real utility tariff rule.

Suggested analysis:
- Peak demand by hour and weekday/weekend
- Temperature vs consumption
- Segment comparison
- Area-level standard deviation/variability
- Peak vs off-peak consumption
- Optional regression: predict consumption from time, weather, segment, area, and tariff features

Do not report model scores or findings as real-world facts; calculate them from the cleaned data.
