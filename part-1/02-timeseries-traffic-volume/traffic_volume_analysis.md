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

## Step 8: Analyze Traffic by Hour and Day

I calculated average traffic volume by hour of day and day of week.

- Traffic volume is lowest during overnight hours.
- Traffic volume increases sharply during the morning and reaches a high level during the afternoon.
- Traffic volume declines during the evening.
- Weekday traffic is higher than weekend traffic.
- Friday has the highest average among the displayed days, while Sunday has the lowest.

## Step 9: Identify Numerical Outliers

I used the IQR method to identify potential outliers in the main numerical columns.

- `temp`: 10 potential outliers (0.02%).
- `rain_1h`: 3,467 potential outliers (7.19%).
- `snow_1h`: 63 potential outliers (0.13%).
- `clouds_all`: 0 potential outliers.
- `traffic_volume`: 0 potential outliers.

The `rain_1h` column has the largest number of potential outliers and requires attention during anomaly handling.

## Step 10: Review Extreme Traffic Values

I reviewed the highest rainfall values and summary percentiles for the numerical columns.

- `temp` ranges from 0 to approximately 310.07, with very few extreme observations.
- `rain_1h` has a median of 0, a 99th percentile of approximately 237.98, and a maximum of 9,831.30.
- `snow_1h` ranges from 0 to 0.51, with a small number of potential outliers.
- `clouds_all` remains within the expected 0–100 range.
- `traffic_volume` ranges from 0 to 7,280 and was not flagged as an IQR outlier.

The extreme rainfall records were identified for anomaly-handling decisions.

## Step 11: Remove Duplicate Records

I created a cleaned traffic DataFrame using `drop_duplicates()`.

- Original rows: 48,204.
- Cleaned rows: 48,187.
- Rows removed: 17.

## Step 12: Handle Missing Values

I treated missing values in the traffic dataset before feature processing.

- Missing values in `holiday` were replaced with `No Holiday`, since blank values represent regular days.
- The imputed dataset retained 48,187 rows.

## Step 13: Create Traffic Time Features and Encode Categories

I created time-based features from `date_time` and encoded the main categorical weather fields.

- Added `hour`, `day_of_week`, `month`, `year`, and `is_weekend`.
- One-hot encoded `holiday` and `weather_main`.
- The processed traffic dataset contains 48,187 rows and 33 columns.

## Step 14: Select and Scale Traffic Modeling Features

I removed non-numeric date and text fields from the model inputs and standardized the selected traffic features. `traffic_volume` was kept separate as the prediction target.

- The scaled feature set was prepared for clustering and machine-learning models.

## Step 15: Perform K-Means Clustering

I applied K-Means clustering with three clusters to the scaled traffic features.

- Cluster 0: 24,461 records.
- Cluster 1: 5,676 records.
- Cluster 2: 18,050 records.
- Silhouette score: 0.147.

## Step 16: Remove Traffic Anomalies

I removed invalid traffic and weather values and applied IQR filtering to temperature and traffic volume. Rainfall spikes were retained because they can represent valid weather events.

- Original rows: 48,187.
- Rows after anomaly removal: 48,177.
- Rows removed: 10.

## Step 17: Prepare Traffic Data for AutoML

I created time-based features, removed date and high-cardinality text fields, encoded categorical variables, and used a chronological train-test split.

- Training dataset: 38,541 rows and 36 columns.
- Testing dataset: 9,636 rows and 36 columns.
- Target column: `traffic_volume`.

