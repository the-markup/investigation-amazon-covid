# TK
This repository contains code and data to reproduce the findings featured in our story, "[TK](TK)."

Jupyter notebooks used for data collection, preprocessing, and analysis are in the `notebooks` folder.

## Installation
### Python
Make sure you have Python 3.6+ installed. We used [virtualenv](https://docs.python-guide.org/dev/virtualenvs/) to create a Python 3.8 virtual environment.

Then install the Python packages:<br>
`pip install -r requirements.txt`

To run `0-download-oregon-health-data.ipynb`, you must download tika, which is used to convert the pdf files to xml. If you use [brew](https://formulae.brew.sh/formula/tika), you can simply run `brew install tika`. This notebook has been tested on OS X, installation may vary depending on your operating system.

## Notebooks
These notebooks have already been run and do not need to run sequentially.

### `0-download-oregon-health-data.ipynb`

This notebook downloads [historical outbreak data](https://www.oregon.gov/oha/covid19/Documents/DataReports/Weekly-Outbreak-COVID-19-Report.pdf) from the Oregon Health Authority, and converts them from PDF files to XML files.

### `1-extract-tables-from-oregon.ipynb`

This notebook takes XML files output from `0-download-oregon-health-data.ipynb` and extracts workplace outbreak data from them. It then outputs that data as `../output/oha-data-{latest_report}.csv`, where `{latest_report}` is the date of the latest report release, formatted as `%Y-%m-%d`.

### `2-filter-chart-oregon-data.ipynb`

This notebook generates the following filtered CSVs: 

- `../output/amazon-covid-reports-all.csv`
- `../output/cumulative-cases-data.csv`
- `../output/longest-outbreaks.csv`

To run this notebook in its entirety, `ITA Data CY 2020 - Sept.csv` must be downloaded from [OSHA](https://www.osha.gov/Establishment-Specific-Injury-and-Illness-Data) and placed in the `data` folder.

### `3-closed-osha-complaints.ipynb`

This notebook filters OSHA complaint data down to just those related to Amazon facilities. To run this notebook in its entirety, `Closed_Federal_State_Plan_Valid_COVID-19_Complaints_Through_1029_2021.xlsx` must be downloaded from [OSHA](https://www.osha.gov/foia/archived-covid-19-data#closed-oct-2021) and placed in the `data` folder. This notebook filters that dataset to just complaints relevant to Amazon warehouses, and exports that as `../output/osha-amazon-closed-complaints.csv`.

## Data

| File | Description |
|------|-------------|
|**`../data/The Markup - Amazon COVID-19 inspections Fed+State as of Oct 31 2021.xlsx`**| Federal and state OSHA inspections of Amazon warehouses as of October 31, 2021. This data is a response to a FOIA request made by The Markup. |
|**`../output/osha-amazon-closed-complaints.csv`**| A filtered list of publicly available closed complaint data, which is available on [OSHA's website](https://www.osha.gov/foia/archived-covid-19-data#closed-oct-2021). |
|**`../output/oha-data-2021-12-15.csv`**| Workplace outbreak counts scraped from Oregon Health Authority outbreak reports from March 10, 2021 to December 15, 2021. |
| **`../output/amazon-covid-reports-all.csv`** | A filtered version of `../output/oha-data-{latest_report}.csv` that only includes Amazon warehouse data. |
| **`../output/cumulative-cases-data.csv`** | Culmulative COVID-19 counts over time for PDX7 and PDX9, based on weekly [Oregon Health Authority outbreak reports](https://www.oregon.gov/oha/covid19/Documents/DataReports/Weekly-Outbreak-COVID-19-Report.pdf). Dates are based on when the data is considered "finalized," which is specified in the introduction of each report. This is typically the Sunday before the report comes out. |
|**`../output/longest-outbreaks.csv`**| A top ten list of workplaces with the longest COVID-19 outbreaks based on Oregon Health Authority reports as of TK, 2021. The outbreak length is calculated as the time between when the outbreak investigation began, and the date of the most recent onset. OHA considers an outbreak "resolved" |
