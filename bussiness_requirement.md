# Business Requirements Document — Spotify Dashboard

## 1. Business Requirement

Spotify stakeholders — music analysts, playlist managers, and marketing teams — need a **consolidated dashboard** to monitor song and artist performance across multiple dimensions.

Based on the report requirements, the solution must deliver three report pages:

### 1.1 Overview Page
- Track KPIs: **Total Songs, Distinct Artists, Average Popularity, Average Duration**
- Compare **Explicit vs. Non-Explicit** songs and their share of the catalog
- Analyze **Songs by Album Type** (single, album, compilation)
- View **Distinct Songs** and **Average Popularity by Year**
- Trend analysis of **Average Popularity & Distinct Songs by Month**
- Highlight **Top Songs & Top Artists by Popularity**

### 1.2 Artist Page
- Show **Top Artists by Popularity**
- Compare **Tracks per Album** and **Songs by Artist**
- Provide drill-down to artist-level detail: songs, release date, average popularity, average chart position, duration
- Support identifying artists with **consistent hits and #1 chart positions**

### 1.3 Songs Page
- Rank **Top Songs by Popularity**
- Show **Tracks per Song** (album/single distribution)
- Compare **Songs by Song Count**
- Provide a detailed table: song name, release date, distinct artists, average popularity, chart position, duration per year

---

## 2. Problem Statement

Spotify's raw "Top 50" dataset is limited to flat lists and rankings, making it difficult for stakeholders to see patterns and act on insights quickly.

| Problem | How the Dashboard Solves It |
|---|---|
| No clear KPI monitoring | Summary cards give an instant read on total songs, artists, popularity, and duration |
| Lack of explicit vs. non-explicit analysis | Dedicated comparison shows how explicit content performs relative to non-explicit |
| Difficulty tracking song/album distribution | Visuals break down the catalog by album type and release year |
| Missing trend visibility | Popularity and distinct-song trends are shown monthly and yearly |
| Artist vs. song insights disconnected | Drill-down Artist and Songs pages connect high-level overview metrics to record-level detail |
| Decision-making gaps | Marketing and curation teams can identify which artists/songs to promote and which content resonates with audiences |

---

## 3. Scope

**In scope:** Power BI report covering Overview, Artist, and Songs pages, built on the historical Spotify Top 50 dataset (daily chart snapshots).

**Out of scope:** Real-time chart refresh, audio-feature-based clustering (danceability, energy, etc.), and user-level listening behavior (not present in the source dataset).

---

## 4. Success Criteria

- Stakeholders can identify top-performing songs and artists without manual filtering of raw data
- Trend and seasonality questions (month/year popularity movement) are answerable in one view
- Explicit vs. non-explicit and album-type splits are visible without additional analysis
- Report loads and filters interactively within Power BI Desktop / Service performance norms
