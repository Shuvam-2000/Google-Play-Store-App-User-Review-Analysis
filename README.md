# Google Play Store App & User Review Analysis

An end-to-end **Data Analytics & Business Intelligence project** analyzing Google Play Store applications and user reviews to understand app popularity, user engagement, ratings, and user sentiment.

The project combines **Python-based data cleaning and EDA**, **review-level sentiment analysis**, **dataset integration**, and an **interactive Power BI dashboard**.

---

## 📊 Dashboard Preview

![Google Play Store App & User Review Analysis Dashboard](https://drive.google.com/file/d/1xX-dQWbUp7DoRVeTcXn-DTkocslJHsIH/view?usp=drive_link)

The dashboard provides an interactive summary of app performance, review volume, ratings, install volume, and user sentiment.

---

## 🎯 Project Objectives

- Analyze the distribution and characteristics of Google Play Store applications.
- Understand app popularity using reviews and install-volume indicators.
- Analyze user sentiment using sentiment labels, polarity, and subjectivity.
- Compare sentiment across app categories and app types.
- Investigate relationships between app ratings, reviews, installs, and sentiment.
- Combine app-level and user-review-level information.
- Build an interactive Power BI dashboard.
- Extract actionable business insights and recommendations.

---

## 🗂️ Datasets

### Google Play Store Apps Dataset

The app-level dataset contains information about:

- App
- Category
- Rating
- Reviews
- Size
- Installs
- Type
- Price
- Content Rating
- Genres
- Last Updated
- Current Version
- Android Version

### Google Play Store User Reviews Dataset

The review-level dataset contains:

- App
- Translated Review
- Sentiment
- Sentiment Polarity
- Sentiment Subjectivity

---

## 🔄 Project Workflow

```text
Raw Data
   │
   ▼
Data Cleaning & Preprocessing
   │
   ├───────────────┐
   ▼               ▼
App-Level EDA   Review-Level EDA
   │               │
   └───────┬───────┘
           ▼
    Review Aggregation
           │
           ▼
   Dataset Integration
           │
           ▼
    Combined Analysis
           │
           ▼
    Power BI Dashboard
           │
           ▼
 Insights & Recommendations
```

---

## 🧹 Data Cleaning & Preprocessing

### App Dataset

**Initial:** 10,841 rows × 13 columns

Key preprocessing steps:

- Investigated missing values.
- Removed the corrupted `Life Made WI-Fi Touchscreen Photo Frame` record.
- Removed the unusable record with missing `Type`.
- Converted `Reviews` to integer.
- Cleaned `Installs` and converted it to numeric install-volume values.
- Converted `Price` to numeric.
- Converted `Size` to MB.
- Converted `Last Updated` to datetime.
- Removed **483 exact duplicate rows**.
- Investigated outliers and retained legitimate extreme observations.
- Retained duplicate app names where they represented valid observations.
- Did not artificially impute missing ratings.

**Final:** 9,658 rows × 13 columns

### User Review Dataset

**Initial:** 64,295 rows × 5 columns

Key preprocessing steps:

- Removed rows where all review-related information was missing.
- Retained rows containing useful sentiment metrics even when review text was unavailable.
- Removed **7,735 exact duplicate occurrences**.
- Retained repeated app names because multiple reviews for an application are valid observations.
- Retained legitimate sentiment polarity outliers.

**Final:** 29,697 rows × 5 columns

---

## 🔍 Exploratory Data Analysis

### App-Level EDA

The analysis covers:

- Category distribution
- Free vs paid applications
- Content rating
- Genre distribution
- Rating distribution
- Review distribution
- Install-volume distribution
- Price distribution
- Application size
- Rating vs reviews
- Rating vs installs
- Type vs rating
- Numerical correlation analysis

### User Review EDA

The analysis covers:

- Sentiment distribution
- Sentiment polarity
- Sentiment subjectivity
- Sentiment vs polarity
- Sentiment vs subjectivity
- Polarity vs subjectivity
- Correlation analysis

### Combined Analysis

Review-level information was aggregated at application level to calculate:

- Positive review count
- Neutral review count
- Negative review count
- Total reviews
- Sentiment percentages
- Average sentiment polarity
- Average sentiment subjectivity

The combined dataset was then used to analyze:

- Category vs sentiment
- App type vs sentiment
- Rating vs sentiment polarity
- Installs vs sentiment polarity

---

## 📈 Key Findings

### 1. Free Applications Dominate

Free applications make up the vast majority of the analyzed app dataset.

### 2. Positive Sentiment Dominates

Positive reviews are the largest sentiment group, followed by negative and neutral reviews.

### 3. Engagement Is Highly Concentrated

Most applications have relatively low review volumes, while a small number of applications account for a large share of reviews and install volume.

### 4. Reviews and Installs Have the Strongest Relationship

The correlation between reviews and installs is approximately **0.63**, indicating a moderate positive relationship.

### 5. Rating Has a Weak Relationship with Popularity

Rating has very weak linear relationships with both reviews and installs.

### 6. Rating and Sentiment Are Directionally Aligned

Higher-rated applications generally show more positive average sentiment polarity, while lower-rated applications tend to show more neutral-to-negative sentiment.

### 7. Sentiment Varies Across Categories

Positive sentiment dominates most major categories, while the Game category shows comparatively stronger negative sentiment.

### 8. Paid Applications Have Lower Review Volume

Free applications generate substantially more review volume than paid applications in the analyzed data.

---

## 💡 Business Recommendations

- **Prioritize user experience:** Monitor user feedback to identify opportunities for product improvement.
- **Monitor negative reviews:** Identify recurring bugs, complaints, usability issues, and missing features.
- **Focus on high-engagement applications:** High-review and high-install applications provide valuable feedback signals.
- **Use category-specific strategies:** User expectations can differ significantly across app categories.
- **Evaluate pricing carefully:** Paid applications should provide sufficient perceived value relative to their price.
- **Use reviews as continuous feedback:** Sentiment analysis can help monitor changes in user perception after product updates.

---

## 📊 Power BI Dashboard

The Power BI dashboard contains:

### KPIs

- **Total Apps:** 10K
- **Total Reviews:** 28K
- **Total Install Volume:** 75bn
- **Average Rating:** 4.17

### Visualizations

- **Top App Categories by Review Volume**
- **Overall Sentiment Distribution**
- **Sentiment Distribution by App Type**
- **Average Sentiment Polarity by App Rating**
- **App Type Filter**

The dashboard is designed to provide a concise view of application performance, popularity, and user sentiment.

---

## ⚠️ Data Limitation

The original `Installs` field contains **bucketed values** such as `1,000+`, `10,000+`, and `1,000,000+`.

Therefore, the cleaned numeric install values represent **install-volume buckets rather than exact installation counts**.

As a result, the dashboard's **Total Install Volume** should be interpreted as an aggregated indicator based on the available install buckets, rather than an exact number of installations.

---

## 🧰 Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Data cleaning and exploratory analysis |
| **Pandas** | Data manipulation |
| **NumPy** | Numerical operations |
| **Matplotlib** | Data visualization |
| **Seaborn** | Statistical visualization |
| **Jupyter Notebook** | Analysis environment |
| **Power BI** | Interactive dashboard |
| **PostgreSQL / SQL** | Analytical querying |
| **Git & GitHub** | Version control |

---

## 📁 Repository Structure

```text
PlayStore-App-Review-Analysis/
│
├── assets/
│   └── dashboard_overview.png
│
├── data/
│   ├── ...
│   └── ...
│
├── Documentation/
│   └── Project_Documentation.md
│
├── notebooks/
│   ├── Google_PlayStore_App.ipynb
│   ├── Google_PlayStore_User_Analysis.ipynb
│   ├── Combined_Analysis.ipynb
│   └── Project_Overview.ipynb
│
├── power bi/
│   └── PlayStore_App_Review_Dashboard.pbix
│
├── .gitignore
├── README.md
├── requirements.txt
└── ...
```

> The `venv/` environment is used locally for development and is excluded from the repository through `.gitignore`.

---

## 📚 Detailed Documentation

For the complete methodology, preprocessing decisions, EDA findings, combined analysis, limitations, and business recommendations, see:

**[Project Documentation](Documentation/Project_Documentation.md)**

---

## 🚀 How to Explore the Project

1. Clone the repository.
2. Review the datasets in the `data/` directory.
3. Open the notebooks in the `notebooks/` directory.
4. Run the notebooks to reproduce the analysis.
5. Open the Power BI `.pbix` file from the `power bi/` directory using Power BI Desktop.
6. Refer to the documentation for the detailed methodology and findings.

---

## 📝 Conclusion

This project demonstrates an end-to-end data analytics workflow by combining **data cleaning, exploratory data analysis, sentiment analysis, dataset integration, and business intelligence visualization**.

By analyzing both application-level metrics and user reviews, the project provides a broader understanding of:

- App popularity
- User engagement
- Application ratings
- User sentiment
- Category-level differences
- Free vs paid application behavior

The final outcome transforms raw Play Store data into **structured analysis, interactive visual insights, and actionable business recommendations**.

---

## 👤 Author

**Shuvam Saha**

**Data Analytics | Python | SQL | Power BI | Exploratory Data Analysis**
