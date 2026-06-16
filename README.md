# 🎵 Spotify User Insights Dashboard

> End-to-end Spotify user analytics dashboard built with Excel and Power BI — analyzing churn, subscription conversion, engagement, and product insights across 50K users.

---

## 📌 Project Overview

This project analyzes a Spotify user dataset of 50,000 users to uncover patterns in user behavior, subscription conversion, churn, engagement, and product feature preferences. The analysis was performed in **Microsoft Excel** for initial exploration and **Power BI** for interactive dashboard creation.

The dashboard is designed to answer real business questions:
- Who is churning and why?
- How effectively are ads converting free users to premium?
- Which age groups and countries drive the most engagement?
- What features do users love and what do they want next?

---

## 🗂️ Dataset

| Property | Details |
|---|---|
| Total Records | 50,000 users |
| Source | Synthetic Spotify-style user dataset |
| Format | Excel (.xlsx) |

### Original Columns
`user_id`, `country`, `age`, `signup_date`, `subscription_type`, `subscription_status`, `months_inactive`, `inactive_3_months_flag`, `ad_interaction`, `ad_conversion_to_subscription`, `music_suggestion_rating_1_to_5`, `avg_listening_hours_per_week`, `favorite_genre`, `most_liked_feature`, `desired_future_feature`, `primary_device`, `playlists_created`, `avg_skips_per_day`

### Helper Columns Added in Excel
| Column | Description |
|---|---|
| `Age Group` | Bucketed age into Gen Z, Young Adults, Mid-Career, Mature Adults, Seniors |
| `Month` | Extracted month number from signup_date |
| `Year` | Extracted year from signup_date |
| `Listening Hour Category` | Binned avg_listening_hours_per_week into Low / Medium / High / Very High |
| `Playlist Creator Category` | Binned playlists_created into Casual / Active / Power User |

---

## 🛠️ Tools Used

- **Microsoft Excel** — Data exploration, pivot tables, helper column creation
- **Power BI Desktop** — Interactive dashboard, DAX measures, DAX columns
- **DAX (Data Analysis Expressions)** — Custom KPI measures

---

## 📐 DAX Measures

```dax
Total Users = COUNT('Table1'[user_id])
Inactive Users = CALCULATE(COUNT('Table1'[user_id]), 'Table1'[inactive_3_months_flag] = 1)
Churn Rate % = DIVIDE([Inactive Users], [Total Users], 0)
Retention Rate % = 1 - [Churn Rate %]
Ad Interaction Users = CALCULATE(COUNT('Table1'[user_id]), 'Table1'[ad_interaction] = "Yes")
Converted Users = CALCULATE(COUNT('Table1'[user_id]), 'Table1'[ad_conversion_to_subscription] = "Yes")
Ad Conversion Rate % = DIVIDE([Converted Users], [Total Users], 0)
Free Users = CALCULATE(COUNT('Table1'[user_id]), 'Table1'[subscription_type] = "Free")
Premium Users = CALCULATE(COUNT('Table1'[user_id]), 'Table1'[subscription_type] <> "Free")
Premium Adoption Rate % = DIVIDE([Premium Users], [Total Users], 0)
Total Playlists Created = SUM('Table1'[playlists_created])
```

---

## 📊 Dashboard Pages

### Page 1 — Spotify User Growth & Executive Overview
High-level summary of platform performance with KPIs, signup trend, subscription mix, and country distribution.

**Key Charts:** User Signup Trend (Line) · Subscription Plan Distribution (Donut) · Active vs Inactive by Subscription Type (Stacked Column) · Avg Listening Hours by Age Group (Column) · Top Countries by User Count (Bar)

---

### Page 2 — Customer Churn & Retention Analysis
Deep dive into inactivity patterns across age groups, subscription types, countries, and genres.

**Key Charts:** Churn Rate by Age Group (Bar) · Churn Rate by Subscription Type (Column) · Churn Rate by Country (Bar) · Inactive Users by Months Inactive (Column) · Active vs Inactive by Age Group (100% Stacked Bar) · Inactive Users by Genre (Treemap)

---

### Page 3 — Subscription & Conversion Analysis
Examines premium adoption rates, ad conversion performance, and the subscription conversion funnel.

**Key Charts:** Subscription Plan Distribution (Donut) · Premium Adoption by Age Group (Column) · Users by Subscription Type (100% Stacked Column) · Ad Conversion Rate by Age Group (Bar) · Premium Adoption by Country (Bar) · Subscription Conversion Funnel

---

### Page 4 — User Engagement & Listening Behavior
Explores listening habits, skip behavior, playlist creation patterns, and recommendation ratings.

**Key Charts:** Avg Listening Hours by Age Group (Column) · Avg Listening Hours by Subscription Type (Bar) · Avg Daily Skips by Genre (Column) · Playlist Creator Category Distribution (Column) · Listening Hours vs Playlist Creation (Scatter) · Avg Recommendation Rating by Genre (Bar)

---

### Page 5 — Product Features & Recommendation
Uncovers genre preferences, most loved features, desired future features, and recommendation satisfaction.

**Key Charts:** Top Favorite Music Genres (Bar) · Avg Recommendation Rating by Genre (Column) · Most Used Spotify Features (Donut) · Desired Future Features (Treemap) · Feature Preference by Subscription Type (Stacked Bar) · Recommendation Rating by Age Group (100% Stacked Column)

---

## 🔍 Key Insights

- **22.25% of users** were inactive for 3+ months, with Mid-Career users showing the highest inactivity rate
- **55% premium adoption rate** — Mature Adults lead slightly at 55.23%
- **Ad conversion is 8.7% platform-wide**, but jumps to ~25% among users who actually interacted with an ad — indicating ad engagement quality matters more than volume
- **Listening hours and skip rates are nearly uniform** across all subscription types (~10 hrs/week, ~10 skips/day), suggesting these behaviors aren't tied to plan tier
- **Mood-based Auto Playlists** is the most desired future feature (8.42K users), followed by Concert Alerts and Social Listening
- **K-Pop and Indie fans** rate music recommendations highest (3.67/5), while Latin fans rate them lowest (3.63/5)
- **Classical** is the most popular genre overall, with nearly even distribution across all 12 genres

---

## 📁 Repository Structure

```
spotify-user-insights-powerbi/
│
├── data/
│   └── spotify_user_behavior_realistic_50000_rows        # Original dataset
│
├── excel/
│   └── spotify_dataset        # Clean dataset with pivot tables wiith helper columns
│
├── dashboard/
│   └── Spotify_Analysis.pbix       # Power BI dashboard file
│   └── Spotify_Analysis.pdf        # Exported PDF of all 5 dashboard pages
│
└── README.md
```

---

## 🚀 How to Use

1. Clone this repository
2. Open `data/spotify_dataset.xlsx` to explore the raw data and pivot tables
3. Open `dashboard/Spotify_Analysis.pbix` in **Power BI Desktop**
4. Use the slicers (Country, Age Group, Subscription Type, Favorite Genre, Year) to filter the dashboard interactively
5. Navigate between pages using the sidebar buttons

---

## 👤 Author

**Your Name**
[LinkedIn](www.linkedin.com/in/akhil-t-v) · [GitHub](https://github.com/AKHIL572)) · [Portfolio](https://akhil-tv-portfolio.vercel.app/)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
