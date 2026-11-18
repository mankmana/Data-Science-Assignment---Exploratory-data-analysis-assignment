# Traffic Volume Time-Series Analysis

## Step 1: Load the Dataset

I loaded `Metro_Interstate_Traffic_Volume.csv` into a pandas DataFrame in Google Colab.

## Step 2: Check the Dataset Structure

I checked the first few records, column data types, and missing values. The dataset contains weather information, a date-time field, and traffic-volume measurements.

## Step 3: Check the Dataset Size

The dataset contains **48,204 rows and 9 columns**.

## Step 4: Check for Duplicate Records

The duplicate-record check found **17 duplicate rows**. These records were identified for review during data preparation.

## Step 5: Review Missing Values

The missing-value analysis showed that:

- `holiday` contains 48,143 missing values, representing 99.87% of the dataset.
- All other columns contain 0 missing values.

## Step 6: Convert and Validate the Date-Time Column

The `date_time` column was converted successfully to `datetime64[ns]` format.

- Invalid date-time values: 0.
- First date: 2012-10-02 09:00:00.
- Last date: 2018-09-30 23:00:00.

## Step 7: Plot Traffic Volume Over Time

I plotted traffic volume over time and created a histogram of the traffic-volume values.

- Traffic volume varies considerably across the recorded time period.
- The time-series plot shows a visible gap or irregular coverage between parts of the time range.
- The traffic-volume distribution is not symmetric and contains multiple concentration areas.
- Traffic volume values extend from near zero to approximately 7,280.

