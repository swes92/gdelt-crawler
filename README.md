# GDELT Crawler README

## Introduction
This is a simple code wrapper for the gdeltPyR module from [linwoodc3](https://github.com/linwoodc3/gdeltPyR). It enables the download of data over large timespans without producing unnecessarily large files by allowing you to pre-filter the daily entries. Make sure you have gdeltPyR installed in your environment.
```python
pip install gdelt
```
For questions regarding the module, please refer to the respective documentation.

Please see import cell for further dependencies:
```python
import pandas as pd
import gdelt
import datetime
import time
```
## About GDELT
[GDELT](https://www.gdeltproject.org/) (Global Database of Events, Language, and Tone) is a project that monitors the world's news media from nearly every corner of every country in print, broadcast, and web formats. It processes the news information to provide a comprehensive view of global events, helping researchers and analysts understand patterns, trends, and dynamics in global society.

## Usage
To use the GDELT Crawler, call the function `gd_crawler(start_date, end_date)` with the desired start and end dates in the format 'YYYY MM DD'. The function will download GDELT data for each day within the specified date range and apply filters to the entries.

### Applying Filters
Familiarize yourself with the data structure of the GDELT tables and the available options for filtering. Modify the code snippet under the comment "Apply filters here" within the `gd_crawler` function to apply custom filters to the GDELT data. By default, as shown in the example, the code filters events based on Actor1CountryCode and QuadClass. You can adjust these filters or add new ones based on your specific requirements.
```python
# Apply filters here
results_filtered = results.dropna(subset=['Actor1CountryCode', 'QuadClass'])
results_filtered = results_filtered[(results_filtered['Actor1CountryCode'] == 'CHN') | (results_filtered['Actor1CountryCode'] == 'TWN')]
results_filtered = results_filtered[(results_filtered['QuadClass'] == 3) | (results_filtered['QuadClass'] == 4)]
```

### Output CSV Files
Two CSV files are generated:
- **Data CSV**: Contains the raw GDELT data with applied filters, named as 'start_date - end_date.csv'.
- **Control CSV**: Contains metrics such as the number of entries, matched entries, and match percentage for each date, named as 'start_date - end_date - control.csv'.

### Log Files and Metrics
A log file named 'gd_crawler_log.txt' is created to record processing information and errors encountered during execution. Metrics such as processing time, progress, and errors are logged for each date processed. By being able to track the progress and have the .csv saved after each day, it is possible to restart the process in case of errors or with the download. To do so, simply create a new query with an adjusted timeframe and merge the two .csv-files later manually.

## Acknowledgement
This GDELT Crawler utilizes the gdeltPyR module developed by [linwoodc3](https://github.com/linwoodc3).

## License
This project is distributed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for more details.
