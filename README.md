# User Profiling and Segmentation for E-commerce Marketing

Using clustering techniques and behavioral analytics, this project identifies key customer personas to power personalized marketing strategies and improve campaign ROI for an e-commerce brand.

## Table of Contents
- [Project Story](#project-story)
- [Dataset Overview](#dataset-overview)
- [Why Segment Users?](#why-segment-users)
- [How We Discovered the 5 Personas](#how-we-discovered-the-5-personas)
- [Meet the Personas (Visual Cards)](#meet-the-personas-visual-cards)
- [Campaign Strategy & ROI](#campaign-strategy--roi)
- [Recommendations for Marketers](#recommendations-for-marketers)
- [Tools & Techniques](#tools--techniques)
- [Future Ideas](#future-ideas)
- [Python Script Summary](#python-script-summary)


## Project Story

An e-commerce brand wants to improve how it targets customers with online marketing. The company has data from over 1,000 users, including their age, income, online activity, and how they interact with ads.

By using clustering techniques, five unique customer groups (personas) are discovered. Each group has different habits and preferences. These insights help the brand decide when to run ads, what messages to show, and how to reach each group more effectively.


## Dataset Overview

- **Demographics**: Age, Gender, Income Level, Education
- **Behavioral Metrics**: Time Online (Weekday/Weekend), Likes, Reactions, Device Usage
- **Ad Engagement**: Click-Through Rate (CTR), Conversion Rate, Ad Interaction Time
- **Top Interests**: Multi-label user interests


## Why Segment Users?

Without segmentation, marketing is a guessing game. With it, we can:

✅ Deliver campaigns to users when they're most active  
✅ Personalize based on interests and intent  
✅ Allocate ad budget toward high-conversion clusters


## How We Discovered the 5 Personas

- Standardized behavioral metrics using `StandardScaler`
- Encoded demographics with `OneHotEncoder`
- Applied KMeans clustering (k=5) using a full pipeline
- Visualized insights via radar charts and KPI comparisons

![Radar Chart](images/radar_chart.png)


## Meet the Personas (Visual Cards)

| Persona | Description | Device | Behavior | Strategy |
|---------|-------------|--------|----------|----------|
| **Weekend Warriors** | Mid-income professionals active only on weekends | Mobile | Weekend browsing spikes | Flash sales, SMS push |
| **Engaged Professionals** | High-income consistent buyers, high CTR | Mobile + Tablet | Loyal and high-value | VIP programs, bundles |
| **Low-Key Users** | Passive scrollers, low ad interaction | Mobile | Quiet browsers | Retarget gently, lifestyle content |
| **Active Explorers** | High browsing but low buying | Desktop + Mobile | Window shoppers | Curated picks, urgency copy |
| **Budget Browsers** | Price-conscious, short attention span | Mobile | Low CTR and short sessions | “Under $10” promos |


## Campaign Strategy & ROI

| Segment | CTR Lift | Conversion Lift | Projected Uplift | Suggested Tactic |
|---------|----------|------------------|------------------|------------------|
| Engaged Professionals | +5% | +10% | $101,325 | Premium perks, loyalty push |
| Weekend Warriors | +5% | +10% | $60,975 | Weekend SMS blitz |
| Budget Browsers | — | — | $9,000 | Price-first ad targeting |

Even small performance increases in high-value segments can drive over **$11K in extra revenue** per campaign cycle.


## Recommendations for Marketers

- Focus spend on segments with high CTR + conversion rates
- Schedule campaigns around **time-based behaviors** (e.g., weekends)
- Personalize creatives using **interest and device preferences**
- Use personas to craft onboarding flows, retargeting, and loyalty content


## Tools & Techniques

- **Languages**: Python  
- **Libraries**: Pandas, Seaborn, Scikit-learn, Plotly  
- **Skills Applied**: EDA, Clustering, Pipelines, Feature Engineering, Persona Design
  

## Future Ideas

- Add silhouette score and elbow method for validating cluster count
- Deploy interactive dashboard (Tableau or Streamlit)
- Simulate A/B test outcomes for persona-based campaigns


## Python Script Summary

```python
# Load data
import pandas as pd
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.cluster import KMeans
import plotly.graph_objects as go

data = pd.read_csv('user_profiles_for_ads.csv')

# Feature selection
features = ['Age', 'Gender', 'Income Level', 'Time Spent Online (hrs/weekday)',
            'Time Spent Online (hrs/weekend)', 'Likes and Reactions']
X = data[features]

# Preprocessing
numeric_features = ['Time Spent Online (hrs/weekday)', 'Time Spent Online (hrs/weekend)', 'Likes and Reactions']
categorical_features = ['Age', 'Gender', 'Income Level']

preprocessor = ColumnTransformer([
    ('num', StandardScaler(), numeric_features),
    ('cat', OneHotEncoder(), categorical_features)
])

# Clustering pipeline
pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('cluster', KMeans(n_clusters=5, random_state=42))
])
