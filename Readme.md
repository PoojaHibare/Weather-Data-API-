# **Weather Data API 🌍🌦️**

This project is a **Flask-based Weather Data API** built to serve historical weather data.
It uses **temperature datasets** from multiple weather stations and provides structured JSON responses through well-defined endpoints.

The API allows you to:

* Explore available **weather stations**
* Fetch **temperature for a specific date**
* Retrieve **all temperature records** of a station
* Extract **year-wise weather data**

## 📂 Project Structure

├── **main.py**                     # Flask application (API logic)

├── **templates**/
│   └── **home.html**               # Homepage template rendered with Jinja2

├── **data_small**/                 # Dataset directory
│   ├── **stations.txt**            # List of all weather stations
│   └── **TG_STAIDxxxxx.txt**       # Daily temperature data for each station

├── **.gitignore**                  # Ignore unnecessary files

└── **README.md**                   # Project documentation

## 🔑 Components

1. **main.py**

* Entry point of the application.
* Uses **Flask** for API routing and **Pandas** for data handling.
* Defines endpoints for:
*     Homepage (station info)
*     Temperature lookup by station/date
*     All records for a station
*     Year-wise records

2. **templates/home.html**

* Frontend landing page of the API.
* Shows:
*     Project title
*     Example API usage
*     Table of available stations (rendered via stations.to_html())

3. **data_small/**

* Contains raw data files.
* **stations.txt**
*     Provides station IDs (STAID) and names (STANAME).
* **TG_STAIDxxxxx.txt (one per station)**
*     Contains daily weather observations.
*     Columns:
*         DATE → Date of observation (YYYY-MM-DD)
*         TG → Mean temperature (tenths of °C, converted to °C in API)

## 🌐 API Endpoints

1. **Homepage**

http://127.0.0.1:5000/
* Displays list of stations in HTML format.
* Provides examples of API usage.

2. **Single Station - Single Date**

(/api/v1/<station>/<date>)
* Fetches the temperature of one station on a given date.
* **Example:**
    http://127.0.0.1:5000/api/v1/10/1988-10-25
* **Response:**
    {
        "station": "10",
        "date": "1988-10-25",
        "temperature": 14.5
    }

3. **Single Station - All Records**

(/api/v1/<station>)
* Returns all available weather records for the given station.
* **Example:**
    http://127.0.0.1:5000/api/v1/10
* **Response (truncated for clarity):**
    [
        {"DATE": "1988-01-01", "TG": 25},
        {"DATE": "1988-01-02", "TG": 27},
        ...
    ]

4. Yearly Data

(/api/v1/yearly/<station>/<year>)
Fetches all temperature records for a station within a specific year.
**Example:**
    http://127.0.0.1:5000/api/v1/yearly/10/1990
**Response:**
    [
        {"DATE": "1990-01-01", "TG": 15},
        {"DATE": "1990-01-02", "TG": 16},
        ...
    ]

## 📊 Dataset Details

The dataset consists of station **metadata and temperature** records:

* **stations.txt**
*     List of station IDs and names.
*     Used to identify which station data to query.
* **TG_STAIDxxxxx.txt**
*     Each file corresponds to a single station.
*     Format:
*         DATE: YYYY-MM-DD
*         TG: Mean temperature in tenths of °C (API converts to °C by dividing by 10).

Example raw data snippet:

    DATE     TG
19880101    25
19880102    27
19880103    -5

## 🖥️ Homepage Preview

The homepage (home.html) provides:

* **Title & description** of the API
* **Sample URLs** for testing endpoints
* **Station list** in table format (rendered with Pandas .to_html())