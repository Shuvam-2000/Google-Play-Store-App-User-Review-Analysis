1. Project Overview
2. Problem Statement
3. Import Libraries

4. Dataset 1: Google Play Store Apps
   - Load Dataset
   - Dataset Overview
   - Data Cleaning
   - EDA

GOOGLE PLAY STORE APPS EDA
│
├── 1. Univariate Analysis
│   │
│   ├── Category distribution
│   ├── Type distribution
│   ├── Content Rating distribution
│   ├── Top Genres
│   ├── Rating distribution
│   ├── Reviews distribution
│   ├── Installs distribution
│   ├── Price distribution
│   └── Size distribution
│
├── 2. Bivariate Analysis
│   │
│   ├── Rating vs Reviews
│   ├── Rating vs Installs
│   ├── Type vs Rating
│
└── 3. Multivariate Analysis
    │
    ├── Correlation Heatmap

5. Dataset 2: Google Play Store User Reviews
   - Load Dataset
   - Dataset Overview
   - Data Cleaning
   - EDA

6. Merge Both Datasets (if needed)

7. Combined Analysis
   - Ratings vs Sentiment
   - Category vs Sentiment
   - Installs vs Sentiment
   - Reviews vs Rating
   - etc.

8. Key Insights

9. Conclusion

Suggested preprocessing order
Check missing values (isnull().sum()).
Check duplicate rows and duplicate app names.
Convert data types:
Reviews → int
Installs → int
Price → float
Last Updated → datetime
Clean Size and convert to a numeric unit (e.g., MB).
Handle "Varies with device" appropriately (especially in Size; optionally treat it as missing in version columns).
Validate ranges and categories (e.g., ratings between 1 and 5).

Check For Outliers:
Rating
Reviews
Installs
Price
Size


COMBINED ANALYSIS
│
├── 1. Keep cleaned datasets
│
├── 2. Aggregate User Reviews by App
│      ├── Review count
│      ├── Positive %
│      ├── Negative %
│      ├── Neutral %
│      ├── Avg Polarity
│      └── Avg Subjectivity
│
├── 3. Quick checks on review summary
│
├── 4. Merge with App dataset using App
│
├── 5. Merge-specific sanity checks
│
├── 6. Combined Visualizations
│      ├── Category vs Sentiment
│      ├── Type vs Sentiment
│      ├── Rating vs Sentiment
│      └── Installs vs Sentiment
│
├── 7. Insights for each visualization
│
└── 8. Final Combined Analysis Conclusion