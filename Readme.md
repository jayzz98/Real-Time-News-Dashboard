# 📰 Real-Time News Analytics Dashboard

An API-driven **Real-Time News Analytics Dashboard** built using **Microsoft Power BI**, **Power Query (M)**, **DAX**, and multiple REST APIs.

The project collects current news and other live information from external APIs, transforms and analyzes the data in Power BI, maintains separate current and historical data tables, and presents the results through an interactive analytical dashboard.

---

## 🚀 Project Overview

The objective of this project is to build a centralized analytics platform that consumes live/current data from multiple APIs and converts it into meaningful insights through Power BI.

The dashboard is designed to provide:

- Current and historical news analysis
- India and world news monitoring
- Multilingual news translation
- Sports and live-score information
- Stock market information
- Weather information
- Daily quotes
- Interactive filtering and data exploration

Instead of manually maintaining datasets, the dashboard uses **REST APIs and automated Power Query transformations** to retrieve and process external data.

---

## 🏗️ Architecture

```text
                    ┌─────────────────────┐
                    │      REST APIs      │
                    ├─────────────────────┤
                    │ GNews API           │
                    │ NewsData.io         │
                    │ AllSportsAPI        │
                    │ EODHD               │
                    │ WeatherAPI          │
                    │ ZenQuotes            │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │    Power Query      │
                    │       / M           │
                    ├─────────────────────┤
                    │ API Requests        │
                    │ JSON Parsing        │
                    │ Data Cleaning       │
                    │ Transformation      │
                    │ Type Conversion     │
                    └──────────┬──────────┘
                               │
                 ┌─────────────┴─────────────┐
                 ▼                           ▼
       ┌──────────────────┐        ┌──────────────────┐
       │ Current Data     │        │ Historical Data  │
       │ Tables           │        │ Storage Tables   │
       └────────┬─────────┘        └────────┬─────────┘
                │                           │
                └─────────────┬─────────────┘
                              ▼
                    ┌─────────────────────┐
                    │    Power BI Model   │
                    ├─────────────────────┤
                    │ DAX Measures        │
                    │ KPIs                │
                    │ Calculations         │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Interactive Dashboard│
                    └─────────────────────┘