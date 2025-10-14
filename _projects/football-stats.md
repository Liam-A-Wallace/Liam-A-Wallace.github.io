---
layout: project
title: "Football Statistics Analysis System"
description: "Automated data pipeline collecting 20+ metrics from 400+ weekly player/team records with interactive visualizations"

github_url: https://github.com/Liam-A-Wallace/footballScraper  # Add your actual GitHub URL
---

## Project Overview

I developed a comprehensive football statistics analysis system that automates data collection, processing, and visualization for the Scottish Premiership. The system gathers extensive player and team data from FBRef, processes it through a robust pipeline, and provides interactive analysis tools.

## Key Features

- **Automated Data Scraping:** Collects 20+ player metrics and team statistics from FBRef
- **Multi-format Storage:** Supports both CSV and SQLite database storage with upsert operations
- **Interactive Analysis:** CLI interface with multiple visualization options including bar charts, radar charts, and scatter plots
- **Data Validation:** Comprehensive cleaning pipeline handling missing values, data type conversion, and outlier removal
- **Relationship Mapping:** Database relationships between players and teams with foreign key constraints

## Technical Implementation

The system is built with a modular Python architecture separating concerns into distinct components:

**Data Collection Layer**

BeautifulSoup web scraping with rate limiting and error handling
Dynamic URL discovery and cleaning for team-specific pages
Header normalization for complex table structures with duplicate columns

**Data Processing Pipeline**

Type conversion and data validation in cleaner modules
Calculation of derived metrics (goals per minute, efficiency rates)
Handling of edge cases (multiple nationalities, position variations)

**Storage & Analysis**

SQLite with proper schema design and foreign key relationships
Pandas for data manipulation and statistical analysis
Matplotlib/Seaborn for static visualizations and Plotly for interactive charts

## Challenges & Solutions

**Web Scraping Complexity:** FBRef uses complex table structures with nested headers. Solved by implementing multi-level header parsing and duplicate column resolution.

**Data Consistency:** Player names and team data required extensive cleaning. Developed normalization functions handling special characters, multiple positions, and inconsistent formatting.

**Performance Optimization:** Rate limiting between requests to avoid being blocked, while maintaining acceptable scrape times for 12 teams and 400+ players.

**Database Integrity:** Implemented UPSERT operations to handle incremental updates and maintain referential integrity between league and player tables.