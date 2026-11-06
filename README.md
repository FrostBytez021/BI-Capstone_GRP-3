# SteamScope

A web-based business intelligence dashboard for estimating and analyzing game sales on Steam.

**McReg Analytics** (3DSA1, Group 3), DSA4157 Business Intelligence, University of Santo Tomas
Mikaela Angela Carlos · Drei Cerise Dayag · Althea Marie Habaluyas · Maria Camela Oliva

## Overview

Steam does not publish sales figures, so this project estimates units sold and gross revenue from public data. A Python pipeline (`steam_scraper.py`) collects data from four public Steam sources into a 26-table SQLite database. After cleaning, the dataset has **990 games** (747 paid, 243 free-to-play), all with 1M+ estimated owners, collected on 19–21 October 2026.

> **Additional Plan:** to increase row counts, we plan to combine the Steam dataset with data from other storefronts such as the Epic Games Store.

## Data sources

No API keys are needed.

| Source | Endpoint | Provides |
|---|---|---|
| SteamSpy | `steamspy.com/api.php` | Game list, owner estimates, tags, concurrent players |
| Steam Store API | `store.steampowered.com/api/appdetails` | Genres, developers, publishers, platforms, languages, requirements, media, DLC, ratings, prices (6 countries) |
| Steam Reviews API | `store.steampowered.com/appreviews` | Review summary and up to 50 sampled reviews per game |
| Steam Web API | `api.steampowered.com` | Achievement unlock percentages |

## Where to find what

| Looking for… | Where |
|---|---|
| Data collection code | `steam_scraper.py` |
| Database schema | `schema.sql` |
| Game list (one row per game) | `apps` table |
| Developers, publishers, genres, categories, tags, languages | Dimension tables, linked through `app_*` bridge tables |
| Prices | `app_prices` |
| Owner estimates | `app_spy_stats` |
| Review counts and sampled reviews | `app_review_summary`, `reviews` |
| Achievements | `app_achievements` |
| Platforms, requirements, screenshots, movies, DLC, ratings | `app_platforms`, `app_requirements`, `app_screenshots`, `app_movies`, `app_dlc`, `app_content_descriptors`, `app_ratings` |
| Calendar table | `dim_date` |
| Methodology, cleaning log, KPIs, findings, limitations | Activity #3 report (`BI_ACT3.pdf`) |

## Notes

- Revenue figures are gross estimates for ranking and comparison only, not actual earnings.
- The `reviews` table contains public Steam user IDs. Don't redistribute it or use it to identify individuals.
- Credit SteamSpy and Steam as data sources.
