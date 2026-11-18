# Airbnb Listings Analysis

## Step 1: Load the Dataset

I loaded `AB_NYC_2019.csv` into a pandas DataFrame in Google Colab.

## Step 2: Check the Dataset Structure

I checked the first few records, column data types, and missing values. The dataset includes listing details, location information, price, minimum-night requirements, review information, and availability.

## Step 3: Check for Duplicate Records

The duplicate-record check returned **0 duplicate rows**.

## Step 4: Check Unique Values

- `room_type` and `neighbourhood_group` contain a small number of categories.
- `id` is almost unique for every listing, so it should be treated as an identifier rather than a modeling feature.
- `price`, `minimum_nights`, reviews, and availability contain numerical values for further analysis.

## Step 5: Review Missing Values

The missing-value analysis produced these results:

- `last_review`: 10,052 missing values (20.56%).
- `reviews_per_month`: 10,052 missing values (20.56%).
- `host_name`: 21 missing values (0.04%).
- `name`: 16 missing values (0.03%).
- All remaining columns had no missing values.

## Step 6: Convert and Validate Review Dates

The `last_review` column was converted successfully to `datetime64[ns]` format.

- Missing review dates: 10,052.
- First review date: 2011-03-28.
- Last review date: 2019-07-08.

## Step 7: Plot Numerical Variable Distributions

I plotted histograms for price, minimum nights, number of reviews, reviews per month, and availability.

- Price is concentrated at lower values with a long right tail, indicating high-price outliers.
- Minimum nights is heavily concentrated at low values and has a long right tail.
- Number of reviews and reviews per month are right-skewed, with most listings having relatively low values.
- Availability has many listings with low availability and another concentration near full-year availability.

## Step 8: Analyze Airbnb Categories

I compared the number of listings by room type and neighbourhood group.

- Entire homes/apartments and private rooms represent most of the listings.
- Shared rooms represent a much smaller portion of the dataset.
- Manhattan and Brooklyn have the largest number of listings.
- Queens has fewer listings than Manhattan and Brooklyn, while the Bronx and Staten Island have the fewest listings.

## Step 9: Identify Numerical Outliers

I used the IQR method to identify potential outliers in the main numerical columns.

- `price`: 2,972 potential outliers (6.08%).
- `minimum_nights`: 6,607 potential outliers (13.51%).
- `number_of_reviews`: 6,021 potential outliers (12.31%).
- `reviews_per_month`: 1,793 potential outliers (3.67%).
- `availability_365`: 0 potential outliers.

The outlier counts were recorded for the data-cleaning and anomaly-handling stage.

## Step 10: Review Extreme Airbnb Values

I reviewed the highest values and summary percentiles for the numerical columns.

- `price` ranges from 0 to 10,000, with several listings at extremely high prices.
- `minimum_nights` ranges from 1 to 1,250, with some listings requiring unusually long stays.
- `number_of_reviews` reaches 629, while most listings have much lower review counts.
- `reviews_per_month` reaches 58.5 and has a strong concentration near lower values.
- `availability_365` ranges from 0 to 365 and does not exceed the expected yearly limit.

The extreme records were identified for anomaly-handling decisions.

## Step 11: Remove Duplicate Records

I created a cleaned Airbnb DataFrame using `drop_duplicates()`.

- Original rows: 48,895.
- Cleaned rows: 48,895.
- Rows removed: 0.

## Step 12: Handle Missing Values

I handled the missing Airbnb values before feature processing.

- Missing text values in `name` and `host_name` were replaced with `Unknown`.
- Missing `reviews_per_month` values were replaced with 0 because they represent listings without reviews.
- A `has_review` indicator was added before filling missing review dates.
- Missing `last_review` values were filled using the median review date.
- The imputed dataset retained 48,895 rows.

## Step 13: Encode Airbnb Categorical Features

I converted `room_type` and `neighbourhood_group` into numerical indicator columns using one-hot encoding.

- The encoded Airbnb dataset contains 48,895 rows and 21 columns.

## Step 14: Select and Scale Airbnb Modeling Features

I removed identifier and text fields that were not suitable for numeric modeling and standardized the selected numeric features.

- The scaled feature set was prepared for clustering and machine-learning models.

## Step 15: Perform K-Means Clustering

I applied K-Means clustering with three clusters to the scaled Airbnb features.

- Cluster 0: 20,464 listings.
- Cluster 1: 22,585 listings.
- Cluster 2: 5,846 listings.
- Silhouette score: 0.274.

## Step 16: Remove Airbnb Anomalies

I removed invalid values and IQR-based outliers from the main Airbnb numerical features.

- Original rows: 48,895.
- Rows after anomaly removal: 32,479.
- Rows removed: 16,416.

## Step 17: Prepare Airbnb Data for AutoML

I created date-based review features, removed identifier and high-cardinality text fields, encoded categorical variables, and split the data for modeling.

- Training dataset: 25,983 rows and 17 columns.
- Testing dataset: 6,496 rows and 17 columns.
- Target column: `price`.
