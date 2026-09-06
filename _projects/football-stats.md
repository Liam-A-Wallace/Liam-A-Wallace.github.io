---
layout: project
title: "Football Statistics Analysis System"
description: "Built an automated data pipeline collecting over 20 statistical metrics across 400+ weekly player and team records, with a data cleaning and validation stage that ensured consistency across large datasets. Applied statistical analysis to identify trends and performance patterns, and built a lightweight interface for structured exploration of the resulting dataset."
technologies: [Python, BeautifulSoup, SQLite, Pandas, Matplotlib, Plotly]
github_url: https://github.com/Liam-A-Wallace/footballScraper
---

## What it does

Collects Scottish Premiership league and player statistics, then runs them through a cleaning and validation pipeline before storage and analysis. A command-line interface drives scraping or a synthetic-data generator, and the results land in SQLite or CSV ready for exploration.

## How it's built

- **Scraping** – a `requests` session with a descriptive user agent and retry/backoff; columns are keyed by FBRef's stable `data-stat` attributes rather than header text, so the parser survives season-to-season markup changes.
- **Cleaning** – typed, data-driven conversion: integers, floats, comma stripping, and age parsing ("23-056" → 23).
- **Storage** – SQLite with upsert-on-rerun and a composite `(Player, Team)` key, so two clubs can field players with the same name; CSV export included.
- **Analysis** – Pandas for statistical work, Matplotlib/Seaborn for static charts, and Plotly for interactive ones (standings, radar, scatter).
- **Demo mode** – a reproducible synthetic-data generator exercises the full pipeline offline, which keeps development and testing going now that FBRef blocks automated requests.

## Notable problems solved

- **Fragile scraping** – replaced hardcoded season table ids and header-text parsing with dynamic table discovery and `data-stat` column mapping.
- **Data consistency** – typed cleaning and normalisation so numeric columns are stored as numbers, not strings.
- **Polite fetching** – user-agent header, exponential backoff, and a random 5–9s delay between requests.
- **Integrity** – upsert operations keep league and player tables consistent across runs.
