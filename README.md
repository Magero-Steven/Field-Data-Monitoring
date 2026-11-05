<h1 align="center">📡 Field Data Monitoring</h1>

<p align="center">
  <b>Catch bad survey data while fieldwork is still running.</b><br>
  GPS validation · Paradata checks · Sync tracking · Enumerator scorecards
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="pandas">
  <img src="https://img.shields.io/badge/Tableau-Dashboards-E97627?style=for-the-badge&logo=tableau&logoColor=white" alt="Tableau">
  <img src="https://img.shields.io/badge/Power%20BI-Reports-F2C811?style=for-the-badge&logo=powerbi&logoColor=black" alt="Power BI">
  <img src="https://img.shields.io/badge/Data-Synthetic-8A2BE2?style=for-the-badge" alt="Synthetic data">
</p>

![Data quality overview](Data%20Quality%20Image.png)

---

## 🌍 Overview

A simulated **CAPI (Computer-Assisted Personal Interviewing)** field monitoring system for large-scale surveys. It combines GPS and paradata validation, synchronization tracking, and enumerator performance scoring to flag problems early.

> [!NOTE]
> All data in this repository is **synthetic** (600 simulated submissions). No real respondents are involved.

---

## 🔍 What It Detects

| | Area | Checks |
|---|---|---|
| 🧩 | **Completeness** | Missing values, duplicate submission IDs, duplicate household IDs |
| ⏱️ | **Paradata / Time** | End before start, reported vs. computed duration mismatch, interviews too short or too long (fixed thresholds + robust median/MAD outlier test) |
| 📍 | **GPS** | Missing or invalid coordinates, points outside the study area, identical coordinates reused across households, impossible travel speed or overlapping interviews |
| ✅ | **Consent** | Missing or unrecognised values, consent refused but a full interview recorded |
| 🔄 | **Synchronization** | Submissions that failed to sync |
| 🏆 | **Enumerator Performance** | Flag rates per enumerator and a 0-100 quality score |

### 🚦 Enumerator Rating

| Rating | Quality score | Meaning |
|---|---|---|
| 🟢 **Good** | 85 - 100 | Data looks reliable |
| 🟡 **Watch** | 70 - 85 | Some issues, monitor closely |
| 🔴 **Needs review** | below 70 | Check interviews and retrain if needed |

---

## 🗂️ Repository Contents

| File | Description |
|---|---|
| 📄 `field_data_600_records.csv` | Synthetic dataset of 600 submissions |
| 🧼 `cleaned_field_data.csv` | Cleaned version of the dataset |
| 🐍 `field_data_monitoring.py` | Python (pandas) pipeline: all checks plus the scorecard |
| 🖼️ `Data QLTY 5.png`, `Data Quality Image.png` | Dashboard and data quality visuals |

---

## 📊 Dataset

| Variable | Description |
|---|---|
| 👤 `enumerator_id` | Interviewer identifier |
| 🔑 `submission_id` | Unique submission identifier |
| 🧭 `gps_lat` | Latitude of the interview |
| 🧭 `gps_long` | Longitude of the interview |
| 🕘 `start_time` | Interview start timestamp |
| 🕔 `end_time` | Interview end timestamp |
| ⏳ `duration_minutes` | Reported interview length in minutes |
| ✍️ `consent` | Respondent consent status |
| 🏠 `household_id` | Household identifier |
| 📶 `sync_status` | Whether the submission synced to the server |

---

## 🚀 Quick Start

```bash
pip install pandas numpy
python field_data_monitoring.py field_data_600_records.csv
```

**Outputs** are saved to an `output/` folder:

- 🚩 `flagged_submissions.csv`: every submission with one True/False column per check
- 🏅 `enumerator_scorecard.csv`: one row per enumerator, ready for a dashboard
- 📝 `summary.txt`: headline counts

### ⚙️ Configuration

> [!TIP]
> Thresholds sit at the top of the script, so you can tune them for each survey.

```python
MIN_DURATION = 10            # minutes
MAX_DURATION = 40            # minutes
MAX_TRAVEL_SPEED_KMH = 100   # implausible travel between interviews
STUDY_AREA_BBOX = None       # (min_lat, max_lat, min_long, max_long)
```

> [!IMPORTANT]
> Consent and sync values are matched against editable sets (`CONSENT_YES`, `CONSENT_NO`, `SYNC_OK`). If your data uses different labels, update these sets first.

---

## 📈 Dashboard Layout

Load `flagged_submissions.csv` and `enumerator_scorecard.csv` into **Tableau** or **Power BI**.

1. 🔢 **KPI strip:** total submissions, % flagged, % sync failed, % consent issues, average duration
2. 📅 **Trend:** submissions and flag rate by day
3. 🏆 **Enumerator scorecard:** ranked table with red/amber/green colouring
4. 📉 **Duration distribution:** histogram with min/max thresholds marked
5. 🗺️ **Map:** submission points coloured by GPS flag
6. 🎛️ **Filters:** date, enumerator, supervisor or region, flag type

---

## 💡 Key Insights

- 🚨 Anomalous submissions are identified using duration thresholds and outlier tests
- 📡 Sync failures affecting data completeness are surfaced per enumerator
- 🎯 Enumerator performance is tracked through a weighted, comparable quality score

> [!WARNING]
> Automated flags are **signals, not verdicts**. Always review flagged interviews before taking action against an enumerator.

---

## 🧰 Tools

![Python](https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/-Pandas-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/-NumPy-013243?logo=numpy&logoColor=white)
![Excel](https://img.shields.io/badge/-Excel-217346?logo=microsoftexcel&logoColor=white)
![Tableau](https://img.shields.io/badge/-Tableau-E97627?logo=tableau&logoColor=white)
![Power BI](https://img.shields.io/badge/-Power%20BI-F2C811?logo=powerbi&logoColor=black)

---

## 📌 About

Simulated field data monitoring system integrating CAPI workflows, GPS/paradata validation, synchronization tracking, and data quality analytics for large-scale surveys.

<p align="center">Built by <a href="https://github.com/Magero-Steven">Magero-Steven</a> 💙</p>
