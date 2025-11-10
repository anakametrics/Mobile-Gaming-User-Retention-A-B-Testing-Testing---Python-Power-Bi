 Mobile Gaming User Retention – A/B Testing (Cookie Cats)

📘 Introduction

Cookie Cats is a popular mobile puzzle game developed by Tactile Entertainment.
It’s a “connect-three” style puzzle where players link tiles of the same color to win levels — featuring adorable singing cats! 🐱🎵

As players progress, they encounter gates that either require waiting or making an in-app purchase.
These gates:
Encourage in-app purchases 💰
Provide natural breaks in playtime ⏱️
Potentially improve long-term enjoyment 🎮

Originally, the first gate appeared at level 30, but developers tested moving it to level 40.
This A/B test investigates how gate placement affects player retention and engagement.

📊 Objective

1. To analyze how changing the first gate from level 30 → level 40 impacts:
2. 1-Day and 7-Day Retention
3. Total Game Rounds Played
4. Overall Player Engagement

🧠 Dataset Overview
File: cookie_cats.csv
Rows: 90,189 players
| Column           | Description                                                 |
| ---------------- | ----------------------------------------------------------- |
| `userid`         | Unique player ID                                            |
| `version`        | A/B test group (`gate_30` = Control, `gate_40` = Treatment) |
| `sum_gamerounds` | Number of rounds played in first 14 days                    |
| `retention_1`    | Player returned 1 day after install (Boolean)               |
| `retention_7`    | Player returned 7 days after install (Boolean)              |

🧮 Methodology
1. Exploratory Data Analysis (EDA)
   Data inspection, summary statistics, and group comparisons
2. Key Metric Calculation
   Average game rounds per version
   Retention rate (Day-1, Day-7)
3. Bootstrapping
   Used to estimate the uncertainty and probability differences between groups
4. Visualization
   Created KPIs and charts to visualize differences in retention and engagement

📈 Dashboard Overview
📍 Title

Mobile Game Retention A/B Testing – Cookie Cats

💡 KPIs (Top Metrics)
| KPI                         | Description                         | Insights                       |
| --------------------------- | ----------------------------------- | ------------------------------ |
| **Total Players per Group** | Count of users in gate_30 / gate_40 | ~45k per group, balanced split |
| **Average Game Rounds**     | Mean rounds played                  | ~52 rounds avg.                |
| **Day-1 Retention %**       | % of players returning after 1 day  | Slightly higher in gate_30     |
| **Day-7 Retention %**       | % returning after 7 days            | Noticeably higher in gate_30   |

Visual Components
| Chart                                   | Type                | Fields                                                                  | Description                                                                         |
| --------------------------------------- | ------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **Probability Gate_30 > Gate_40**       | Donut Chart         | *Retention_Period* → Legend, *Probability (%)* → Values                 | Shows probability that gate_30 has higher retention (97% for Day-1, ~99% for Day-7) |
| **Day-1 & Day-7 Retention by Version**  | Clustered Bar Chart | *Version* → Axis X, *Retention Rate* → Axis Y                           | Compares average retention between A/B versions                                     |
| **Average Game Rounds by Version**      | Bar Chart           | *Version* → X, *Avg Game Rounds* → Y                                    | Shows that gate_30 players tend to play slightly more rounds                        |
| **Bootstrap % Difference in Retention** | Line or Bar Chart   | *Retention_Period* → X, *Bootstrap % Difference* → Y                    | Highlights the difference in retention probabilities between gate_30 and gate_40    |
| **Filters**                             | Slicer              | *Version* (`gate_30`, `gate_40`), *Retention_Period* (`Day-1`, `Day-7`) | Allows selecting and comparing subsets dynamically                                  |

🧩 Step-by-Step Dashboard Guide (Power BI)
1. Import Data
Load cookie_cats.csv into Power BI.

2. Data Preparation
Ensure correct data types:
userid → Whole number
version → Text
sum_gamerounds → Whole number
retention_1, retention_7 → Boolean

3. Create Calculated Measures
Total Players: COUNT(userid)
Avg Game Rounds: AVERAGE(sum_gamerounds)
Day-1 Retention %: AVERAGE(retention_1) * 100
Day-7 Retention %: AVERAGE(retention_7) * 100

4. Build Visuals
| Visual    | Fields                                             | Title                              |
| --------- | -------------------------------------------------- | ---------------------------------- |
| Card      | `COUNT(userid)`                                    | Total Players per Group            |
| Card      | `AVERAGE(sum_gamerounds)`                          | Average Game Rounds                |
| Card      | `AVERAGE(retention_1)*100`                         | Day-1 Retention %                  |
| Card      | `AVERAGE(retention_7)*100`                         | Day-7 Retention %                  |
| Donut     | Retention_Period, Probability                      | Probability Gate_30 > Gate_40      |
| Bar Chart | version (X), retention_1_rate/retention_7_rate (Y) | Day-1 & Day-7 Retention by Version |
| Bar Chart | version (X), avg_game_rounds (Y)                   | Average Game Rounds by Version     |
| Line/Bar  | retention_period (X), bootstrap_diff (Y)           | Bootstrap % Difference             |

🔍 Key Insights

1. Both groups had roughly equal player counts (~45k each).
2. 1-Day Retention: 44.8% (gate_30) vs 44.2% (gate_40)
3. 7-Day Retention: 19.0% (gate_30) vs 18.2% (gate_40)
Bootstrapping shows:
1. 97% probability that gate_30 has higher 1-day retention.
2. 99% probability that gate_30 has higher 7-day retention.
Conclusion: Moving the gate later (to level 40) reduces retention.
Earlier gating helps maintain engagement and long-term player retention.

🧾 Conclusion

This A/B test reveals that retention is better when the first gate remains at level 30.
The dashboard and analysis demonstrate a data-driven approach to decision-making in mobile game design — balancing engagement, monetization, and player satisfaction.

🛠️ Tools & Technologies

Python (Pandas, Matplotlib, NumPy, SciPy)
Power BI (Dashboard Visualization)
A/B Testing & Bootstrapping for Statistical Inference
