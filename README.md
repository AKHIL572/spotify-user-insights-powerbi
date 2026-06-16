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
High-level summary of overall platform performance — user growth, subscription mix, engagement, and geographic distribution.

**Business Questions Answered:**
- How has the user base grown over the years?
- What is the current subscription plan breakdown?
- How many users are active vs inactive across subscription types?
- Which age groups listen the most on average?
- Which countries have the highest user count?

**KPIs:** Total Users · Active Users · Churn Rate % · Avg Weekly Listening Hours · Ad Conversion Rate %

**Charts:**
1. User Signup Trend Over Time — Line Chart (Year/Month)
2. Subscription Plan Distribution — Donut Chart
3. Active vs Inactive Users by Subscription Type — Stacked Column Chart
4. Average Listening Hours by Age Group — Clustered Column Chart
5. Top Countries by User Count — Clustered Bar Chart

---

### Page 2 — Customer Churn & Retention Analysis
Deep dive into inactivity patterns across age groups, subscription types, countries, and genres.

**Business Questions Answered:**
- Which age group churns the most?
- Which age group is the most active?
- Which countries have the highest inactivity rates?
- Which genres are associated with higher churn?
- How long do users stay inactive before churning?
- What is the Active vs Inactive split across age groups?

**KPIs:** Total Users · Inactive Users · Churn Rate % · Avg Months Inactive · Retention Rate %

**Charts:**
1. Churn Rate by Age Group — Clustered Bar Chart
2. Churn Rate by Subscription Type — Clustered Column Chart
3. Churn Rate by Country — Clustered Bar Chart (Top 8)
4. Inactive Users by Months Inactive — Clustered Column Chart
5. Active vs Inactive Users by Age Group — 100% Stacked Bar Chart
6. Inactive Users by Favorite Genre — Treemap

---

### Page 3 — Subscription & Conversion Analysis
Examines premium adoption rates, ad conversion performance, and the full subscription conversion funnel.

**Business Questions Answered:**
- Do users who interact with ads convert more to premium?
- Which age groups convert best from free to premium?
- Which device type drives the most subscriptions?
- Which countries have the highest premium adoption rate?
- What does the full conversion funnel look like from total users to paid subscribers?

**KPIs:** Total Subscribers · Premium Users · Free Users · Premium Adoption Rate % · Ad Conversion Rate %

**Charts:**
1. Subscription Plan Distribution — Donut Chart
2. Premium Adoption by Age Group — Clustered Column Chart
3. Users by Subscription Type (Active vs Inactive) — 100% Stacked Column Chart
4. Ad Conversion Rate by Age Group — Clustered Bar Chart
5. Premium Adoption Rate by Country — Clustered Bar Chart (Top 8)
6. Subscription Conversion Funnel — Funnel Chart (Total Users → Ad Interaction Users → Converted Users)

---

### Page 4 — User Engagement & Listening Behavior
Explores listening habits, skip behavior, playlist creation patterns, and music recommendation satisfaction.

**Business Questions Answered:**
- Which genre users listen the most on average?
- Do playlist creators spend more time listening?
- Which age groups skip music the most?
- How does listening behavior differ across subscription types?
- Is there a relationship between listening hours and playlist creation?
- Which genres receive the best recommendation ratings?

**KPIs:** Avg Weekly Listening Hours · Avg Daily Skips · Total Playlists Created · Avg Playlists Per User · Avg Recommendation Rating

**Charts:**
1. Average Listening Hours by Age Group — Clustered Column Chart
2. Average Listening Hours by Subscription Type — Clustered Bar Chart
3. Average Daily Skips by Favorite Genre — Clustered Column Chart
4. Playlist Creator Category Distribution — Clustered Column Chart
5. Listening Hours vs Playlist Creation — Scatter Chart (by Subscription Type)
6. Average Recommendation Rating by Genre — Clustered Bar Chart (Top 8)

---

### Page 5 — Product Features & Recommendation
Uncovers genre preferences, most loved current features, desired future features, and recommendation satisfaction by segment.

**Business Questions Answered:**
- What do users currently love most about Spotify?
- What should Spotify build or prioritize next?
- Which genre users are happiest with music recommendations?
- Are premium users more satisfied with recommendations than free users?
- How does feature preference vary across subscription types?
- How are recommendation ratings distributed across age groups?

**KPIs:** Avg Recommendation Rating · Total Genres · Most Popular Genre · Total Feature Requests · Total Feature Preferences

**Charts:**
1. Top Favorite Music Genres — Clustered Bar Chart (Top 8)
2. Average Recommendation Rating by Genre — Clustered Column Chart
3. Most Used Spotify Features — Donut Chart
4. Desired Future Features — Treemap
5. Feature Preference by Subscription Type — Stacked Bar Chart
6. Recommendation Rating by Age Group and Genre — 100% Stacked Column Chart

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
