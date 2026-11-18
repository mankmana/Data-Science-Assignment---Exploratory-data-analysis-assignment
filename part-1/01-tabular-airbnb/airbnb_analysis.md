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
