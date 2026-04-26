# Business Case Analysis  
## Promotion Effectiveness at a Fashion Retail Chain

---

## B1. Problem Formulation

### (a) Machine Learning Problem Definition

| Component        | Description |
|------------------|------------|
| Target Variable | `items_sold` (number of items sold per store per month) |
| Input Features | store_size, location_type, promotion_type, month, festival_flag, competition_density, footfall |
| Problem Type | Supervised Learning (Regression) |

**Justification:**  
The objective is to predict a continuous numerical outcome using historical labeled data, making this a regression problem.

---

### (b) Why "Items Sold" is Better than Revenue

| Metric        | Limitation |
|--------------|-----------|
| Revenue      | Affected by pricing, discounts, and promotions |
| Items Sold   | Direct measure of demand |

**Explanation:**
- Revenue can be misleading due to price variations across promotions.
- Items sold reflects true customer demand, making it a more reliable target.

**Key Principle:**  
Choose a target variable that directly aligns with the business objective.

---

### (c) Alternative Modeling Strategy

Instead of a single global model:

**Recommended Approach:**
- Segment-based models (Urban / Semi-Urban / Rural)
- Or include interaction features (e.g., promotion × location)

**Justification:**
- Customer behavior differs across regions
- Improves personalization and accuracy

---

## B2. Data and EDA Strategy

### (a) Data Integration

**Data Sources:**
- Transactions
- Store Attributes
- Promotion Details
- Calendar Data

**Join Keys:**
- `store_id`
- `transaction_date`

**Final Dataset Design:**

| Aspect | Description |
|------|------------|
| Grain | One row = one store per month |
| Target | Total items sold |
| Features | Aggregated monthly metrics |

**Aggregations:**
- Total items sold
- Monthly revenue
- Average basket size
- Footfall
- Promotion type
- Competition density
- Festival/weekend flags

---

### (b) Exploratory Data Analysis

| Analysis | Chart Type | Purpose | Impact |
|--------|----------|--------|--------|
| Promotion vs Sales | Bar Chart | Identify best promotions | Feature importance |
| Seasonality | Line Plot | Detect trends over time | Add time features |
| Store Type Comparison | Boxplot | Compare performance | Segmentation |
| Competition Impact | Scatter Plot | Analyze external factors | Better modeling |

---

### (c) Handling Data Imbalance

**Problem:**
- 80% of data has no promotion, leading to bias

**Solutions:**
- Oversampling promotion data
- Weighted models
- Separate models for promotion vs no promotion
- Balanced evaluation metrics

---

## B3. Model Evaluation and Deployment

### (a) Train-Test Strategy

| Approach | Description |
|--------|------------|
| Train Set | First ~2.5 years |
| Test Set | Last ~6 months |

**Why not random split?**
- Causes data leakage
- Leads to unrealistic evaluation

---

### Evaluation Metrics

| Metric | Meaning |
|------|--------|
| RMSE | Penalizes large errors |
| MAE  | Average prediction error |

**Interpretation:**
- Lower RMSE indicates fewer large errors  
- Lower MAE indicates better average prediction accuracy  

---

### (b) Explaining Model Recommendations

**Scenario:**
- December → Loyalty Points Bonus  
- March → Flat Discount  

**Explanation:**

| Factor | December | March |
|------|----------|-------|
| Season | Festival | Normal |
| Demand | High | Moderate |
| Strategy | Retention | Attraction |

**Insight:**
Promotions perform differently based on seasonal and demand-related factors.

---

### (c) Deployment Pipeline

**Step 1: Save Model**
```python
import joblib
joblib.dump(model, 'model.pkl')

###Step 2: Prepare Data
- Collect monthly store data  
- Apply the same preprocessing pipeline  

### Step 3: Generate Predictions
- Load model  
- Predict best promotion per store  

### Step 4: Automation
- Run a monthly batch pipeline  
- Deliver outputs via dashboard or report  

---

## Monitoring and Retraining

| Trigger | Action |
|--------|--------|
| Performance drop | Retrain model |
| Data drift | Update features |
| Seasonality change | Re-evaluate model |

---

## Final Summary
- Framed as a regression problem  
- Selected an appropriate target variable  
- Designed a structured dataset  
- Applied time-aware validation  
- Proposed a scalable deployment pipeline  

---

## Key Takeaway

Data-driven promotion strategies enable targeted decision-making and improved sales performance across diverse store segments.