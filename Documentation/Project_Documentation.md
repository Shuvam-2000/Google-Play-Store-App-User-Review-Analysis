# Google Play Store App & User Review Analysis

## 1. Project Overview

This project performs an end-to-end exploratory analysis of Google Play Store applications and user reviews.

The analysis combines app-level information such as category, rating, reviews, installs, price, size, and content rating with user-review information such as sentiment, sentiment polarity, and subjectivity.

The project follows:

**Data Cleaning → App EDA → Review EDA → Review Aggregation → Dataset Integration → Combined Analysis → Power BI Dashboard → Business Insights**

## 2. Problem Statement

The Google Play Store contains applications with different levels of popularity, ratings, pricing, and user experiences. App-level metrics alone do not fully explain how users perceive these applications.

This project analyzes both app-level and review-level data to identify patterns in popularity, engagement, ratings, and user sentiment, and to derive actionable business insights.

## 3. Objectives

- Clean and prepare both datasets.
- Perform univariate, bivariate, and multivariate EDA.
- Analyze app popularity using reviews and installs.
- Analyze sentiment using sentiment labels, polarity, and subjectivity.
- Aggregate review-level information at app level.
- Combine app and review datasets.
- Examine relationships between rating, popularity, and sentiment.
- Build an interactive Power BI dashboard.
- Derive business insights and recommendations.

## 4. Datasets

### Google Play Store Apps

Key fields include:

| Column | Description |
|---|---|
| App | Application name |
| Category | Application category |
| Rating | Average application rating |
| Reviews | Number of reviews |
| Size | Application size |
| Installs | Install bucket/value |
| Type | Free or Paid |
| Price | Application price |
| Content Rating | Target audience |
| Genres | Application genre |
| Last Updated | Last update date |
| Current Ver | Current application version |
| Android Ver | Required Android version |

### Google Play Store User Reviews

| Column | Description |
|---|---|
| App | Application name |
| Translated_Review | Translated user review |
| Sentiment | Positive, Neutral, or Negative |
| Sentiment_Polarity | Sentiment score from -1 to 1 |
| Sentiment_Subjectivity | Subjectivity score from 0 to 1 |

## 5. Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook
- Power BI
- PostgreSQL / SQL
- Git & GitHub

## 6. Project Workflow

```text
Raw App Dataset
      ↓
Data Cleaning
      ↓
App-Level EDA
      ↓
Raw Review Dataset → Review Cleaning → Review-Level EDA
                                      ↓
                              Review Aggregation
                                      ↓
                         App + Review Integration
                                      ↓
                              Combined Analysis
                                      ↓
                            Power BI Dashboard
                                      ↓
                         Insights & Recommendations
```

# 7. App Dataset Cleaning

### Initial Dataset

- 10,841 rows
- 13 columns

### Cleaning Performed

- Investigated and handled missing values.
- Removed the corrupted `Life Made WI-Fi Touchscreen Photo Frame` record.
- Removed the unusable missing-Type record for `Command & Conquer: Rivals`.
- Converted `Reviews` to integer.
- Cleaned `Installs` by removing commas and plus signs.
- Converted `Price` to numeric.
- Converted `Size` to MB.
- Converted `Last Updated` to datetime.
- Removed 483 exact duplicate rows.
- Investigated outliers and retained legitimate extreme observations.
- Duplicate application names were not automatically removed because they can represent legitimate observations.

### Missing-Value Decisions

Missing ratings were retained rather than artificially imputed because there was no defensible basis for estimating them.

Missing `Current Ver` and `Android Ver` values were retained because reliable values could not be inferred.

### Final Dataset

**9,658 rows × 13 columns**

Saved as:

`googleplaystore_cleaned.csv`

> **Important:** Install values are bucketed in the source data. Therefore, cleaned install values represent install-volume buckets rather than exact installation counts.

# 8. App-Level EDA

## Category Distribution

Family is the largest category, followed by Game and Tools. Category representation is uneven.

**Insight:** The app ecosystem in this dataset is concentrated in a limited number of major categories.

## Free vs Paid

Free applications heavily dominate the dataset.

**Insight:** The dataset represents a strongly free-oriented app ecosystem.

## Content Rating

`Everyone` is the dominant content-rating group.

**Insight:** Applications intended for broad audiences form the majority.

## Genres

Tools, Entertainment, Education, and Business are among the most represented genres.

## Rating Distribution

Ratings are concentrated mainly between approximately 4.0 and 4.8, with a peak around 4.4–4.5.

**Insight:** Most rated applications have relatively positive ratings.

## Reviews

Review counts are highly right-skewed. Most applications have relatively few reviews, while a small number have extremely large review volumes.

**Insight:** User engagement is highly concentrated among a small number of applications.

## Installs

Install values are strongly right-skewed, with a small number of applications in the highest install buckets.

**Insight:** Popularity is concentrated among a relatively small group of applications.

## Price

Most applications are free. Paid applications are concentrated around relatively low price points such as $0.99, $1.99, $2.99, and $4.99.

## Size

Application size is concentrated mostly in lower MB ranges with a long right tail.

## Bivariate & Multivariate Findings

### Rating vs Reviews

No strong linear relationship was observed.

### Rating vs Installs

Highly installed applications often have positive ratings, but highly rated applications can also have low install volumes.

### Type vs Rating

Free and paid applications generally show positive ratings, with a slightly higher central tendency for paid applications.

### Correlation

| Variables | Approx. Correlation |
|---|---:|
| Reviews vs Installs | 0.63 |
| Rating vs Reviews | 0.06 |
| Rating vs Installs | 0.04 |
| Size vs Reviews | 0.18 |
| Size vs Installs | 0.13 |

**Key insight:** Reviews and installs have the strongest relationship, while rating has very weak linear relationships with popularity metrics.

# 9. User Review Dataset Cleaning

### Initial Dataset

- 64,295 rows
- 5 columns

Approximately 41.8% of records had all review-related fields missing.

### Cleaning Performed

- Removed rows where all review information fields were missing.
- Retained rows where sentiment metrics existed even when review text was missing.
- Removed 7,735 exact duplicate occurrences.
- Retained repeated application names because multiple reviews for the same app are legitimate.
- Retained legitimate polarity outliers because strongly negative reviews are valid observations.

### Final Dataset

**29,697 rows × 5 columns**

Saved as:

`user_reviews_cleaned.csv`

# 10. User Review EDA

## Sentiment Distribution

Positive reviews are the largest group, followed by Negative and then Neutral reviews.

**Insight:** Overall user feedback is predominantly positive.

## Sentiment Polarity

Polarity is concentrated around neutral-to-positive values.

**Insight:** Numerical sentiment supports the overall positive sentiment finding.

## Subjectivity

Subjectivity spans the full 0–1 range, with substantial observations in moderate-to-high subjectivity levels.

**Insight:** Many reviews reflect personal opinions and experiences.

## Sentiment vs Polarity

Positive reviews have higher polarity, negative reviews lower polarity, and neutral reviews cluster around zero.

**Insight:** Sentiment labels align with the numerical polarity measure.

## Sentiment vs Subjectivity

Positive and negative reviews generally show moderate-to-high subjectivity, while neutral reviews have a broader distribution.

## Polarity vs Subjectivity

Correlation is approximately **0.27**, indicating a weak positive relationship.

# 11. Combined Analysis

## Review Aggregation

Review data was grouped by application to calculate:

- Positive review count
- Neutral review count
- Negative review count
- Total reviews
- Positive percentage
- Neutral percentage
- Negative percentage
- Average sentiment polarity
- Average sentiment subjectivity

## Dataset Integration

The aggregated review summary was merged with the cleaned app dataset using `App`.

A **left join** was used to preserve all app records.

### Results

- App dataset: 9,658 rows
- Review summary: 865 unique applications
- Matched applications: 816
- Applications without review matches: 8,842

Unmatched application names were retained rather than artificially matched.

## Category vs Sentiment

Positive reviews are the largest sentiment group across most major categories.

The Game category is a notable exception, showing comparatively stronger negative sentiment.

**Insight:** User sentiment varies by category.

## App Type vs Sentiment

Free applications generate substantially more review volume than paid applications.

**Insight:** Free applications have considerably greater review engagement in this dataset.

## Rating vs Sentiment Polarity

Higher-rated applications generally show more positive average sentiment polarity, while lower-rated applications tend to show more neutral-to-negative polarity.

**Insight:** Rating and sentiment are directionally aligned, but rating does not fully explain sentiment.

## Installs vs Sentiment Polarity

Higher-install applications generally show neutral-to-positive average polarity, while lower-install applications show wider variation.

**Insight:** Popularity is associated with broadly positive sentiment, but does not guarantee uniformly positive feedback.

# 12. Power BI Dashboard

The Power BI dashboard provides an interactive summary of the analysis.

### KPIs

- Total Apps
- Total Reviews
- Total Install Volume
- Average Rating

### Visuals

1. Top App Categories by Review Volume
2. Overall Sentiment Distribution
3. Sentiment Distribution by App Type
4. Average Sentiment Polarity by App Rating
5. App Type filter

# 13. Key Insights

1. **Free apps dominate:** Free applications represent the majority of the dataset.
2. **Positive sentiment dominates:** Positive reviews are the largest sentiment group.
3. **Engagement is concentrated:** A small number of applications account for a large share of reviews and installs.
4. **Reviews and installs are moderately related:** Their correlation is approximately 0.63.
5. **Rating is weakly related to popularity:** Rating has very weak linear relationships with reviews and installs.
6. **Rating and sentiment are directionally aligned:** Higher-rated apps generally have more positive average sentiment.
7. **Sentiment varies by category:** Most major categories are predominantly positive, while Games show comparatively stronger negative sentiment.
8. **Paid apps have lower review volume:** Paid apps receive substantially fewer reviews than free apps.

# 14. Business Recommendations

### 1. Prioritize User Experience
Maintain product quality and monitor feedback to protect positive sentiment and ratings.

### 2. Monitor Negative Reviews
Identify recurring complaints, bugs, usability issues, and missing features.

### 3. Focus on High-Engagement Applications
High-review and high-install applications provide valuable feedback signals from larger user bases.

### 4. Use Category-Specific Strategies
Analyze feedback within category context because user expectations differ across categories.

### 5. Maintain Competitive Pricing
Evaluate paid-app pricing against engagement and perceived value.

### 6. Use Reviews as Continuous Feedback
Monitor sentiment over time to identify changes following updates and feature releases.

# 15. Limitations

- Install values are bucketed and are not exact installation counts.
- The two datasets do not contain identical sets of applications.
- Missing ratings were not imputed.
- Sentiment analysis relies on the available sentiment labels and metrics.
- Correlation does not imply causation.
- Application names were used as the merge key, so differently represented names may remain unmatched.
- The dataset may not represent the current Google Play Store ecosystem.

# 16. Project Structure

```text
PlayStore-App-Review-Analysis/
│
├── data/
│   ├── unprocessed/
│   └── processed/
│
├── notebooks/
│   ├── Project_Overview.ipynb
│   ├── Google_PlayStore_App.ipynb
│   ├── Google_PlayStore_User_Analysis.ipynb
│   └── Combined_Analysis.ipynb
│
├── powerbi/
│   └── PlayStore_App_Review_Analysis_Dashboard.pbix
│
├── documentation/
│   └── Project_Documentation.md
│
├── README.md
└── requirements.txt
```

# 17. Conclusion

This project combines application-level and user-review-level data to provide a comprehensive analysis of the Google Play Store ecosystem.

The analysis shows that the dataset is dominated by free applications and positive user feedback. User engagement is highly concentrated, while reviews and installs show the strongest relationship among the major numerical variables.

The combined analysis also shows that higher-rated applications generally have more positive user sentiment, while sentiment varies across categories and app types.

By combining **Python-based data cleaning, exploratory analysis, review aggregation, dataset integration, and Power BI visualization**, this project demonstrates an end-to-end data analytics workflow from raw data to actionable business insights.
