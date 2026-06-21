# French Travel Destination Recommender

End-to-end data pipeline that scrapes hotel data from Booking.com, enriches it with geolocation and weather forecasts, and recommends the best French destinations based on hotel ratings and upcoming temperatures.

---

## What it does

1. Scrapes hotel names, ratings, links, and descriptions for 35 French cities from Booking.com (Scrapy)
2. Retrieves each hotel's address by crawling its individual Booking.com page (BeautifulSoup)
3. Geocodes hotel addresses to latitude/longitude via the Nominatim API (OpenStreetMap)
4. Fetches 7-day maximum temperature forecasts for each city via the OpenWeatherMap API
5. Stores the enriched dataset in an AWS S3 data lake and exports it to a SQLite database
6. Visualizes results on interactive maps: hotel ratings by city, temperature forecasts, and top-rated hotels

---

## Output

- **Top 5 warmest cities** for the next 7 days among the 35 destinations
- **Top 20 hotels** by rating across all cities
- Interactive Plotly geospatial maps overlaying hotel ratings and temperature forecasts

---

## Pipeline

```
Booking.com (Scrapy)
    └── Hotel names, ratings, links, descriptions
          └── BeautifulSoup (per-hotel page)
                └── Hotel addresses
                      └── Nominatim API
                            └── Latitude / Longitude
                                  └── OpenWeatherMap API
                                        └── 7-day temperature forecast
                                              ├── AWS S3 (data lake)
                                              └── SQLite (local database)
```

---

## Tech Stack

| Package | Role |
|---|---|
| `scrapy` | Hotel scraping from Booking.com |
| `beautifulsoup4` | Per-hotel address extraction |
| `requests` | Nominatim and OpenWeatherMap API calls |
| `boto3` | AWS S3 data lake storage |
| `sqlite3` | Local SQL database export |
| `pandas` | Data cleaning and aggregation |
| `plotly` | Interactive geospatial maps |

---

## Cities covered

35 destinations across France, including Paris, Lyon, Marseille, Strasbourg, Annecy, Biarritz, Mont Saint-Michel, Carcassonne, and more.

---

## Files

| File | Description |
|---|---|
| `Version_finale_projet1_Matthieu_Marechal.ipynb` | Full pipeline notebook |
| `scrap_booking.json` | Raw scraping output |
| `hotels.csv` | Enriched hotel dataset (geocoded + weather) |
| `cities_hotels_meteo.csv` | City-level aggregated data |
| `Matthieu.db` | SQLite database |

---

## Installation

```bash
git clone https://github.com/mmatthieu1290/Project1
cd Project1
pip install scrapy beautifulsoup4 requests boto3 pandas plotly lxml
```

**API keys required:**
- [OpenWeatherMap](https://openweathermap.org/api) — set your key in the notebook before running
- AWS credentials — configure via `aws configure` or environment variables
