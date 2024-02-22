# Weather Data Collection via NOAA API Guide

This document provides a guide on how to collect weather data from the NOAA (National Oceanic and Atmospheric Administration) Climate Data Online (CDO) web services. Specifically, we will focus on retrieving data from two weather stations: Los Angeles International Airport (LAX) and New York City Central Park.
* See, **HOWtoGet_WeatherData.ipynb**
## NOAA Climate Data Online: Web Services Documentation

NOAA's Climate Data Online (CDO) provides free access to NCDC's archive of global historical weather and climate data in addition to station history information. Data can be accessed via the CDO Web Services API.

For more information, refer to the official documentation:
[Climate Data Online: Web Services Documentation](https://www.ncdc.noaa.gov/cdo-web/webservices/v2)

## Measurement Locations

### Los Angeles LAX Weather Station

- **Elevation**: 29.7 meters
- **Date Range**: 1944-01-01 to 2024-02-20
- **Latitude**: 33.93816
- **Location Name**: LOS ANGELES INTERNATIONAL AIRPORT, CA US
- **Data Coverage**: 100%
- **Station ID**: GHCND:USW00023174
- **Longitude**: -118.3866

### New York Central Park Weather Station

- **Elevation**: 42.7 meters
- **Date Range**: 1869-01-01 to 2024-02-19
- **Latitude**: 40.77898
- **Location Name**: NY CITY CENTRAL PARK, NY US
- **Data Coverage**: 100%
- **Station ID**: GHCND:USW00094728
- **Longitude**: -73.96925

## Collecting Data Using Google Colab

To collect data from NOAA's API using Google Colab, follow these steps:

1. **Set Up Google Colab Notebook**: Open Google Colab and create a new notebook.

2. **Install Required Libraries**: Ensure your Colab environment has the necessary libraries installed. You might need `requests` for making API calls. Use the following command to install it if needed:
    ```python
    !pip install requests
    !pip install pandas
    ```

3. **Define API Key**: Sign up for a NOAA API key [here](https://www.ncdc.noaa.gov/cdo-web/token) and define it in your notebook:
    ```python
    api_key = 'YOUR_API_KEY'
    ```
## Configuring the Folder Path

4. Before starting the data collection process, configure the folder path where you want to save the CSV files:

    ```python
    folder_path = "Path_to_save_CSV_files"
## Configuring Variables for Data Collection

5. Before initiating the data collection process, several variables need to be configured to specify the data you wish to retrieve:

   - `station_id`: This identifies the weather station from which you want to collect data. Ensure you use the correct station ID as per NOAA's listings.
   - `location_name`: A user-friendly name for the location associated with the `station_id` to help identify the data context in your project.
   - `year`: The year for which you want to collect data.
   - `start_month`, `start_month_day`, `end_month`, `end_month_day`: These variables allow you to define the specific start and end dates of the data collection period within the specified year.

   For example, to collect data for New York Central Park for the entire year of 1990:

    ```python
    api_key = "YOUR_API_KEY"  # Replace with your actual API key
    station_id = "USW00094728"  # Station ID for New York Central Park
    location_name = "NY"  # Short name for the location
    year = "1990"
    start_month = "01"
    start_month_day = "01"
    end_month = "12"
    end_month_day = "31"

6. **Make API Request**: Use the `requests` library to make a GET request to the NOAA API. Here's an example to fetch data from the Los Angeles LAX weather station:
    ```python
    import requests

    url = "https://www.ncdc.noaa.gov/cdo-web/api/v2/data"
    headers = {"token": api_key}
    records = []

    for data_type in data_types:
        params = {
            "datasetid": "GHCND",
            "stationid": f"GHCND:{station_id}",
            "startdate": start_date,
            "enddate": end_date,
            "datatypeid": data_type,
            "limit": 1000,
            "units": "metric"
        }

        response = requests.get(url, headers=headers, params=params)
        data = response.json()
    ```
7. **Additional Function**: The `calculate_monthly_averages_and_save` function calculates monthly averages and generates a CSV file.
8. **Process and Analyze Data**: After retrieving the data, you can process and analyze it according to your needs.

9. **Repeat for Other Locations**: Modify the `stationid`, `startdate`, and `enddate` parameters to collect data from other locations or time ranges.

This guide provides a basic overview of collecting weather data from NOAA's CDO web services using Google Colab. For detailed analysis or more complex queries, refer to the official API documentation.
