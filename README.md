# SPOTIFY-SONGS-AND-ARTIST-ANALYTICS-DASHBOARD-
# Spotify Songs & Artist Analytics Dashboard

An end-to-end Power BI analytics solution built on a Spotify tracks dataset, covering data modeling, DAX-based measure design, and a multi-page interactive report for catalog and popularity analysis.

<p align="left">
  <img src="https://img.shields.io/badge/Power%20BI-Desktop-F2C811?logo=powerbi&logoColor=black" />
  <img src="https://img.shields.io/badge/DAX-Data%20Modeling-yellow" />
  <img src="https://img.shields.io/badge/Power%20Query-ETL-blue" />
  <img src="https://img.shields.io/badge/License-MIT-green" />
</p>

**Demo:** [Watch the walkthrough](https://youtu.be/MjeDkDHJqzc?si=0qx3-Uplxv7RXt0O)

---

## 1. Project Summary

This project transforms a raw Spotify tracks dataset into a governed data model and a three-page Power BI report, designed to answer core catalog-analytics questions:

- How is the catalog distributed across album types (single vs. album) and content rating (explicit vs. non-explicit)?
- How has average track popularity trended month-over-month and year-over-year?
- Which artists contribute the most distinct tracks, and how does popularity vary by song and artist?
- Are there seasonal patterns in release volume?

The report follows a standard BI workflow: **raw data → Power Query transformation → star-schema-oriented data model → DAX measures → report layer**, with a custom Spotify-branded dark theme and button-driven page navigation.

---

## 2. Architecture & Approach

| Stage | Description |
|---|---|
| **Ingestion** | Source dataset loaded via Power Query (`Get Data`) from CSV/Excel |
| **Transformation** | Data cleaning, type casting, column splitting (artist/track), duration normalization, and de-duplication handled in Power Query (M) |
| **Modeling** | Fact table (`Songs`) related to supporting dimension tables (`Artists`, `Calendar`) using single-direction relationships to avoid ambiguity |
| **Calculation Layer** | KPIs and trend logic implemented as DAX measures, kept in a dedicated measures table for maintainability |
| **Presentation** | Three report pages — Home, Overview, Songs/Artists — connected via bookmarks and button-based navigation, styled with a custom dark/green theme JSON |

A dedicated **Date/Calendar table** is used (rather than relying on auto date hierarchies) to support accurate year-over-year and month-over-month DAX comparisons.

---

## 3. Tools & Technologies

| Category | Tool / Technique |
|---|---|
| BI & Visualization | Microsoft Power BI Desktop |
| Data Transformation | Power Query Editor (M language) |
| Calculation Engine | DAX (Data Analysis Expressions) |
| Data Modeling | Star-schema-oriented relational model within Power BI |
| Report Navigation | Bookmarks, Buttons, Selection Pane |
| Theming | Custom Power BI JSON theme (Spotify dark/green palette) |
| Version Control | Git & GitHub |

---

## 4. Dataset

| Attribute | Detail |
|---|---|
| Source | *[Add dataset source/link — e.g., Kaggle Spotify Tracks Dataset]* |
| Volume | 282K total tracks, 789 distinct songs |
| Grain | One row per track |
| Key fields | Track name, artist, album type, release date, popularity score, duration, explicit flag |

> **Note on data licensing:** If the source dataset's license does not permit redistribution, do not commit the raw file to this repository. Instead, reference the original source and, if needed, include a small anonymized sample under `/data/sample/` for reproducibility.

---

## 5. Repository Structure

```
spotify-analytics-dashboard/
│
├── PowerBI/
│   └── Spotify_Dashboard.pbix       # Primary Power BI report file
│
├── data/
│   └── spotify_dataset.csv          # Source dataset (or /sample for a license-safe subset)
│
├── docs/
│   ├── dax_measures.md              # Full list of DAX measures with definitions
│   └── data_model.png               # Entity-relationship diagram of the model
│
├── assets/
│   ├── home_page.png
│   ├── overview_page.png
│   └── songs_artists_page.png
│
├── README.md
└── LICENSE
```

---

## 6. Report Pages

**Home** — Landing page with report navigation.

**Overview** — Executive summary: total tracks, distinct songs, average duration, average popularity, album-type and explicit-content breakdowns, year-over-year comparisons, monthly popularity trend, and release seasonality.

**Songs / Artists** — Drill-down view: distinct song counts by artist and average popularity by individual track, supporting granular comparison.

---

## 7. Key DAX Measures

```DAX
Total Tracks = 
COUNTROWS ( 'Songs' )

Distinct Songs = 
DISTINCTCOUNT ( 'Songs'[Track Name] )

Average Popularity = 
AVERAGE ( 'Songs'[Popularity] )

Average Duration (Min) = 
DIVIDE ( AVERAGE ( 'Songs'[Duration Ms] ), 60000 )

Distinct Songs by Artist = 
CALCULATE (
    DISTINCTCOUNT ( 'Songs'[Track Name] ),
    ALLEXCEPT ( 'Songs', 'Songs'[Artist] )
)

YoY Popularity Change % = 
VAR CurrentPop = [Average Popularity]
VAR PriorYearPop = 
    CALCULATE ( [Average Popularity], SAMEPERIODLASTYEAR ( 'Calendar'[Date] ) )
RETURN
    DIVIDE ( CurrentPop - PriorYearPop, PriorYearPop )
```

> Replace the above with the exact measures exported from your `.pbix` (Model view → Measures) to ensure documentation matches the shipped report. Full list maintained in [`docs/dax_measures.md`](docs/dax_measures.md).

---

## 8. Setup & Usage

**Prerequisites:** Power BI Desktop (latest version recommended).

```bash
git clone https://github.com/<your-username>/spotify-analytics-dashboard.git
cd spotify-analytics-dashboard
```

1. Open `PowerBI/Spotify_Dashboard.pbix` in Power BI Desktop.
2. If prompted, update the data source path (`Transform Data → Data Source Settings`) to point to `data/spotify_dataset.csv`.
3. Click **Refresh** to reload the data model.
4. Navigate the report using the top navigation bar (Home / Overview / Artists / Songs).

---

## 9. Skills Demonstrated

- Data cleaning and transformation using Power Query (M)
- Relational data modeling (fact/dimension design, relationship cardinality)
- DAX measure authoring, including time-intelligence functions (`SAMEPERIODLASTYEAR`, `ALLEXCEPT`)
- Report UX design: custom theming, bookmark-based navigation, KPI card layout
- Translating a business question into a measurable, visualized metric

---

## 10. Roadmap / Possible Extensions

- Add a Power BI Service deployment with scheduled refresh
- Incorporate audio-feature fields (danceability, energy, tempo) for genre-level clustering
- Add row-level security (RLS) for artist-scoped access
- Automate ETL via Power BI dataflows or a Python pre-processing pipeline

---

## 11. License

Licensed under the [MIT License](LICENSE).

---

## 12. Author

**Arpit**
B.Tech (Metallurgical & Materials Engineering), NIT Warangal
Data Analyst | Power BI · SQL · Python

Feedback and suggestions are welcome via Issues or Pull Requests.
