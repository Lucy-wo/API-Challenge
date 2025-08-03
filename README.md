# Weather & Vacation Planner (WeatherPy + VacationPy)

## Summary
This project pulls global weather data, cleans it, and builds **interactive heatmaps** to visualize climate patterns (e.g., humidity). It then filters for **“ideal weather” cities** and overlays **nearby hotel markers** on the map—creating a simple, data-driven vacation planner.

---

## Goal
- Demonstrate end-to-end use of public APIs for **data collection → cleaning → geospatial visualization**.
- Help travelers (or travel teams) **discover destinations** that match preferred weather conditions and **see hotel options** at a glance.

---

## Procedure
1. **Collect weather data**
   - Query OpenWeather (One Call / Current Weather) for many cities worldwide.
   - Store features such as latitude/longitude, temperature, humidity, wind, cloudiness.
   - Save the unified dataset to `final_weather_data.csv`.

2. **Clean & prepare**
   - Remove duplicates/nulls, cast numeric types, standardize column names.
   - Create derived fields (e.g., humidity as a 0–1 weight for heatmaps).

3. **Visualize climate**
   - Build a **Google Maps heatmap** (via `gmaps`) weighted by humidity.
   - Tune parameters like `dissipating`, `max_intensity`, and `point_radius` for readability.

4. **Filter “ideal weather” cities**
   - Apply user-defined thresholds (e.g., moderate temp, reasonable humidity/wind).
   - Produce a shortlist for hotel search.

5. **Add hotels**
   - Use **Google Places** Nearby Search to fetch the top hotel for each shortlisted city.
   - Overlay a **marker layer** with info boxes (e.g., “Hotel name: Glace Bay”, “Tasiilaq”, “Vestmannaeyjar”).

6. **Notebooks**
   - `WeatherPy.ipynb`: data collection/cleaning and base visualizations.
   - `VacationPy.ipynb`: heatmap + hotel overlay and trip exploration.

---

## Result
- An **interactive humidity heatmap** highlighting clusters across North America, the North Atlantic, Iceland/Greenland, and Scandinavia.
- A second map with **hotel markers** on top of the heatmap; clicking shows hotel names in info boxes.
- A clean CSV (`final_weather_data.csv`) ready for further analysis or dashboards.

> If you see the “For development purposes only” watermark on the maps, configure a valid Google Maps API key with billing enabled and proper key restrictions.

---

## Business Impact
- **Faster destination discovery:** Quickly match customers to regions with preferred weather conditions.
- **Personalized offers:** Pair climate filters with **hotel availability** to surface relevant deals.
- **Market insights:** Identify **seasonal/weather clusters** to plan marketing, staffing, and inventory.
- **Reusable data asset:** The curated weather table can feed forecasting, dynamic pricing, or route planning.

---

## Next Steps to Make It Better
1. **API & keys**
   - Add a `.env` template and instructions; resolve Google Maps billing/key restrictions.

2. **Richer features**
   - Incorporate precipitation, UV index, air quality, seasonality, and historical normals.
   - Compute a **comfort index** (weighted score) and run **K-Means** clustering for “climate archetypes.”

3. **Hotel search & UX**
   - Return top *N* hotels with ratings/price bands; custom map icons; city-level tooltips.

4. **Open maps**
   - Provide a Folium/Leaflet fallback to avoid Google key requirements.

5. **Reproducibility**
   - Add `requirements.txt`, data schema checks, and a small CLI to refresh data (`make refresh-data`).
   - Optional: containerize with Docker; schedule refresh via GitHub Actions.

6. **Productization**
   - Publish a **Streamlit/Dash** app so users can set filters and download itineraries.

---

## Quick Start
```bash
# 1) Environment
python -m venv .venv && source .venv/bin/activate     # Windows: .venv\Scripts\activate
pip install -U pip pandas numpy jupyter gmaps requests python-dotenv folium

# 2) API keys
# Create a .env file with:
# OPENWEATHER_API_KEY=your_key_here
# GOOGLE_API_KEY=your_key_here

# 3) Run notebooks
jupyter notebook WeatherPy.ipynb
jupyter notebook VacationPy.ipynb
````

---

## Repository

```
.
├── WeatherPy.ipynb
├── VacationPy.ipynb
├── final_weather_data.csv
└── README.md
```
