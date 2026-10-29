# GANS — European Cities, Weather & Flights ETL
**Python · pandas · requests · BeautifulSoup · SQLAlchemy · MySQL**  
Data collection and relational-modelling coursework project.

## Business question
How can city, weather and flight-arrival information from different sources be brought into a common database for urban or mobility analysis?

## Deliverable
[The notebook](gans_cities_final.ipynb) contains a pipeline that:
1. Scrapes city coordinates and population information from Wikipedia.
2. Requests weather forecasts from OpenWeatherMap.
3. Finds nearby airports and requests arrivals through AeroDataBox/RapidAPI.
4. Normalises responses with pandas.
5. Creates and loads six related MySQL tables.

The configured city list contains 23 European cities, including Landsberg am Lech. This is the input list, not a claim that every source request succeeds.

## Data model
| Table | Purpose |
| --- | --- |
| `cities` | City identifiers, names and coordinates |
| `populations` | Population values linked to a city |
| `weathers` | Forecast observations linked to a city |
| `airports` | Airport identifiers and names |
| `cities_airports` | Many-to-many relationship between cities and airports |
| `flights` | Flight-arrival records linked to airports |

## What this project practises
- Reading HTML and JSON responses.
- Working with HTTP errors, timeouts and missing observations.
- Transforming API records into DataFrames and related database tables.
- Modelling keys and a junction table.
- Identifying where data provenance and repeatable loading need improvement.

## Run locally
1. Create a Python environment and install dependencies from `requirements.txt`.
2. Install Jupyter if it is not already available.
3. Start a local MySQL instance and provide a dedicated, disposable database.
4. Configure OpenWeatherMap, RapidAPI/AeroDataBox and MySQL settings in the notebook. Keep personal keys out of commits.
5. Review the export cells before running the notebook from top to bottom.

**The current export code drops and recreates the configured database. Use only a disposable project database.**

## Validation and limits
- The published notebook has no saved execution outputs. A fresh end-to-end run needs working API credentials, provider access and MySQL; it was not performed for this documentation revision.
- Wikipedia layouts can change. Population parsing is heuristic, and several missing populations are manually supplied without a recorded source date.
- The population timestamp uses the execution year; it is not evidence of the population's reference year.
- API availability and subscription access affect coverage. Empty responses must not be interpreted as confirmed zero activity.
- Overlapping airport searches may collect the same arrivals more than once.
- This is an ETL learning project, not a validated demand forecast or GIS decision model.

## Next improvements
- Record source URL, retrieval time and reference year separately.
- Store configuration in environment variables.
- Add an offline sample, unique load keys and non-destructive upserts.
- Save a successful run and publish a compact coverage/data-quality report.

[Portfolio](https://github.com/nuvazic-pixel)
