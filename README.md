# 📰 Real-Time News Analytics Dashboard

An **API-driven news and information analytics dashboard** built with **Microsoft Power BI**, **Power Query (M)**, **DAX**, and multiple REST APIs.

The project brings **World News, India News, Sports, Stock Market indicators, Weather, Social/Tweet updates, Quotes, and multilingual news content** into a single interactive Power BI experience.

Instead of relying on a manually maintained dataset, the dashboard connects to external APIs, retrieves JSON data, transforms and cleans it in Power Query, maintains dedicated current/historical storage queries, and presents the processed information through interactive Power BI pages.

---
<img width="928" height="666" alt="Screenshot 2026-10-06 165916" src="https://github.com/user-attachments/assets/ff79c684-bde0-4899-b9dc-51334ce3cb7e" />
<img width="929" height="666" alt="Screenshot 2026-10-06 165940" src="https://github.com/user-attachments/assets/2474275e-a608-49dc-bbfe-c1c5691c29fc" />
<img width="931" height="664" alt="Screenshot 2026-10-06 165959" src="https://github.com/user-attachments/assets/a47a664e-cc55-49f7-a53c-0f014578f577" />


## 📌 Project Overview

The goal of this project was to build a **centralized live/current-information analytics platform** that demonstrates how Power BI can work with data coming from multiple REST APIs and semi-structured JSON sources.

The dashboard is organized into three primary user-facing pages:

1. 🌍 **World News**
2. 🇮🇳 **India News**
3. 🏟️ **Sports News**

Each page combines its main content with supporting information and interactive elements.

### World News

The World News page provides a global overview of current headlines and a weekly news digest.

It includes:

- Today's Headlines
- Weekly News Digest
- Weather information
- Stock-market indicators
- Quote of the Day
- Tweet/social updates
- Explore Channels
- Time/date display
- News filtering

### India News

The India News page focuses on India-specific news and follows a similar information layout.

It includes:

- Today's Headlines
- Weekly News Digest
- Indian market indicators
- City-level weather information
- Quote of the Day
- Tweet/social updates
- Indian news channels
- Interactive filters
- Time/date display

### Sports News

The Sports News page is designed for sports-focused monitoring and combines news with live/current match information.

It includes:

- Today's Sports Headlines
- Weekly Sports Digest
- Cricket Live Score
- Football Live Score
- Match status information
- Sports news channels
- Interactive navigation
- Current API-driven sports information

---

# 🎯 Key Objectives

The project was built to demonstrate practical skills in:

- REST API integration
- Power Query / M
- JSON parsing and transformation
- Data cleaning and preparation
- Data modeling
- DAX calculations
- Historical/current data management
- Multi-source data integration
- API-based dashboard development
- Multilingual data processing
- Interactive Power BI reporting

---

# 🏗️ Overall Architecture

```text
                         EXTERNAL APIs
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
   GNews API            NewsData.io          AllSportsAPI
        │                     │                     │
        │                     │              ┌──────┴──────┐
        │                     │              │             │
        │                     │          Sports Data   Live Scores
        │                     │
        ├───────────────┬─────┘
        │               │
        ▼               ▼
   World News       India News
        │               │
        └────────┬──────┘
                 ▼
          Power Query / M
                 │
      ┌──────────┼──────────┐
      │          │          │
      ▼          ▼          ▼
 Current Data  Storage   Enrichment
    Queries    Queries      APIs
      │          │          │
      │          │      ┌───┴──────────────┐
      │          │      │                  │
      │          │   LibreTranslate    WeatherAPI
      │          │
      │          │
      └──────┬───┴──────────────────────────┐
             ▼                              ▼
      Power BI Data Model              Supporting Data
             │
             ▼
        DAX Measures
             │
             ▼
     Interactive Dashboard
```

---

# 🔄 How the Dashboard Works

The dashboard follows an API → ETL → Model → Visualization workflow.

## 1. API Data Collection

Power BI connects to external APIs using `Web.Contents()` in Power Query.

The APIs return data primarily in **JSON format**.

Example flow:

```text
REST API
   ↓
JSON Response
   ↓
Power Query
```

---

## 2. JSON Parsing

Power Query converts API responses into tables.

Typical operations include:

- Converting JSON lists into tables
- Expanding records
- Expanding nested lists
- Selecting required fields
- Renaming columns
- Converting data types
- Handling null values
- Cleaning text
- Preparing data for analysis

---

## 3. Current Data Queries

Dedicated queries are used to retrieve the latest/current API information.

Examples from the project include:

```text
World News
India News
Sports
LiveScore
Fixtures
All Matches
India Stock
Cricket
Tweets
Quote of the day
```

These queries act as the main ingestion layer.

---

# 🗄️ News Storage & Historical Data

A major part of the project is the use of **separate storage queries/tables** for retaining news and other information for analysis.

Examples include:

```text
World News
      ↓
World News Storage

India News
      ↓
India News Storage

Sports
      ↓
Sports Storage
```

The **Storage** queries are kept separate from the current API queries so that current ingestion and historical data handling remain modular.

### Why use Storage queries?

Without a storage/history layer, an API-driven report may only contain the latest response returned by the source.

The storage approach allows the project to support:

- Historical news analysis
- Weekly news summaries
- Comparison across refresh periods
- Trend analysis
- Retention of previously retrieved records

### Important implementation note

For this version of the project, the storage layer is implemented within the **Power BI / Power Query workflow** using dedicated Storage queries/tables. It is not presented as an external SQL database.

---

# 🌐 Multilingual News Processing

One of the project's key features is multilingual news support using **LibreTranslate**.

The workflow is:

```text
News API
   ↓
News Article/Text
   ↓
LibreTranslate API
   ↓
Translated Text
   ↓
Power BI
```

The project was designed to support translations such as:

- English
- Hindi
- Spanish

This demonstrates API chaining, where output from one API-driven workflow becomes input for another service.

---

# 🔌 APIs & Data Sources

## 📰 GNews API

Used as a primary news source for retrieving current news.

Typical article attributes include:

- Title
- Description
- Source
- Publication date
- Article URL
- Image/thumbnail
- News search/category information

---

## 🌍 NewsData.io

Used as an additional source for current news retrieval.

It provides another external source that can complement the primary news feed.

---

## 🏏 AllSportsAPI

Used for sports-related information.

The project includes functionality for:

- Sports news
- Cricket information
- Football information
- Live scores
- Fixtures
- Match listings
- Match status

Power BI queries in the project include:

```text
Sports
Sports Storage
LiveScore
Fixtures
All Matches
Cricket
```

---

## 📈 EODHD

Used for stock-market data.

The Indian-stock workflow was designed around NSE symbols such as:

```text
RELIANCE.NSE
TCS.NSE
INFY.NSE
HDFCBANK.NSE
ICICIBANK.NSE
```

The data can be used for market indicators and stock-related dashboard components.

> Market data availability and delay depend on the EODHD account/endpoint being used.

---

## 🌦️ WeatherAPI

Used to retrieve weather information displayed alongside the news experience.

Examples shown in the dashboard include city-specific weather information such as:

```text
Nagpur
New York
```

The weather component provides context alongside the news feed.

---

## 💬 ZenQuotes

Used for the **Quote of the Day** component.

The quote is displayed as a supporting information card within the dashboard.

---

## 🐦 Social / Tweet Data

The project also contains a dedicated **Tweets** query used to display social/news-related updates within the dashboard.

The exact source or connector configuration can depend on the original Power BI implementation.

---

# 📊 Dashboard Pages

## 1. 🌍 World News Page

The World News page acts as the global information hub.

### Main sections

**Today's Headlines**

Displays selected current headlines with article images, titles, sources, and publication timing.

**Weekly News Digest**

Provides a broader view of recent news collected for the selected period.

**Weather**

Displays current weather context for a selected location.

**Quote of the Day**

Shows a daily quote retrieved from the quote API.

**Sensex / Stock Market**

Displays selected market indicators alongside the news feed.

**Tweets**

Shows selected social/news updates.

**Explore Channels**

Provides quick access to selected news/media sources.

---

## 2. 🇮🇳 India News Page

The India News page is dedicated to India-focused content.

### Main sections

- Today's Headlines
- Weekly News Digest
- Indian market indicators
- Weather
- Tweets
- Quote of the Day
- Indian news channels
- Interactive filtering

The page is designed to provide a focused view of India-related information without mixing it with the broader world-news feed.

---

## 3. 🏟️ Sports News Page

The Sports News page combines news analytics with current sports information.

### Main sections

- Today's Headlines
- Weekly News Digest
- Cricket Live Score
- Football Live Score
- Match status
- Sports channels
- Sports navigation

The sports page demonstrates how Power BI can combine **editorial/news information and structured live-event data** in the same report.

---

# 🖼️ Dashboard Screenshots

## World News Dashboard

The World News dashboard provides a global news overview with headline cards, a weekly digest, market information, weather, social updates, quotes, and curated channels.

<img width="928" height="666" alt="Screenshot 2026-10-06 165916" src="https://github.com/user-attachments/assets/7009bcae-85c6-4bd5-a298-893e1b701f00" />


---

## India News Dashboard

The India News dashboard focuses on India-specific headlines and recent news while also displaying market indicators, weather, social updates, quotes, and Indian media channels.

<img width="929" height="666" alt="Screenshot 2026-10-06 165940" src="https://github.com/user-attachments/assets/907bae68-d69c-4531-8bac-fbb51e516cfa" />


---

##  Sports News Dashboard

The Sports News dashboard combines current sports news with cricket and football live-score sections, match status information, a weekly digest, and sports media channels.

<img width="931" height="664" alt="Screenshot 2026-10-06 165959" src="https://github.com/user-attachments/assets/a698b4b5-3cc6-4f61-823e-69a7096ce72c" />


---

# ⚡ Real-Time / Current Data Concept

The project is described as **Real-Time News Analytics** because its primary data sources are external APIs that provide current or frequently updated information instead of a manually maintained static dataset.

The general refresh process is:

```text
API
 ↓
Power Query
 ↓
Transform
 ↓
Load
 ↓
Power BI Model
 ↓
Visuals
```

However, it is important to distinguish **API-driven current data** from a true second-by-second streaming architecture.

This implementation uses Power BI data refresh and API retrieval. It should therefore be described technically as an **API-driven current/live-data dashboard**, rather than claiming that every visual updates every second.

Some external services, especially financial APIs, may also provide delayed market data depending on the endpoint and subscription.

---

# 🔁 Data Refresh Workflow

When the Power BI queries are refreshed:

```text
1. Power BI sends API requests
          ↓
2. APIs return JSON data
          ↓
3. Power Query parses responses
          ↓
4. Records/lists are expanded
          ↓
5. Data is cleaned and transformed
          ↓
6. Translated fields are generated where required
          ↓
7. Current and storage queries are processed
          ↓
8. Data is loaded into the Power BI model
          ↓
9. DAX measures are recalculated
          ↓
10. Dashboard visuals update
```

---

# 🧮 Power Query & M

Power Query is the main ETL layer of the project.

### Major transformations

- REST API requests using `Web.Contents()`
- JSON parsing
- List-to-table conversion
- Record expansion
- Nested record expansion
- Column selection
- Column renaming
- Data type conversion
- Null handling
- Text transformations
- Date/time transformation
- Data preparation for the semantic model

This allowed semi-structured API responses to become structured analytical tables.

---

# 📐 DAX & Analytics

DAX is used for analytical calculations and dashboard metrics.

Typical DAX use cases include:

- KPI calculations
- Aggregations
- Current-value indicators
- Trend calculations
- Dynamic measures
- Time-based analysis
- Filter-aware calculations

The combination of **Power Query for ETL** and **DAX for analytics** separates data preparation from analytical logic.

---

# 🗂️ Power BI Query Organization

The project is organized using functional query groups rather than putting every API into one large query.

Examples include:

```text
World News
World News Storage

India News
India News Storage

Sports
Sports Storage

LiveScore
Fixtures
All Matches
Cricket

India Stock
Tweets
Quote of the day
```

This modular organization makes the project easier to maintain and troubleshoot.

---

# 🛠️ Technology Stack

| Technology / Service | Purpose |
|---|---|
| Microsoft Power BI | Dashboard, modeling & visualization |
| Power Query | Data extraction & transformation |
| Power Query M | API integration & ETL logic |
| DAX | Measures, KPIs & analytics |
| REST APIs | External data ingestion |
| JSON | API response format |
| GNews API | News data |
| NewsData.io | Additional news data |
| AllSportsAPI | Sports, scores & fixtures |
| EODHD | Stock market data |
| WeatherAPI | Weather data |
| ZenQuotes | Daily quotes |
| LibreTranslate | Multilingual translation |

---

# 📁 Suggested Repository Structure

```text
Real-Time-News-Analytics-Dashboard/
│
├── PowerBI/
│   └── Real-Time-News-Analytics-Dashboard.pbix
│
├── Screenshots/
│   ├── world-news-dashboard.png
│   ├── india-news-dashboard.png
│   └── sports-news-dashboard.png
│
├── Documentation/
│   └── architecture.png
│
└── README.md
```

> Add the `.pbix` file to the `PowerBI` folder only when you are comfortable sharing the report file publicly.

---

# ⚙️ Setup & Usage

## 1. Install Power BI Desktop

Open the project using Microsoft Power BI Desktop.

## 2. Open the PBIX File

Open:

```text
Real-Time-News-Analytics-Dashboard.pbix
```

## 3. Configure API Credentials

Go to:

```text
Home
→ Transform Data
→ Data Source Settings
```

Configure the required credentials for the APIs used by the report.

## 4. Refresh

After configuring the API credentials:

```text
Home → Refresh
```

Power BI will retrieve the latest available data from the configured sources.

---

# 🔐 API Security

API keys and tokens should **never be committed to GitHub**.

Do not publish:

- API keys
- Authentication tokens
- Passwords
- Private endpoints
- Personal credentials

Use placeholders such as:

```text
YOUR_GNEWS_API_KEY
YOUR_ALLSPORTS_API_KEY
YOUR_EODHD_API_KEY
YOUR_WEATHER_API_KEY
```

Configure the real credentials locally through Power BI's data-source settings.

---

# 🚀 Key Project Highlights

### Multi-API Integration

Integrated multiple external REST APIs into one Power BI reporting environment.

### Semi-Structured Data Processing

Converted JSON API responses into structured analytical tables using Power Query.

### Current + Historical Data Workflow

Separated current ingestion queries from Storage queries to support historical analysis.

### Multilingual Data

Integrated LibreTranslate to create translated news content.

### Interactive Analytics

Created a multi-page Power BI experience with filters, cards, news panels, market indicators, live sports information, and supporting information.

### Modular Architecture

Organized APIs and transformations into separate functional queries for easier maintenance.

---

# 💼 Skills Demonstrated

This project demonstrates practical experience with:

- Power BI
- Power Query
- Power Query M
- DAX
- REST API integration
- API authentication
- JSON parsing
- ETL
- Data transformation
- Data modeling
- Historical data handling
- Multi-source data integration
- Semi-structured data
- Multilingual data processing
- Interactive dashboard design
- API-driven analytics

---

# 🎯 What I Learned

Through this project, I gained practical experience in building an analytics workflow from an external API all the way to a business-facing dashboard.

The key learning areas were:

```text
API Integration
      ↓
JSON Processing
      ↓
Power Query / M
      ↓
Data Transformation
      ↓
Data Storage
      ↓
Data Modeling
      ↓
DAX
      ↓
Power BI Visualization
```

The project also helped me understand the challenges of working with external APIs, including changing responses, missing fields, authentication, refresh behavior, API limits, and nested JSON structures.

---

# 👨‍💻 Author

**Jaykumar Kadao**

Data Analyst | Power BI | SQL | Python

Focused on:

- Data Analytics
- Business Intelligence
- Power BI
- Data Engineering
- GenAI & LLM Integration

---

## ⭐ Project Summary

> **An API-driven Power BI analytics platform that transforms current news and multi-source information into an interactive, multilingual dashboard experience.**

---

## 📄 Disclaimer

This project is built for **learning, portfolio, and demonstration purposes**.

The availability, accuracy, freshness, and usage limits of the displayed information depend on the respective third-party APIs and their subscription plans.
