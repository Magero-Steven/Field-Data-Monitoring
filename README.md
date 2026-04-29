# Field-Data-Monitoring
![Field Data Dashboard](https://github.com/Magero-Steven/Field-Data-Monitoring/blob/ed680191fb917cb72854570861d4e9bc655b5629/Data%20Quality%20Image.png)
CAPI-based Field Data Monitoring System for GPS, paradata tracking, data quality assurance, and real-time survey validation using Python and dashboard to ascertai quality .
### Features
- GPS & timestamp (paradata) validation
- Data quality checks (duration, consent, sync issues)
- Enumerator performance tracking
- Dashboard visualization (Power BI/Tableau)
---
### 🗂️ Synthetic Dataset

- File: `/data/field_data_600_records.csv`
- Sample size: 600 participants
- Variables:
  - `enumerator_id`
  - `submission_id` 
  - `gps_lat` (Lattitude)
  - `gps_long` (Longitude)
  - `start_time`
  - `end_time`
  - `duration_minutes`
  - `consent`
  - `household_id`
  - `sync_status`
### Tools

- Excel-Data Sorting/Preview
- Tableau - Dashbords/Reports
- Python (Pandas)
---

### Key Insights
- Identified anomalous submissions using duration thresholds
---
Python 
The csv fie is loaded ready for analysis 
```
    import pandas as pd

# Load data
    df = pd.read_csv("field_data.csv")

# Convert time columns
    df['start_time'] = pd.to_datetime(df['start_time'])
    df['end_time'] = pd.to_datetime(df['end_time'])

# Data Quality Checks
    print("🔍 Missing Values:\n", df.isnull().sum())

# Flag suspicious durations (<10 min or >40 min)
    df['duration_flag'] = df['duration_minutes'].apply(
        lambda x: "Suspicious" if x < 10 or x > 40 else "Normal"
)

```
- Detected sync failures affecting data completeness
- Monitored enumerator performance for quality control
