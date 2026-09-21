# 🍽️ Plate to Platform: The Battle of Giants — Swiggy vs Zomato

> **An interactive Tableau BI case study comparing Swiggy and Zomato across consumer tiers, financial performance, customer experience, sentiment, behaviour, geography, restaurant types, cuisines and operational metrics.**

**Tableau Public:**  
https://public.tableau.com/app/profile/somnath.roy7901/viz/PlatetoPlatform_TheBattleofGiants_SwiggyvsZomatoAnalysisReport/SwiggyvsZomatoComparisosnAnalyticsStoryboard?publish=yes

---

## 📌 Project Overview

**Plate to Platform — The Battle of Giants** is a Tableau-based Business Intelligence and analytical storytelling project designed to move beyond a simple Swiggy-vs-Zomato comparison.

The analysis decomposes platform performance by **consumer spending behaviour**, using four custom consumer tiers:

| Consumer Tier | Avg Cost Per Order |
|---|---:|
| Budget Friendly | ₹0 – < ₹300 |
| Moderate | ₹300 – < ₹700 |
| Premium | ₹700 – < ₹1,300 |
| Elite | ₹1,300 – ₹3,500 |

The project combines financial, operational, customer-experience and behavioural indicators into an interactive analytical framework.

### Core analytical dimensions

- Revenue
- Net profit
- Net profit margin
- Estimated monthly orders
- Market share
- Platform commission
- Commission amount
- Delivery fee
- Delivery time
- Discount frequency
- Estimated expense
- Ratings
- Reviews
- Customer sentiment
- Consumer experience
- Restaurant type
- Cuisine
- Top-selling dishes
- Repeat-customer behaviour
- Geography / city-level behaviour
- Year-over-year / time-based trends

---

# 🎯 Business Questions

The project attempts to answer questions such as:

1. Which platform performs differently across consumer spending tiers?
2. Which consumer tier contributes the greatest revenue concentration?
3. How do revenue and profit patterns change across Budget, Moderate, Premium and Elite customers?
4. Does higher customer sentiment correspond with higher ratings and stronger platform performance?
5. How do delivery fee, delivery time, commission and estimated expense relate to platform economics?
6. Which platform demonstrates stronger performance by restaurant type?
7. Which cuisines and dishes are associated with stronger customer response?
8. How do reviews, ratings, repeat orders and sentiment interact?
9. Are platform advantages consistent across cities?
10. Where do financial performance and customer-experience indicators disagree?
11. Can a single comparison framework dynamically evaluate multiple KPIs without creating separate dashboards for every metric?

---

# 🧠 BI Approach

This project follows a **decision-oriented BI workflow** rather than a collection of disconnected charts:

**Raw / cleaned data → segmentation → calculated metrics → normalization → KPI comparison → interactive dashboards → analytical storyboard → business interpretation**

The design intentionally combines:

- Descriptive analytics
- Comparative analytics
- Diagnostic analysis
- Segmentation
- KPI engineering
- Parameter-driven analysis
- Customer-experience scoring
- Financial-performance analysis
- Geospatial analysis
- Behavioural analysis
- Analytical storytelling

---

# 🏗️ Tableau Architecture

The workbook contains:

- **26 analytical worksheets**
- **5 primary dashboards/storytelling stages**
- Parameter-driven metric selection
- Consumer-tier parameterization
- Platform-selection parameterization
- Calculated fields for derived financial and behavioural metrics
- Interactive filtering and dashboard actions
- Custom indices using **Min-Max normalization**
- A composite **Consumer Experience Score**
- Dynamic platform-comparison logic

### Main dashboards

1. **Platform Demographics Dashboard**
2. **Platform Performance Per Consumer Tier Dashboard**
3. **Sentiment vs Behaviour Analysis Per Consumer Tier Dashboard**
4. **Consumer Experience Analysis Dashboard**
5. **Swiggy vs Zomato Financial Analysis Dashboard**
6. **Swiggy vs Zomato Comparison Analytics Storyboard**

---

# 🎛️ Parameters

The workbook uses three major parameters to make the analysis dynamic.

## 1. Consumer Tier

Controls the analytical population:

- All
- Budget Friendly Customers
- Moderate Customers
- Premium Customers
- Elite Customers

The parameter feeds calculated filters so the same dashboards can be reused across consumer segments.

## 2. Platform Selection

Controls whether the analysis focuses on:

- `SWIGGY`
- `ZOMATO`
- `ALL`

This avoids duplicating dashboards for each platform.

## 3. Selected Metric

Controls the KPI being evaluated in the comparison logic.

The framework includes:

- Selected Platform Revenue
- Selected Platform Net Profit
- Selected Platform Rating
- Consumer Rating Index
- Consumer Experience Score
- Selected Platform Orders
- Selected Platform Reviews
- Selected Platform Market Share
- Selected Platform Commission Amount
- Selected Platform Delivery Fee
- Selected Platform Delivery Time
- Selected Platform Discount Frequency
- Selected Platform Expense Amount
- Selected Platform Net Profit Margin

This creates a reusable **metric-switching BI framework**.

---

# 🧮 Key Calculated Fields

## Consumer Segmentation

### Budget Friendly Customers

```tableau
IF [Avg Cost Per Order] >= 0
AND [Avg Cost Per Order] < 300
THEN TRUE
ELSE FALSE
END
```

### Moderate Customers

```tableau
IF [Avg Cost Per Order] >= 300
AND [Avg Cost Per Order] < 700
THEN TRUE
ELSE FALSE
END
```

### Premium Customers

```tableau
IF [Avg Cost Per Order] >= 700
AND [Avg Cost Per Order] < 1300
THEN TRUE
ELSE FALSE
END
```

### Elite Customers

```tableau
IF [Avg Cost Per Order] >= 1300
AND [Avg Cost Per Order] <= 3500
THEN TRUE
ELSE FALSE
END
```

---

# 📐 Custom Consumer Experience Index

One of the key analytical features is a custom **Consumer Experience Score**.

The workbook first normalizes sentiment and rating measures using **Min-Max normalization**.

## Consumer Sentiment Index

```text
If value is NULL → NULL

If MAX = MIN → 5

Otherwise:

((Value - MIN) / (MAX - MIN)) × 10
```

## Consumer Rating Index

The same Min-Max normalization approach is applied to rating.

```text
If value is NULL → NULL

If MAX = MIN → 5

Otherwise:

((Value - MIN) / (MAX - MIN)) × 10
```

## Consumer Experience Score

The final score is the arithmetic mean of the two normalized components:

```text
Consumer Experience Score
=
(Consumer Sentiment Index + Consumer Rating Index) / 2
```

### Why this matters

Ratings and sentiment are measured on different scales and may not behave identically.

Normalization creates a common analytical scale, allowing the project to combine them into a composite experience indicator without treating the raw measures as directly interchangeable.

---

# 🔢 Standardization / Normalization Layer

The project uses a **custom Min-Max normalization framework** for comparative scoring.

### Min-Max formula

```text
Normalized Value =
(Value - Minimum)
-------------------
(Maximum - Minimum)
```

The normalized value is then scaled to a 0–10 interpretation in the Consumer Sentiment and Consumer Rating indices.

### Constant-value handling

If:

```text
Maximum = Minimum
```

the workbook assigns a neutral midpoint value of:

```text
5
```

This prevents division-by-zero and avoids artificially creating an extreme score when there is no variation.

---

# 💰 Financial & Platform Calculations

## Selected Platform Revenue

The parameter dynamically switches between platform revenue.

```text
SWIGGY → Swiggy Estimated Monthly Revenue
ZOMATO → Zomato Estimated Monthly Revenue
ALL    → Swiggy Revenue + Zomato Revenue
```

## Selected Platform Orders

```text
SWIGGY → Swiggy Estimated Monthly Orders
ZOMATO → Zomato Estimated Monthly Orders
ALL    → Swiggy Orders + Zomato Orders
```

## Selected Platform Net Profit

```text
SWIGGY → Swiggy Estimated Net Profit
ZOMATO → Zomato Estimated Net Profit
ALL    → Swiggy Profit + Zomato Profit
```

## Selected Platform Delivery Time

For `ALL`, the workbook uses the average of the two platform delivery times.

```text
(Swiggy Delivery Time + Zomato Delivery Time) / 2
```

## Selected Platform Delivery Fee

```text
(Swiggy Delivery Fee + Zomato Delivery Fee) / 2
```

when both platforms are selected.

## Selected Platform Reviews

The workbook switches between platform review measures and combines them when `ALL` is selected.

## Selected Platform Commission %

```text
(Swiggy Commission % + Zomato Commission %) / 2
```

for the combined view.

## Selected Platform Total Expense

Expense is derived as:

```text
Estimated Revenue - Estimated Net Profit
```

For the combined view, platform expenses are added together.

## Delivery Fee %

The workbook calculates delivery fee relative to average cost per order:

```text
Delivery Fee % =
Delivery Fee / Avg Cost Per Order × 100
```

## Expense %

```text
Expense % =
(Revenue - Net Profit) / Revenue × 100
```

## Commission Amount

For individual platform selection:

```text
Commission Amount =
Commission % / 100 × Avg Cost Per Order
```

The `ALL` calculation uses a weighted-style aggregation based on platform commission and revenue/order measures.

## Expense Amount

The workbook derives a cost amount using:

```text
Avg Cost Per Order × Expense %
```

## Net Profit Margin

The workbook provides a dynamic profitability metric. For the combined platform view:

```text
Net Profit Margin =
Total Net Profit / Total Revenue × 100
```

---

# ⚖️ Dynamic Platform Comparison Logic

A major BI feature is the dynamic comparison engine.

The workbook does not simply compare Swiggy and Zomato once.

Instead, the `Selected Metric` parameter determines **what is being compared**.

For example:

### Higher is better

- Revenue
- Net Profit
- Rating
- Orders
- Reviews
- Market Share
- Commission amount
- Net Profit Margin

### Lower is better

- Delivery Fee
- Delivery Time
- Discount Frequency
- Expense Amount

This creates a reusable metric-specific comparison framework rather than hard-coding a single winner.

---

# 📊 Dashboard 1 — Platform Demographics

### Worksheets included

- Platform Ratings by Restaurant
- Platform Revenue Trend
- Cuisines vs Delivery Time & Ratings per Platform
- Platform Geospatial Order Analysis
- Price Segment per Consumer Tier

### Analytical purpose

This dashboard establishes the market and customer context before moving into detailed financial analysis.

It examines:

- Revenue trends
- Restaurant ratings
- Price segmentation
- Cuisine-level delivery and rating behaviour
- Geographic order distribution
- Consumer-tier concentration

### Storyboard Insight — Full Interpretation

The central finding is that the **Moderate consumer segment is the dominant middle-market segment** and represents approximately half of the total revenue contribution in the storyboard analysis.

The Moderate tier therefore becomes an important analytical bridge between value-oriented Budget customers and high-spending Premium/Elite customers.

The storyboard identifies **Zomato as stronger on revenue within the Moderate consumer tier**.

The dashboard also establishes that platform performance is not uniform across consumer segments. Looking only at an overall platform total would therefore hide important segment-level differences.

The demographic dashboard additionally connects:

**consumer spending → revenue → geography → cuisine → delivery experience → ratings**

This provides the foundation for the later profitability and experience analysis.

---

# 📈 Dashboard 2 — Platform Performance Per Consumer Tier

### Worksheets included

- Platform Profit Trend Per Consumer Tier
- Platform Ratings Per Consumer Tier
- Platform Discounts Per Consumer Tier
- Platform Market Share vs Order Per Consumer Tier
- Platform Commission / Order Per Consumer Tier

### Analytical purpose

This dashboard investigates how platform economics change as consumer spending increases.

### Full Storyboard Insight

The profitability pattern is segmented rather than universal:

- **Zomato performs better in Budget Friendly and Moderate tiers in terms of profit.**
- **Swiggy performs better in Premium and Elite tiers in terms of profit.**

This is important because it demonstrates that a platform's financial strength can depend heavily on **who the customer is**, not simply on the platform's aggregate performance.

The dashboard further examines:

- Market share versus orders
- Commission behaviour
- Discount frequency
- Ratings
- Profit trends

The combination helps separate **scale indicators** from **profitability indicators**.

For example, high order volume does not automatically imply superior profit performance, because commission, discounting and estimated expenses influence the economic outcome.

The consumer-tier approach therefore exposes a more granular platform-performance structure than a single overall revenue comparison.

---

# ❤️ Dashboard 3 — Sentiment vs Behaviour Analysis Per Consumer Tier

### Worksheets included

- Top Selling Dish vs Review / Order Per Consumer Tier
- Sentiment Score vs Ratings Per Consumer Tier
- City Based Sentiment / Monthly Order Growth Per Consumer Tier
- Restaurant Type Revenue Distribution by Sentiment / Ratings
- Top Selling Dish / Cuisines vs Repeat Orders Per Consumer Tier

### Analytical purpose

This dashboard investigates whether customer perception and behaviour move together.

It connects:

**sentiment → ratings → reviews → orders → repeat behaviour → revenue**

### Full Storyboard Insight

The sentiment analysis indicates:

- **Swiggy performs better in Moderate and Elite consumer tiers.**
- Swiggy also shows stronger sentiment performance in the Premium segment in the broader storyboard narrative.
- **Zomato performs better in the Budget Friendly tier.**

This produces an interesting contrast with the financial dashboard.

The analysis therefore suggests that:

> A platform can perform better financially in a segment without necessarily having the highest customer-sentiment score in that same segment.

That divergence is analytically important because it prevents customer sentiment from being treated as a direct substitute for financial performance.

The dashboard also investigates whether stronger ratings translate into:

- more reviews,
- more orders,
- repeat customers,
- stronger restaurant-type revenue,
- and stronger cuisine/dish performance.

The city-level view adds another layer: sentiment and monthly order growth can move differently, meaning positive customer perception does not automatically imply positive short-term order growth.

---

# 🧑‍🍳 Dashboard 4 — Consumer Experience Analysis

### Worksheets included

- Consumer Experience Score Per Restaurant
- Consumer Experience Score by Restaurant Delivery
- Consumer Experience Score by Year
- Consumer Experience Score by Top Sold Dishes
- Consumer Experience Score by Restaurant Type

### Analytical purpose

This dashboard converts raw ratings and sentiment into a unified **Consumer Experience Score**.

### Full Storyboard Insight

The Consumer Experience Score broadly supports the segment-level pattern seen in the sentiment analysis:

- **Swiggy's experience/sentiment position is stronger in Premium and Elite segments.**
- **Zomato's position is stronger in Budget and Moderate segments.**

This creates consistency between the sentiment analysis and the composite experience framework.

The dashboard also examines the experience score through multiple operational lenses:

### Delivery

The analysis tests whether delivery time and delivery fee are associated with customer experience.

### Restaurant Type

The experience score is evaluated across different restaurant categories to identify differences in customer perception.

### Top-Selling Dishes

The project investigates whether highly ordered dishes also demonstrate stronger customer experience indicators.

### Time

The yearly trend allows experience behaviour to be viewed longitudinally rather than as a single cross-sectional value.

The important BI insight is that **customer experience is multidimensional**.

It is not represented by rating alone.

The project therefore combines normalized:

- Sentiment
- Rating

into a composite score and then breaks that score down by operational and commercial dimensions.

---

# 💵 Dashboard 5 — Swiggy vs Zomato Financial Analysis

### Worksheets included

- Platform Performance by Commission vs Consumer Tier
- Platform Performance by Revenue / Year / Restaurant
- Platform Performance by Profit / Year / Restaurant Type
- Platform Performance by Avg Cost Per Order vs Cost-to-Consumer % / Year Growth
- Platform Geospatial Performance Analysis
- Top KPI

### Analytical purpose

This dashboard examines the economic engine behind the two platforms.

It brings together:

- Revenue
- Profit
- Commission
- Expense
- Delivery fee
- Cost per order
- Cost-to-consumer percentage
- Restaurant type
- Geography
- Time

### Full Storyboard Insight

The storyboard highlights that **delivery fee, commission and estimated expense are relatively similar between the two platforms within the analysed framework**.

This matters because large differences in customer order counts cannot automatically be attributed to a large fee or commission differential.

The Moderate consumer tier becomes especially important:

- Swiggy shows stronger sentiment performance in the Moderate tier across the analysed decade.
- Zomato performs better in the Moderate tier on revenue and profit according to the storyboard.

This creates a clear **sentiment-versus-financial-performance divergence**.

The storyboard explicitly identifies this as an area requiring further investigation.

However, the project also recognises that the available dataset does not provide enough supporting variables to establish a causal explanation.

Therefore, the appropriate BI conclusion is:

> The data reveals a performance divergence worth investigating, but it does not establish causation.

This distinction is deliberately retained in the project rather than presenting correlation as causation.

---

# 📖 Dashboard 6 — Swiggy vs Zomato Comparison Analytics Storyboard

The storyboard acts as the executive narrative layer.

## Story Point 1 — Consumer Demographics

**Visible storyline:**

> The Mid-Range / Moderate consumer segment dominates the price segment and contributes approximately 50% of total revenue. Zomato performs better in revenue within the Moderate Consumer Tier.

### Complete analytical interpretation

The first story establishes the importance of consumer segmentation.

Instead of treating customers as a single population, the project separates spending behaviour into four tiers.

The Moderate segment becomes the central commercial segment because it combines meaningful order economics with a large share of revenue.

Zomato's stronger revenue performance in this segment provides the first indication that overall platform performance may be driven by a particular customer population.

This leads to the next analytical question:

**Does stronger revenue also translate into stronger profit?**

---

## Story Point 2 — Consumer-Tier Profitability

**Visible storyline:**

> Zomato performs well for Budget Friendly and Moderate consumers, while Swiggy performs well for Premium and Elite consumers in terms of profit.

### Complete analytical interpretation

The profitability dashboard shows a clear segmentation effect.

Zomato's stronger performance is concentrated in the lower-to-mid spending tiers, while Swiggy's stronger profitability appears in the higher spending tiers.

This means the two platforms demonstrate different economic patterns across customer value levels.

The insight is not simply:

> Platform A is profitable.

It is:

> Profitability varies by consumer tier.

That is a materially different BI finding because it suggests that customer mix can alter the interpretation of platform performance.

---

## Story Point 3 — Sentiment and Customer Behaviour

**Visible storyline:**

> Swiggy performs better in Moderate and Elite consumer tiers and dominates the Premium segment, while Zomato performs better for Budget Friendly consumers in sentiment.

### Complete analytical interpretation

Customer sentiment does not mirror the profitability pattern perfectly.

Swiggy's sentiment position becomes stronger as the analysis moves toward higher-value consumer groups, while Zomato has stronger sentiment performance in the Budget segment.

This introduces an important distinction between:

- customer perception,
- customer behaviour,
- financial performance.

The dashboard further examines reviews, repeat orders, top dishes, cuisines, restaurant types and city-level sentiment.

Therefore, sentiment is treated as a behavioural signal rather than a standalone business outcome.

---

## Story Point 4 — Composite Consumer Experience

**Visible storyline:**

> Consumer Experience Score supports the revenue/profit pattern: Swiggy has stronger experience/sentiment performance in Premium and Elite tiers, while Zomato is stronger in Budget and Moderate tiers.

### Complete analytical interpretation

The Consumer Experience Score provides an additional validation layer.

Instead of relying only on raw rating or sentiment, the project normalizes the two measures and combines them.

The resulting composite score broadly preserves the segment-level sentiment pattern.

This makes the experience analysis more robust from a BI perspective because the conclusion is not dependent on a single customer metric.

The dashboard then evaluates experience across:

- restaurant,
- delivery,
- year,
- restaurant type,
- top-selling dish.

This creates a multidimensional view of customer experience.

---

## Story Point 5 — Financial / Operational Divergence

**Visible storyline:**

> Delivery fee, commission and estimated expense are relatively similar for both platforms. Swiggy has stronger sentiment in the Moderate tier, while Zomato performs better in revenue and profit. The divergence requires further investigation, but current data limitations do not support causal investigation.

### Complete analytical interpretation

This is the most important diagnostic insight in the storyboard.

The data shows a divergence between customer sentiment and financial performance within the Moderate segment.

At the same time, delivery fee, commission and estimated expense do not show a sufficiently large difference in the analysed framework to directly explain the performance gap.

Therefore, several possible explanatory factors remain outside the current analytical scope.

The project deliberately does **not** claim causation.

Instead, it identifies the divergence as a **diagnostic opportunity** for a future dataset containing variables such as:

- customer acquisition cost,
- promotion-level discount value,
- delivery distance,
- delivery partner availability,
- restaurant commission contracts,
- customer retention,
- churn,
- order frequency,
- cohort behaviour,
- platform-specific customer acquisition,
- actual rather than estimated financial measures.

This is an example of BI being used to identify the next business question rather than forcing an unsupported answer.

---

# 🔍 Key Business Insights

## 1. Consumer segmentation changes the platform comparison

Overall platform numbers can hide meaningful differences between Budget, Moderate, Premium and Elite consumers.

## 2. Moderate consumers are commercially significant

The Moderate segment contributes approximately half of the analysed revenue in the storyboard and becomes a major driver of the comparison.

## 3. Revenue and profit do not tell the same story

Zomato's stronger revenue/profit position in the Moderate tier coexists with stronger Swiggy sentiment in that tier.

## 4. Premium and Elite economics favour a different pattern

Swiggy shows stronger profitability and consumer-experience/sentiment performance in higher-value segments within the analysed framework.

## 5. Budget behaviour differs from high-value behaviour

Zomato performs better on the analysed sentiment/experience indicators for Budget customers, while Swiggy's relative strength increases in higher-value tiers.

## 6. Customer experience is multidimensional

Rating alone is insufficient. The project combines normalized rating and sentiment into a composite Consumer Experience Score.

## 7. Operational economics require deeper investigation

Delivery fee, commission and estimated expense are relatively similar in the analysed comparison, so they do not by themselves explain every platform-performance difference.

## 8. Correlation is not treated as causation

Where the dataset cannot establish a causal mechanism, the storyboard explicitly labels the finding as an area for further investigation.

---

# 🧩 Filters & Dashboard Interactivity

The workbook uses interactive filters and dashboard actions across dimensions such as:

- Consumer Tier
- City
- Restaurant Name
- Restaurant Type
- Cuisine
- Platform
- Year / Listing Date
- Price Segment
- Top Selling Dish
- Geographic selection
- Quantitative ranges for selected measures

Several views also use **dashboard actions** such as city/restaurant selections to propagate analytical context across worksheets.

This supports exploratory BI rather than a static presentation.

---

# 🗺️ Geospatial Analysis

The project includes two geospatial analytical layers:

### Platform Geospatial Order Analysis

Used to understand the distribution of platform orders geographically.

### Platform Geospatial Performance Analysis

Used to investigate geographical variation in platform performance.

Geography is therefore treated as an analytical dimension rather than merely a visual map.

---

# 🍜 Food, Cuisine & Restaurant Analysis

The project extends beyond platform-level KPIs into restaurant and food behaviour.

Analyses include:

- Top-selling dishes
- Cuisine-level delivery time
- Cuisine-level ratings
- Repeat orders
- Restaurant-type revenue
- Restaurant-type sentiment
- Restaurant-level experience
- Restaurant-level ratings

This allows platform performance to be connected to the underlying restaurant ecosystem.

---

# 🧪 Analytical Methodology

### Layer 1 — Segmentation

Customers are segmented using average cost per order.

### Layer 2 — Platform Selection

A parameter allows Swiggy, Zomato or both to be selected.

### Layer 3 — Metric Selection

A separate parameter changes the KPI being evaluated.

### Layer 4 — Derived Metrics

Revenue, profit, margin, expense, delivery %, commission amount and experience metrics are calculated.

### Layer 5 — Normalization

Rating and sentiment are normalized using Min-Max scaling.

### Layer 6 — Composite Index

Normalized rating and sentiment are combined into Consumer Experience Score.

### Layer 7 — Comparative Logic

Metric-specific rules determine whether higher or lower values represent stronger performance.

### Layer 8 — Storytelling

The resulting analysis is organised into dashboards and a five-stage executive storyboard.

---

# ⚠️ Data & Analytical Limitations

This project should be interpreted as a **BI analytical case study based on the available dataset**, not as audited financial reporting.

Important limitations include:

- Revenue and profit measures are represented as estimated fields in the workbook.
- Commission is modelled as a percentage-based measure.
- Expense is derived from revenue minus estimated net profit.
- The dataset does not contain enough variables to establish causal explanations for every observed difference.
- Sentiment and rating are treated as analytical indicators and combined through a custom normalization framework.
- Composite scores depend on the selected normalization methodology.
- Some analytical fields represent modelled/derived values rather than directly reported company figures.
- The storyboard's Moderate-tier sentiment-versus-profit divergence should therefore be treated as a diagnostic finding rather than a causal conclusion.

---

# 🛠️ Tableau Techniques Demonstrated

This project demonstrates practical BI capabilities including:

- Calculated Fields
- Parameters
- Parameter-driven calculations
- Dynamic KPI selection
- Dynamic platform selection
- Dynamic consumer-tier filtering
- Boolean calculated filters
- Min-Max normalization
- Composite scoring
- Conditional comparison logic
- Aggregation logic
- KPI cards
- Trend analysis
- Segmentation
- Geographic analysis
- Dashboard actions
- Interactive filtering
- Cross-dimensional analysis
- Executive storytelling
- Multi-dashboard architecture
- Financial KPI modelling
- Customer-experience analytics
- Behavioural analytics

---

# 📚 Workbook Structure

### Worksheets

The workbook contains analytical views covering:

- City-based sentiment / monthly order growth
- Consumer experience by restaurant
- Consumer experience by delivery
- Consumer experience by restaurant type
- Consumer experience by top-selling dish
- Consumer experience over time
- Cuisine vs delivery time and ratings
- Commission per consumer tier
- Discounts per consumer tier
- Geospatial order analysis
- Geospatial performance analysis
- Market share vs orders
- Commission vs consumer tier
- Profit by restaurant type
- Revenue by restaurant
- Cost per order vs cost-to-consumer
- Profit trend
- Ratings per consumer tier
- Restaurant ratings
- Revenue trend
- Price segmentation
- Restaurant-type revenue distribution
- Sentiment vs ratings
- Top KPI
- Top-selling dish vs reviews/orders
- Top-selling dish/cuisine vs repeat orders

---

# 🚀 Why This Project Is More Than a Dashboard

The project is designed around a central BI principle:

> **A dashboard should not only display what happened; it should help explain where the difference occurs, which segment drives it, what metrics move together, and what question should be investigated next.**

The Swiggy-vs-Zomato comparison therefore moves through multiple analytical layers:

```text
Platform
   ↓
Consumer Tier
   ↓
Revenue / Orders / Profit
   ↓
Commission / Discount / Expense
   ↓
Ratings / Sentiment
   ↓
Consumer Experience
   ↓
Restaurant / Cuisine / Dish
   ↓
City / Geography
   ↓
Behaviour / Repeat Orders
   ↓
Executive Story
```

---

# 📌 Final Executive Takeaway

The project demonstrates that a two-platform comparison becomes substantially more informative when performance is segmented by **consumer economics and analysed across multiple business dimensions**.

The major pattern identified by the storyboard is not a single universal platform advantage.

Instead, the data shows **segment-specific differences**:

- Zomato shows stronger financial performance in the Budget/Moderate range in the analysed framework.
- Swiggy shows stronger profitability in Premium/Elite segments.
- Swiggy's sentiment/experience position is stronger in higher-value segments.
- Zomato's sentiment/experience position is stronger in the Budget/Moderate side of the segmentation.
- The Moderate segment is particularly important because it combines high revenue contribution with a notable divergence between sentiment and financial performance.
- Delivery fee, commission and estimated expense appear relatively similar within the analysed framework, leaving the Moderate-tier divergence as an open diagnostic question.

The most important outcome is therefore the **analytical framework itself**: it transforms a conventional platform comparison into an interactive BI system capable of segment-level diagnosis, metric switching, normalization, customer-experience scoring and executive storytelling.

---

# 🔗 Tableau Public

**Explore the interactive workbook:**

https://public.tableau.com/app/profile/somnath.roy7901/viz/PlatetoPlatform_TheBattleofGiants_SwiggyvsZomatoAnalysisReport/SwiggyvsZomatoComparisosnAnalyticsStoryboard?publish=yes

---

## 👤 Author

**Somnath Roy**

Business Intelligence / Data Analytics Portfolio Project

Focus areas demonstrated:

`Tableau` · `Business Intelligence` · `Data Visualization` · `Customer Analytics` · `Financial Analytics` · `Segmentation` · `KPI Design` · `Calculated Fields` · `Parameters` · `Data Storytelling`

---

## ⭐ Project Theme

**From Platform Comparison → to Consumer Segmentation → to Financial Diagnosis → to Customer Experience → to Behavioural Intelligence.**
